# Multi-Omics Survival Modelling in Triple-Negative Breast Cancer

Integrating transcriptomic and genomic data to find survival-associated gene signatures in basal / triple-negative breast cancer (TNBC), and cross-checking candidate biomarkers across independent methods. MSc module project (AI for Personalised Medicine, UCD).

## Overview

TNBC has the worst prognosis of the major breast-cancer subtypes and lacks targeted therapies, so prognostic biomarker discovery is clinically valuable. This project asks whether **integrating RNA-seq and copy-number alteration (CNA) data** identifies survival-associated genes that either data type alone would miss, and whether candidates agree across modelling approaches.

Data: TCGA Breast Invasive Carcinoma (PanCancer Atlas, n = 1,084; 171 basal/TNBC patients).

## Approach

1. **Feature selection:** elastic-net penalised Cox regression over the combined RNA-seq + CNA feature matrix.
2. **Validation:** a random survival forest for independent variable-importance ranking.
3. **Biological interpretation:** PROGENy pathway activity scoring, KEGG enrichment, and STRING protein-interaction networks.
4. **Cross-method agreement:** genes selected by *both* the Cox model and the survival forest are treated as higher-confidence candidates.

## Key result

**KRTAP10-6** emerged as a top survival-associated gene across both independent methods (top risk coefficient in elastic-net Cox; highest variable importance in the survival forest), the kind of cross-method agreement that strengthens a biomarker hypothesis. Risk genes enriched for metabolic-reprogramming pathways; protective genes enriched for immune signalling, consistent with known TNBC biology.

> **Notes:** only 22 death events limited statistical power, and the survival forest reached a training C-index of 0.985 (clear overfitting, used for relative importance, not performance). Findings are hypothesis-generating and would need an external cohort to confirm.

## Repository structure

```
.
├── README.md
├── MO_modelling.qmd              # full analysis (Quarto / R): preprocessing → Cox → RSF → enrichment
├── brca_tcga_pan_can_atlas_2018/    # TCGA data (download separately)
└── results/                         # gene tables, figures (CSV / PDF)
```

The whole analysis lives in a single Quarto document; render it with `quarto render MO_modelling.qmd` (or run the chunks in RStudio).

## Data

TCGA Breast Invasive Carcinoma (PanCancer Atlas) is obtained via cBioPortal and is not committed here. Download the `brca_tcga_pan_can_atlas_2018` folder separately and place it alongside the `.qmd`.

## Tech stack

R / Quarto · `glmnet` · `survival` · `survminer` · `randomForestSRC` · `PROGENy` · `clusterProfiler` (KEGG) · `STRINGdb` · `corrplot`

## Acknowledgements

MSc AI for Medicine and Medical Research, University College Dublin (AI for Personalised Medicine).
