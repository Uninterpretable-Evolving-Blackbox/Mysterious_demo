# VEP AI Assistant

A prototype chatbot that recommends [Ensembl VEP](https://www.ensembl.org/info/docs/tools/vep/index.html) (Variant Effect Predictor) configuration based on your analysis scenario. Built as a GSoC demo.

The assistant uses a local LLM via [Ollama](https://ollama.com/) with a curated knowledge base of 22 VEP options and 8 scenario-to-recommendation training examples. It recommends which options to enable or disable, explains why, and generates a ready-to-use VEP command.

## Features

- **Scenario-based recommendations** -- describe your analysis (rare disease, cancer, GWAS, etc.) and get tailored VEP configuration
- **Decision trace** -- full transparency into retrieval scoring, option provenance, and confidence levels
- **VEP output explainer** -- explain consequence terms and annotations in plain language
- **Post-hoc constraint checker** -- automatically detects and corrects species restriction violations and option conflicts
- **Keyword-based retrieval** -- selects the most relevant training examples using word overlap (no embedding model needed)
- **Semantic retrieval** (`--semantic`) -- uses sentence-transformers embeddings for more accurate example and option retrieval

## Requirements

- Python 3.10+
- [Ollama](https://ollama.com/) running locally
- A pulled model (default: `qwen2.5:3b`)

## Setup

```bash
# Install Ollama (macOS)
brew install ollama

# Start Ollama and pull a model
ollama serve
ollama pull qwen2.5:3b

# Install Python dependency
pip install -r requirements.txt
```

## Usage

### 1. Interactive recommendation

```bash
python vep_assistant.py
```

Prompts you to describe your analysis scenario, then streams a recommendation with:
- Detected use case category
- Per-option enable/disable decisions with confidence and source citations
- A generated VEP command line

### 2. Recommendation with decision trace (`--explain`)

```bash
python vep_assistant.py --explain "I have germline exome variants from a rare disease patient"
```

Shows the full decision trace before the recommendation:
- **Layer 1: Retrieval transparency** -- all training examples ranked by relevance score with matched keywords
- **Layer 2: Option confidence map** -- priority and confidence for each option given the detected use case
- **Layer 3: Confidence scores** -- high/medium/low derived from `priority_by_use_case` metadata

### 3. VEP output explainer

```bash
python vep_assistant.py explain-result "Why is my variant annotated as splice_donor_variant?"
```

Explains VEP consequence terms and annotations using definitions from `vep_consequences.json`.

### 4. Semantic retrieval mode (`--semantic`)

```bash
python vep_assistant.py --semantic "I have germline exome variants from a rare disease patient"
python vep_assistant.py --semantic --explain "I have mouse variants from CRISPR editing in GRCm39"
```

Uses sentence-transformers (`BAAI/bge-small-en-v1.5`, ~130MB, CPU-only) to embed queries and match against training examples and VEP options by cosine similarity instead of keyword overlap. Requires `sentence-transformers`:

```bash
pip install sentence-transformers
```

When combined with `--explain`, the decision trace shows cosine similarity scores instead of word overlap counts.

### Additional flags

| Flag | Description |
|------|-------------|
| `--explain` | Show decision trace before recommendation |
| `--semantic` | Use embedding-based semantic retrieval instead of keyword overlap |
| `--no-check` | Skip post-hoc constraint checking |

### Inline query

```bash
python vep_assistant.py "I have somatic variants from a tumour-normal pair"
```

## Evaluation

Compare knowledge-base-enhanced recommendations against a bare model across 7 test scenarios:

```bash
# Keyword retrieval only (2 conditions: bare vs keyword KB)
python evaluate.py

# With semantic retrieval (3 conditions: bare vs keyword KB vs semantic KB)
python evaluate.py --semantic

# Specify a different model
python evaluate.py --model qwen2.5:7b
python evaluate.py --model qwen2.5:14b --semantic
```

| Flag | Description |
|------|-------------|
| `--semantic` | Add a third "with KB + semantic retrieval" condition |
| `--model MODEL` | Ollama model name (default: `VEP_MODEL` env var or `qwen2.5:3b`) |

Runs each test query with each condition, then scores against ground truth using precision, recall, and F1 for both enabled and disabled options. Also checks for species restriction and conflict violations. Results are saved to `results/evaluation_results.md`.

## Configuration

| Environment variable | Default | Description |
|---------------------|---------|-------------|
| `VEP_MODEL` | `qwen2.5:3b` | Ollama model name |
| `OLLAMA_BASE_URL` | `http://localhost:11434/v1` | Ollama API endpoint |

## Project structure

```
vep_assistant.py        # Main assistant (3 modes: recommend, explain, explain-result)
evaluate.py             # Evaluation: knowledge-base vs bare model comparison
vep_options.json        # 22 VEP options with structured metadata
training_examples.json  # 8 curated scenario-to-recommendation pairs
vep_consequences.json   # VEP consequence term definitions
requirements.txt        # Python dependencies (openai, sentence-transformers)
results/                # Saved recommendations and evaluation reports
```

## How it works

1. **Knowledge base loading** -- VEP options (with priorities, conflicts, species restrictions) and training examples are loaded from JSON files
2. **Retrieval** -- the user query is matched against training examples by word overlap (default) or cosine similarity over sentence embeddings (`--semantic`); top 2 examples are included in the prompt. In semantic mode, the top 10 most relevant options (out of 22) are also selected
3. **Prompt compression** -- options are compressed into a compact text format to fit within small model context windows
4. **LLM generation** -- the local model generates a recommendation with per-option decisions, source citations, and a VEP command
5. **Constraint checking** -- the response is parsed and checked for species restriction violations and option conflicts, which are auto-corrected with warnings

## Knowledge base

The knowledge base covers 7 use case categories:

| Category | Example scenario |
|----------|-----------------|
| Rare disease (germline) | Exome variants from a Mendelian disorder patient |
| Somatic cancer | Tumour-normal paired somatic variants |
| Regulatory / non-coding | GWAS hits in intergenic regions |
| Population genetics | Allele frequency comparison across populations |
| Structural variants | Large deletions/duplications from long-read WGS |
| Splice analysis | Variants near exon-intron boundaries |
| Quick lookup | Single rsID annotation |

Each of the 22 VEP options has metadata including:
- Priority per use case (critical / recommended / optional / not_applicable)
- Species restrictions (human-only vs all species)
- Conflicts with other options
- Dependencies
