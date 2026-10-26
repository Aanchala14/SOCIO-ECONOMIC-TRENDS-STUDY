# Socio-Economic Trends Study: Central Heating Deprivation and Health Outcomes in England & Wales (2011 & 2021)

This project analyses how household heating deprivation and health outcomes vary across Local Authorities in England and Wales, comparing 2011 and 2021 census data. The work combines data cleaning, geographic harmonisation, Bayesian regression, dimensionality reduction, and interactive Tableau visualisations to explore socio-economic drivers of poor heating access and related health outcomes.

## Research question

What socio-economic factors; occupational class, housing tenure, and age, predict whether a household lacks central heating across Local Authorities in England and Wales, and does the absence of heating correlate with worse self-reported health outcomes between 2011 and 2021?

## Key findings

- In 2011, the national mean proportion of households without central heating was 2.54% (median 2.27%) across Local Authority Districts.
- Private rental tenure was the dominant structural predictor of heating deprivation (standardised Bayesian Ridge coefficient: 1.43; 95% CI [1.34, 1.52]).
- The 65+ age group showed a higher no-heat rate (2.80%) compared with 0–15 year olds (1.07%).
- A Bayesian trend model projecting the 2011–2021 trajectory estimated a national mean of approximately 0.27% by 2031, with substantial uncertainty.
- Interactive Tableau dashboards (choropleth maps, ranked bar charts, and scatter plots) were used to communicate geographic patterns and relationships for policy and planning audiences.

## Project overview

The analysis pipeline is implemented in the notebook:
- `python_scripts/main.ipynb`

It covers:

1. Loading and inspecting raw census-style datasets
2. Cleaning and feature extraction
3. Merging the 2011 datasets into a single master table
4. Harmonising 2011 local authority boundaries to 2021 authorities
5. Assessing missing data
6. Imputing missing values with Bayesian Ridge via `IterativeImputer`
7. Standardising variables for analysis
8. Performing dimensionality reduction with PCA, t-SNE and MDS
9. Running Bayesian credible interval analysis for heating deprivation and health outcomes
10. Forecasting 2031 heating deprivation trends
11. Exporting datasets for Tableau visualisation

## Repository structure

```text
SOCIO-ECONOMIC-TRENDS-STUDY/
├── README.md
├── tableau_workbook.twbx
├── plots/
├── plots.pdf
├── _Report.pdf
├── downloaded_datasets/
│   ├── central_heating-2011.csv
│   ├── central_heating-2021.csv
│   ├── central_heating-age-2011.csv
│   ├── central_heating-tenure.csv
│   ├── health-2021.csv
│   ├── health-nssec-2011.csv
│   └── ...
├── python_scripts/
│   ├── main.ipynb
│   ├── master_dataset.csv
│   ├── data_2011_348_clean.csv
│   ├── pca_projection.csv
│   ├── tsne_projection.csv
│   ├── mds_projection.csv
│   ├── credible_intervals.csv
│   ├── trend_prediction_2031.csv
│   ├── health_regression_coefficients.csv
│   ├── hybrid_tableau_dataset_optimized.csv
│   └── ...
└── ...
```

## Data sources

The analysis uses local authority level census-derived files stored under `downloaded_datasets/`, including:

- central heating prevalence by local authority
- central heating by age group
- central heating by housing tenure
- self-reported health outcomes
- occupational class / NS-SEC indicators

These are combined and compared across the 2011 and 2021 geographies.

## Key methods

### Geographic harmonisation

Because several 2011 local authorities were merged into larger 2021 unitary authorities, the project aggregates the earlier district counts to 2021 boundaries before comparing the two periods. This avoids distortions that would result from comparing raw percentages across mismatched geographies.

### Bayesian imputation

Missing values are handled using `BayesianRidge` within `IterativeImputer` to estimate incomplete features while accounting for uncertainty.

### Bayesian inference

The analysis estimates posterior coefficients and 95% credible intervals for:

- predictors of no central heating
- predictors of poor health
- projected heating deprivation in 2031

### Dimensionality reduction

The dataset is reduced using:

- PCA
- t-SNE
- MDS

These are used to explore structure and support Tableau-based exploratory analysis.

## Output files

### Final analytical datasets

- `python_scripts/master_dataset.csv` — final 2021-boundary master dataset
- `python_scripts/data_2011_348_clean.csv` — cleaned 2011 dataset before harmonisation
- `python_scripts/hybrid_tableau_dataset_optimized.csv` — Tableau-friendly hybrid dataset for mapping and tooltip analysis

### Projection files

- `python_scripts/pca_projection.csv`
- `python_scripts/tsne_projection.csv`
- `python_scripts/mds_projection.csv`

### Bayesian outputs

- `python_scripts/credible_intervals.csv`
- `python_scripts/trend_prediction_2031.csv`
- `python_scripts/health_regression_coefficients.csv`

### Visual outputs

The notebook saves plots for:

- credible intervals
- trend prediction to 2031
- health regression coefficients
- PCA, t-SNE and related visualisations

## How to run the analysis

1. Open the project in a Python environment.
2. Install the required packages:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn umap-learn arviz
```

3. Run the notebook cells in `python_scripts/main.ipynb` in order.
4. Generated outputs will be written to the `python_scripts/` folder.

## Tableau

The project includes:

- `tableau_workbook.twbx`
- Tableau-friendly CSV exports for visual analytics and map-based exploration

This is designed for exploratory dashboarding and comparison of local authority-level outcomes across 2011 and 2021.

## Notes

- The project focuses on Local Authorities in England and Wales.
- Boundary harmonisation is crucial for valid decade-to-decade comparison.
- The analysis emphasises uncertainty, using credible intervals rather than only point estimates.

## Summary

This repository provides a reproducible socio-economic trend study using official local authority data to identify how heating deprivation and health outcomes vary spatially and over time. It combines quantitative modelling with visual analytics for communication and dashboarding.
