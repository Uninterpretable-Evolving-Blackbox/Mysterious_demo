# VEP Assistant Evaluation Results

**Date:** 2026-03-16T18:49:50.816076
**Model:** qwen2.5:14b
**Temperature:** 0.7
**Max tokens:** 4096

## Per-Query Results

### test_rare_disease
**Query:** I use VEP to annotate my VCF. I have exome data from a rare disease patient and I would like to know if there is a way, if a variant has a high impact in a non-canonical transcript, to keep it and the annotations in the canonical. What options should I enable for clinical reporting?

**Source:** [https://www.biostars.org/p/9517871/](https://www.biostars.org/p/9517871/)

**Ground truth use case:** rare_disease_germline

| Metric | Without KB | With KB (keyword) | With KB (all examples) | With KB (semantic) |
|--------|---|---|---|---|
| Options detected | 3 en / 2 dis | 18 en / 3 dis | 16 en / 6 dis | 14 en / 0 dis |
| Enable precision | 67% | 72% | 75% | 64% |
| Enable recall | 12% | 81% | 75% | 56% |
| Enable F1 | 21% | 76% | 75% | 60% |
| Disable precision | 0% | 33% | 33% | 0% |
| Disable recall | 0% | 33% | 67% | 0% |
| Disable F1 | 0% | 33% | 44% | 0% |
| Species violations | 0 | 0 | 0 | 0 |
| Conflict violations | 0 | 0 | 0 | 7 |
| Use case detected | unknown (incorrect) | rare_disease_germline (correct) | rare_disease_germline (correct) | rare_disease_germline (correct) |
| Citation rate | 0% (0/3 cited) | 76% (19/25 cited) | 79% (19/24 cited) | 94% (16/17 cited) |

### test_non_human
**Query:** We performed CRISPR knockouts in mouse embryonic stem cells and called variants from WGS against the GRCm39 reference. What VEP settings should I use?

**Ground truth use case:** non_human

| Metric | Without KB | With KB (keyword) | With KB (all examples) | With KB (semantic) |
|--------|---|---|---|---|
| Options detected | 9 en / 0 dis | 14 en / 0 dis | 19 en / 2 dis | 18 en / 0 dis |
| Enable precision | 44% | 50% | 42% | 39% |
| Enable recall | 44% | 78% | 89% | 78% |
| Enable F1 | 44% | 61% | 57% | 52% |
| Disable precision | 0% | 0% | 50% | 0% |
| Disable recall | 0% | 0% | 10% | 0% |
| Disable F1 | 0% | 0% | 17% | 0% |
| Species violations | 4 | 7 | 10 | 10 |
| Conflict violations | 0 | 0 | 0 | 0 |
| Use case detected | non_human (correct) | rare_disease_germline (incorrect) | rare_disease_germline (incorrect) | rare_disease_germline (incorrect) |
| Citation rate | 0% (0/0 cited) | 95% (20/21 cited) | 74% (20/27 cited) | 100% (19/19 cited) |

*Species violations (Without KB):* {'regulatory', 'polyphen', 'sift', 'clinvar_sv'}

*Species violations (With KB (keyword)):* {'gnomad_af', 'alphamissense', 'sift', 'cadd', 'clinvar', 'mane_select', 'regulatory'}

*Species violations (With KB (all examples)):* {'gnomad_af', 'alphamissense', 'clinvar_sv', 'sift', 'polyphen', 'cadd', 'revel', 'clinvar', 'mane_select', 'regulatory'}

*Species violations (With KB (semantic)):* {'gnomad_af', 'alphamissense', 'sift', 'spliceai', 'polyphen', 'cadd', 'revel', 'clinvar', 'mane_select', 'regulatory'}

### test_regulatory
**Query:** I have a set of GWAS hits in non-coding regions — mostly intronic and intergenic SNPs. I need to figure out if any overlap regulatory elements and identify possible target genes.

**Ground truth use case:** regulatory_noncoding

| Metric | Without KB | With KB (keyword) | With KB (all examples) | With KB (semantic) |
|--------|---|---|---|---|
| Options detected | 3 en / 0 dis | 12 en / 0 dis | 21 en / 0 dis | 14 en / 0 dis |
| Enable precision | 33% | 67% | 43% | 50% |
| Enable recall | 11% | 89% | 100% | 78% |
| Enable F1 | 17% | 76% | 60% | 61% |
| Disable precision | 0% | 0% | 0% | 0% |
| Disable recall | 0% | 0% | 0% | 0% |
| Disable F1 | 0% | 0% | 0% | 0% |
| Species violations | 0 | 0 | 0 | 0 |
| Conflict violations | 0 | 0 | 9 | 0 |
| Use case detected | non_human (incorrect) | rare_disease_germline (incorrect) | rare_disease_germline (incorrect) | rare_disease_germline (incorrect) |
| Citation rate | 0% (0/1 cited) | 100% (23/23 cited) | 95% (20/21 cited) | 87% (20/23 cited) |

### test_structural
**Query:** Does VEP do a good job at annotating structural variants from CNVkit, Manta, Lumpy? I have large deletions and duplications and need to identify clinically relevant SVs and filter out common ones.

**Source:** [https://www.biostars.org/p/181819/](https://www.biostars.org/p/181819/)

**Ground truth use case:** structural_variants

| Metric | Without KB | With KB (keyword) | With KB (all examples) | With KB (semantic) |
|--------|---|---|---|---|
| Options detected | 2 en / 0 dis | 12 en / 0 dis | 6 en / 0 dis | 6 en / 0 dis |
| Enable precision | 50% | 58% | 50% | 67% |
| Enable recall | 11% | 78% | 33% | 44% |
| Enable F1 | 18% | 67% | 40% | 53% |
| Disable precision | 0% | 0% | 0% | 0% |
| Disable recall | 0% | 0% | 0% | 0% |
| Disable F1 | 0% | 0% | 0% | 0% |
| Species violations | 0 | 0 | 0 | 0 |
| Conflict violations | 0 | 0 | 0 | 0 |
| Use case detected | structural_variants (correct) | rare_disease_germline (incorrect) | structural_variants (correct) | structural_variants (correct) |
| Citation rate | 0% (0/1 cited) | 100% (22/22 cited) | 95% (21/22 cited) | 100% (15/15 cited) |

### test_somatic_cancer
**Query:** I'm relatively new to analyzing variants data generated by WES in a cohort of cancer patients. I've called variants using Mutect2 and now I want to annotate these variants with information such as whether they are known variants in dbSNP and their pathogenicity prediction, whether it's known in ExAC etc. What VEP options should I use?

**Source:** [https://www.biostars.org/p/9479508/](https://www.biostars.org/p/9479508/)

**Ground truth use case:** somatic_cancer

| Metric | Without KB | With KB (keyword) | With KB (all examples) | With KB (semantic) |
|--------|---|---|---|---|
| Options detected | 10 en / 0 dis | 18 en / 0 dis | 8 en / 0 dis | 7 en / 0 dis |
| Enable precision | 70% | 72% | 75% | 43% |
| Enable recall | 54% | 100% | 46% | 23% |
| Enable F1 | 61% | 84% | 57% | 30% |
| Disable precision | 0% | 0% | 0% | 0% |
| Disable recall | 0% | 0% | 0% | 0% |
| Disable F1 | 0% | 0% | 0% | 0% |
| Species violations | 0 | 0 | 0 | 0 |
| Conflict violations | 0 | 0 | 0 | 0 |
| Use case detected | non_human (incorrect) | rare_disease_germline (incorrect) | somatic_cancer (correct) | somatic_cancer (correct) |
| Citation rate | 0% (0/1 cited) | 100% (20/20 cited) | 100% (14/14 cited) | 100% (8/8 cited) |

### test_population_large_vcf
**Query:** I am trying to annotate WGS VCF files through VEP, and even on multi-threading the process is painfully slow. The VCF sizes range between 1-1.5 Gb with about 2 million variants. Apart from gene and functional impact level annotation, I am using VEP plugins for CADD and gnomAD genome based frequencies. What options do you recommend?

**Source:** [https://www.biostars.org/p/336474/](https://www.biostars.org/p/336474/)

**Ground truth use case:** population_genetics

| Metric | Without KB | With KB (keyword) | With KB (all examples) | With KB (semantic) |
|--------|---|---|---|---|
| Options detected | 4 en / 0 dis | 15 en / 0 dis | 11 en / 0 dis | 7 en / 0 dis |
| Enable precision | 25% | 40% | 36% | 29% |
| Enable recall | 14% | 86% | 57% | 29% |
| Enable F1 | 18% | 55% | 44% | 29% |
| Disable precision | 0% | 0% | 0% | 0% |
| Disable recall | 0% | 0% | 0% | 0% |
| Disable F1 | 0% | 0% | 0% | 0% |
| Species violations | 0 | 0 | 0 | 0 |
| Conflict violations | 0 | 0 | 0 | 0 |
| Use case detected | unknown (incorrect) | somatic_cancer (incorrect) | rare_disease_germline (incorrect) | rare_disease_germline (incorrect) |
| Citation rate | 0% (0/0 cited) | 100% (18/18 cited) | 100% (14/14 cited) | 100% (7/7 cited) |

### test_quick
**Query:** Does anyone know how gnomAD allele frequencies as outputted by Ensembl's VEP should be interpreted? I just want to quickly look up a single variant — rs1799945 — and check if it is clinically significant.

**Source:** [https://www.biostars.org/p/355992/](https://www.biostars.org/p/355992/)

**Ground truth use case:** quick_lookup

| Metric | Without KB | With KB (keyword) | With KB (all examples) | With KB (semantic) |
|--------|---|---|---|---|
| Options detected | 4 en / 0 dis | 19 en / 0 dis | 14 en / 1 dis | 11 en / 0 dis |
| Enable precision | 100% | 68% | 71% | 73% |
| Enable recall | 29% | 93% | 71% | 57% |
| Enable F1 | 44% | 79% | 71% | 64% |
| Disable precision | 0% | 0% | 0% | 0% |
| Disable recall | 0% | 0% | 0% | 0% |
| Disable F1 | 0% | 0% | 0% | 0% |
| Species violations | 0 | 0 | 0 | 0 |
| Conflict violations | 0 | 0 | 0 | 0 |
| Use case detected | non_human (incorrect) | rare_disease_germline (incorrect) | rare_disease_germline (incorrect) | rare_disease_germline (incorrect) |
| Citation rate | 0% (0/2 cited) | 100% (20/20 cited) | 95% (19/20 cited) | 89% (17/19 cited) |

## Summary

| Metric | Without KB | With KB (keyword) | With KB (all examples) | With KB (semantic) | Δ (keyword vs bare) | Δ (all examples vs bare) | Δ (semantic vs bare) |
|--------|---|---|---|---|---|---|---|
| Enable F1 | 32% | 71% | 58% | 50% | +39% | +26% | +18% |
| Disable F1 | 0% | 5% | 9% | 0% | +5% | +9% | +0% |
| Enable Precision | 56% | 61% | 56% | 52% | +5% | +0% | -4% |
| Enable Recall | 25% | 86% | 67% | 52% | +61% | +42% | +27% |
| Species violations (total) | 4 | 7 | 10 | 10 | +3 | +6 | +6 |
| Conflict violations (total) | 0 | 0 | 9 | 7 | +0 | +9 | +7 |
| Use case accuracy | 2/7 (29%) | 1/7 (14%) | 3/7 (43%) | 3/7 (43%) | -1 | +1 | +1 |
| Citation rate (avg) | 0% | 96% | 91% | 96% | +96% | +91% | +96% |
