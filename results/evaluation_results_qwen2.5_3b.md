# VEP Assistant Evaluation Results

**Date:** 2026-03-16T18:36:51.743781
**Model:** qwen2.5:3b
**Temperature:** 0.7
**Max tokens:** 4096

## Per-Query Results

### test_rare_disease
**Query:** I use VEP to annotate my VCF. I have exome data from a rare disease patient and I would like to know if there is a way, if a variant has a high impact in a non-canonical transcript, to keep it and the annotations in the canonical. What options should I enable for clinical reporting?

**Source:** [https://www.biostars.org/p/9517871/](https://www.biostars.org/p/9517871/)

**Ground truth use case:** rare_disease_germline

| Metric | Without KB | With KB (keyword) | With KB (all examples) | With KB (semantic) |
|--------|---|---|---|---|
| Options detected | 1 en / 0 dis | 3 en / 0 dis | 14 en / 0 dis | 7 en / 1 dis |
| Enable precision | 100% | 67% | 71% | 57% |
| Enable recall | 6% | 12% | 62% | 25% |
| Enable F1 | 12% | 21% | 67% | 35% |
| Disable precision | 0% | 0% | 0% | 0% |
| Disable recall | 0% | 0% | 0% | 0% |
| Disable F1 | 0% | 0% | 0% | 0% |
| Species violations | 0 | 0 | 0 | 0 |
| Conflict violations | 0 | 0 | 5 | 4 |
| Use case detected | unknown (incorrect) | rare_disease_germline (correct) | rare_disease_germline (correct) | rare_disease_germline (correct) |
| Citation rate | 0% (0/1 cited) | 75% (3/4 cited) | 33% (2/6 cited) | 42% (5/12 cited) |

### test_non_human
**Query:** We performed CRISPR knockouts in mouse embryonic stem cells and called variants from WGS against the GRCm39 reference. What VEP settings should I use?

**Ground truth use case:** non_human

| Metric | Without KB | With KB (keyword) | With KB (all examples) | With KB (semantic) |
|--------|---|---|---|---|
| Options detected | 0 en / 0 dis | 8 en / 0 dis | 12 en / 1 dis | 17 en / 5 dis |
| Enable precision | 0% | 25% | 42% | 41% |
| Enable recall | 0% | 22% | 56% | 78% |
| Enable F1 | 0% | 24% | 48% | 54% |
| Disable precision | 0% | 0% | 100% | 80% |
| Disable recall | 0% | 0% | 10% | 40% |
| Disable F1 | 0% | 0% | 18% | 53% |
| Species violations | 0 | 6 | 7 | 7 |
| Conflict violations | 0 | 0 | 0 | 9 |
| Use case detected | unknown (incorrect) | regulatory_noncoding (incorrect) | population_genetics (incorrect) | rare_disease_germline (incorrect) |
| Citation rate | 0% (0/0 cited) | 100% (14/14 cited) | 90% (9/10 cited) | 80% (16/20 cited) |

*Species violations (Without KB):* none

*Species violations (With KB (keyword)):* {'regulatory', 'spliceai', 'alphamissense', 'sift', 'cadd', 'mane_select'}

*Species violations (With KB (all examples)):* {'revel', 'spliceai', 'alphamissense', 'sift', 'cadd', 'clinvar', 'mane_select'}

*Species violations (With KB (semantic)):* {'revel', 'gnomad_af', 'sift', 'polyphen', 'cadd', 'clinvar', 'mane_select'}

### test_regulatory
**Query:** I have a set of GWAS hits in non-coding regions — mostly intronic and intergenic SNPs. I need to figure out if any overlap regulatory elements and identify possible target genes.

**Ground truth use case:** regulatory_noncoding

| Metric | Without KB | With KB (keyword) | With KB (all examples) | With KB (semantic) |
|--------|---|---|---|---|
| Options detected | 1 en / 0 dis | 13 en / 3 dis | 8 en / 6 dis | 3 en / 7 dis |
| Enable precision | 100% | 31% | 38% | 33% |
| Enable recall | 11% | 44% | 33% | 11% |
| Enable F1 | 20% | 36% | 35% | 17% |
| Disable precision | 0% | 100% | 67% | 43% |
| Disable recall | 0% | 30% | 40% | 30% |
| Disable F1 | 0% | 46% | 50% | 35% |
| Species violations | 0 | 0 | 0 | 0 |
| Conflict violations | 0 | 0 | 0 | 0 |
| Use case detected | unknown (incorrect) | rare_disease_germline (incorrect) | somatic_cancer (incorrect) | regulatory_noncoding (correct) |
| Citation rate | 0% (0/3 cited) | 77% (10/13 cited) | 67% (16/24 cited) | 100% (6/6 cited) |

### test_structural
**Query:** Does VEP do a good job at annotating structural variants from CNVkit, Manta, Lumpy? I have large deletions and duplications and need to identify clinically relevant SVs and filter out common ones.

**Source:** [https://www.biostars.org/p/181819/](https://www.biostars.org/p/181819/)

**Ground truth use case:** structural_variants

| Metric | Without KB | With KB (keyword) | With KB (all examples) | With KB (semantic) |
|--------|---|---|---|---|
| Options detected | 4 en / 0 dis | 9 en / 0 dis | 14 en / 3 dis | 1 en / 1 dis |
| Enable precision | 50% | 33% | 43% | 0% |
| Enable recall | 22% | 33% | 67% | 0% |
| Enable F1 | 31% | 33% | 52% | 0% |
| Disable precision | 0% | 0% | 33% | 100% |
| Disable recall | 0% | 0% | 8% | 8% |
| Disable F1 | 0% | 0% | 13% | 15% |
| Species violations | 0 | 0 | 0 | 0 |
| Conflict violations | 0 | 0 | 0 | 0 |
| Use case detected | structural_variants (correct) | structural_variants (correct) | somatic_cancer (incorrect) | structural_variants (correct) |
| Citation rate | 0% (0/1 cited) | 100% (7/7 cited) | 62% (13/21 cited) | 0% (0/7 cited) |

### test_somatic_cancer
**Query:** I'm relatively new to analyzing variants data generated by WES in a cohort of cancer patients. I've called variants using Mutect2 and now I want to annotate these variants with information such as whether they are known variants in dbSNP and their pathogenicity prediction, whether it's known in ExAC etc. What VEP options should I use?

**Source:** [https://www.biostars.org/p/9479508/](https://www.biostars.org/p/9479508/)

**Ground truth use case:** somatic_cancer

| Metric | Without KB | With KB (keyword) | With KB (all examples) | With KB (semantic) |
|--------|---|---|---|---|
| Options detected | 4 en / 0 dis | 16 en / 1 dis | 15 en / 0 dis | 3 en / 0 dis |
| Enable precision | 50% | 62% | 53% | 67% |
| Enable recall | 15% | 77% | 62% | 15% |
| Enable F1 | 24% | 69% | 57% | 25% |
| Disable precision | 0% | 100% | 0% | 0% |
| Disable recall | 0% | 17% | 0% | 0% |
| Disable F1 | 0% | 29% | 0% | 0% |
| Species violations | 0 | 0 | 0 | 0 |
| Conflict violations | 0 | 0 | 0 | 0 |
| Use case detected | unknown (incorrect) | somatic_cancer (correct) | somatic_cancer (correct) | somatic_cancer (correct) |
| Citation rate | 0% (0/1 cited) | 0% (0/0 cited) | 89% (17/19 cited) | 100% (3/3 cited) |

### test_population_large_vcf
**Query:** I am trying to annotate WGS VCF files through VEP, and even on multi-threading the process is painfully slow. The VCF sizes range between 1-1.5 Gb with about 2 million variants. Apart from gene and functional impact level annotation, I am using VEP plugins for CADD and gnomAD genome based frequencies. What options do you recommend?

**Source:** [https://www.biostars.org/p/336474/](https://www.biostars.org/p/336474/)

**Ground truth use case:** population_genetics

| Metric | Without KB | With KB (keyword) | With KB (all examples) | With KB (semantic) |
|--------|---|---|---|---|
| Options detected | 9 en / 0 dis | 9 en / 0 dis | 8 en / 0 dis | 10 en / 0 dis |
| Enable precision | 33% | 22% | 25% | 20% |
| Enable recall | 43% | 29% | 29% | 29% |
| Enable F1 | 38% | 25% | 27% | 24% |
| Disable precision | 0% | 0% | 0% | 0% |
| Disable recall | 0% | 0% | 0% | 0% |
| Disable F1 | 0% | 0% | 0% | 0% |
| Species violations | 0 | 0 | 0 | 0 |
| Conflict violations | 0 | 0 | 0 | 0 |
| Use case detected | structural_variants (incorrect) | population_genetics (correct) | population_genetics (correct) | structural_variants (incorrect) |
| Citation rate | 0% (0/2 cited) | 0% (0/8 cited) | 86% (6/7 cited) | 100% (6/6 cited) |

### test_quick
**Query:** Does anyone know how gnomAD allele frequencies as outputted by Ensembl's VEP should be interpreted? I just want to quickly look up a single variant — rs1799945 — and check if it is clinically significant.

**Source:** [https://www.biostars.org/p/355992/](https://www.biostars.org/p/355992/)

**Ground truth use case:** quick_lookup

| Metric | Without KB | With KB (keyword) | With KB (all examples) | With KB (semantic) |
|--------|---|---|---|---|
| Options detected | 2 en / 0 dis | 15 en / 1 dis | 12 en / 0 dis | 4 en / 1 dis |
| Enable precision | 100% | 87% | 75% | 50% |
| Enable recall | 14% | 93% | 64% | 14% |
| Enable F1 | 25% | 90% | 69% | 22% |
| Disable precision | 0% | 0% | 0% | 0% |
| Disable recall | 0% | 0% | 0% | 0% |
| Disable F1 | 0% | 0% | 0% | 0% |
| Species violations | 0 | 0 | 0 | 0 |
| Conflict violations | 0 | 0 | 0 | 0 |
| Use case detected | unknown (incorrect) | rare_disease_germline (incorrect) | rare_disease_germline (incorrect) | population_genetics (incorrect) |
| Citation rate | 0% (0/0 cited) | 41% (7/17 cited) | 100% (10/10 cited) | 67% (2/3 cited) |

## Summary

| Metric | Without KB | With KB (keyword) | With KB (all examples) | With KB (semantic) | Δ (keyword vs bare) | Δ (all examples vs bare) | Δ (semantic vs bare) |
|--------|---|---|---|---|---|---|---|
| Enable F1 | 21% | 43% | 51% | 25% | +21% | +29% | +4% |
| Disable F1 | 0% | 11% | 12% | 15% | +11% | +12% | +15% |
| Enable Precision | 62% | 47% | 50% | 38% | -15% | -12% | -24% |
| Enable Recall | 16% | 44% | 53% | 25% | +28% | +37% | +9% |
| Species violations (total) | 0 | 6 | 7 | 7 | +6 | +7 | +7 |
| Conflict violations (total) | 0 | 0 | 5 | 13 | +0 | +5 | +13 |
| Use case accuracy | 1/7 (14%) | 4/7 (57%) | 3/7 (43%) | 4/7 (57%) | +3 | +2 | +3 |
| Citation rate (avg) | 0% | 56% | 75% | 70% | +56% | +75% | +70% |
