# When dengue outgrows the model

**Urban transmission regimes and season-ahead forecasting in Bangladesh**

This repository holds the analysis code for the manuscript *"When dengue outgrows the model: urban transmission regimes and season-ahead forecasting in Bangladesh"* (submitted to *City and Environment Interactions*). One notebook reproduces every table, data figure and number in the paper.

## What the study does

Using daily reported dengue cases and weather for the eight divisions of Bangladesh (January 2022 to October 2025), the notebook:

1. characterises two transmission regimes: persistent transmission in Dhaka and intermittent, zero-inflated transmission elsewhere;
2. compares population density with incidence, and the Dhaka city corporations with the rest of Dhaka Division;
3. describes season timing, the spatial lead–lag between divisions and lagged climate associations;
4. evaluates forecasts 1, 7 and 14 days ahead in three season-ahead folds (2023, 2024 and a 2025 hold-out), with persistence and moving-average baselines;
5. shows why count-level tree ensembles cannot forecast beyond their training range in a record season, and tests a level-anchored LightGBM model that removes this ceiling;
6. runs feature-group ablations (weather, calendar, census covariates), threshold alerts and season-ahead conformal prediction intervals.

## Repository contents

| File | Description |
|---|---|
| `urban-dengue-regimes.ipynb` | The complete analysis (Sections 0–11) |
| `README.md` | This file |

## Data

The notebook uses the open dataset:

> Rahman, A. (2026). *Daily Dengue Data of Bangladesh 2022–2025* [Data set, version 1]. Kaggle. Licence: CC BY 4.0.
> https://www.kaggle.com/datasets/brownsugar297/dengue-and-weather-data-bangladesh-20222025

- **Dengue counts:** daily reported patients by division, from the national dengue surveillance of the Directorate General of Health Services (DGHS), Bangladesh.
- **Weather:** daily maximum and minimum temperature, rainfall and relative humidity. The dataset documentation states these come from the Open-Meteo Historical Weather API, which uses the ERA5 reanalysis.
- **Census covariates:** division population and area from the Bangladesh Population and Housing Census 2022 (preliminary report). They are written into the notebook, so no extra file is needed.
- **Dhaka city-corporation figures:** published annual DGHS totals, written into Section 2b with their sources.

The notebook expects a file named `Dataset.csv` with the columns `date, division, Patients, max temp, min temp, rainfall, humidity`.

## How to run

### On Kaggle (recommended)

1. Create a new notebook and import `urban-dengue-regimes.ipynb` (*File → Import Notebook*).
2. Click *Add Input* and attach the dataset above.
3. Open *Settings* and turn *Internet* on. This is only needed for the optional version-pinning cell.
4. Click *Run All*. A CPU session is enough; the run takes about 10–20 minutes.
5. The outputs are written to `/kaggle/working/outputs/`.

### Locally

```bash
pip install numpy pandas scipy matplotlib scikit-learn==1.9.1 xgboost==3.1.3 lightgbm==4.7.0 catboost==1.2.10 jupyter
```

Put `Dataset.csv` in the same folder as the notebook and run all cells.

### Reproducing the paper's numbers exactly

The paper's results were produced with **xgboost 3.1.3, lightgbm 4.7.0, catboost 1.2.10 and scikit-learn 1.9.1**, with random seed 42. XGBoost results change slightly between versions. To pin the versions, set `PIN_VERSIONS = True` in the first code cell, run that cell, restart the kernel and then run all cells. A second run on another machine, with newer numpy and pandas, gave identical results.

## Outputs

| Folder | Contents |
|---|---|
| `outputs/results/cei_results.json` | Every number used in the manuscript |
| `outputs/tables/` | Result tables as CSV files |
| `outputs/figures/` | Figures 3–11 as vector PDF, plus 600-dpi PNG and TIFF |

## Notebook sections

| Section | Content |
|---|---|
| 0 | Setup, library versions, data loading, census covariates |
| 1 | Dataset characterisation |
| 2 | Urban gradient across divisions |
| 2b | Dhaka city corporations vs. the rest of Dhaka Division |
| 3 | Season timing by division and year |
| 4 | Spatial lead–lag between Dhaka and the other divisions |
| 5 | Lagged climate–dengue associations |
| 6 | Season-ahead, multi-horizon forecasting and the extrapolation diagnostic |
| 7 | Skill by division and moving-block bootstrap confidence intervals |
| 8 | Feature-group ablation |
| 9 | Outbreak alerts |
| 10 | Season-ahead conformal prediction intervals |
| 11 | Export of all results |

## Citation

If you use this code, please cite the article, which is currently under review. The full reference will be added here once it is published.

> Bangabashi, M. M., et al. When dengue outgrows the model: urban transmission regimes and season-ahead forecasting in Bangladesh. *City and Environment Interactions* (under review).

Please also cite the dataset (Rahman, 2026) listed above.

## Licence

The code in this repository is released under the MIT Licence (see `LICENSE`). The dataset belongs to its creator and is covered by its own CC BY 4.0 licence.

## Contact

Md. Maruf Bangabashi, Department of Computer Science and Engineering, Dhaka International University, Dhaka, Bangladesh. Email: marufbangabashi@gmail.com
