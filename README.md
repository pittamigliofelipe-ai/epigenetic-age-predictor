# Epigenetic Age Predictor

A machine learning project that predicts biological age from DNA methylation data using ElasticNet regression — inspired by epigenetic clocks like Horvath's model.

## Overview

Biological age and chronological age are not always the same. Epigenetic clocks measure DNA methylation patterns across CpG sites to estimate how old a person's cells actually are, independent of their birth date. This project explores that concept using two public datasets and a linear model.

## Datasets

| Dataset | Source | Tissue | Samples | Age Range |
|--------|--------|--------|---------|-----------|
| GSE139307 | GEO / pyaging | Sperm | 37 | 65–94 years |
| GSE41169 | GEO / biolearn | Blood | 95 | 18–65 years |

## Results

| Dataset | Mean MAE | Notes |
|--------|----------|-------|
| GSE139307 | 6.28 years | Small sample size limits generalization |
| GSE41169 | 8.05 years | Wider age range, skewed toward young adults |

## Key Observations

- Both models show a **regression toward the mean** — extreme ages are pulled toward the dataset average, a known limitation with small or skewed datasets.
- The sperm dataset (GSE139307) produced a case where a 94-year-old donor was predicted as ~73, suggesting potentially slower epigenetic aging — consistent with what epigenetic clocks are designed to detect.
- Dimensionality reduction to the top 1000 CpGs by variance was necessary to avoid memory issues with ~485k features.

## Methods

- Feature selection: top 1000 CpG sites by variance
- Model: ElasticNet regression (handles high-dimensional biological data well)
- Evaluation: 5-fold cross-validation
- Missing values: imputed with column mean

## Dependencies
```
pyaging
biolearn
scikit-learn
pandas
numpy
matplotlib
```

## Future Work

- Test on larger datasets (GSE40279, UK Biobank subsets)
- Implement Horvath's original 353-CpG clock for comparison
- Explore tissue-specific aging differences
