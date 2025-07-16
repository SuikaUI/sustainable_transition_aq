# Recoding Our Energy Future: A Data-Driven Analysis of Sustainable Transition and Air Quality

## Overview

This project mainly pivoting on a theme **“Recode The Earth: Digital Innovation for a Sustainable Future.”** Our goal is to leverage advanced data science and machine learning to unravel the complex relationship between sustainable energy transitions and air quality at a global scale.

We combine two rich, complementary datasets:
- **Global Data on Sustainable Energy (2000–2020):** Annual, country-level indicators on energy access, renewable energy, fossil fuel consumption, CO₂ emissions, and economic metrics.
- **Global Air Pollution Dataset:** City-level, cross-sectional air quality measurements for key pollutants (PM2.5, PM10, NO₂, CO, Ozone).

By harmonizing these datasets, we create a unified analytical platform to explore, model, and visualize the energy–pollution nexus.

---

## Table of Contents

- [Project Motivation](#project-motivation)
- [Data Sources](#data-sources)
- [Approach & Methodology](#approach--methodology)
  - [1. Data Acquisition & Cleaning](#1-data-acquisition--cleaning)
  - [2. Data Harmonization & Feature Engineering](#2-data-harmonization--feature-engineering)
  - [3. Baseline Modeling](#3-baseline-modeling)
  - [4. Advanced Modeling: Blending Ensemble](#4-advanced-modeling-blending-ensemble)
  - [5. Exploratory Data Analysis (EDA)](#5-exploratory-data-analysis-eda)
- [Key Insights](#key-insights)
- [How to Run](#how-to-run)
- [Team Members](#team-members)

---

## Project Motivation

The world faces a dual crisis:
- **Escalating Climate Crisis:** Driven by greenhouse gas emissions from fossil fuels, demanding a rapid shift to renewables.
- **Severe Public Health Crisis:** Air pollution, responsible for millions of premature deaths, is tightly linked to energy generation.

**Our objective:**  
1. **Exploratory Analysis:** Understand historical relationships (2000–2020) between energy patterns, renewables, economic indicators, and air quality.
2. **Predictive Modeling:** Build a machine learning model to forecast CO₂ emissions based on these interconnected factors.

---

## Data Sources

- [`datasets/global-data-on-sustainable-energy (1).csv`](datasets/global-data-on-sustainable-energy%20(1).csv): Main dataset, annual country-level energy and economic indicators.
- [`datasets/global air pollution dataset.csv`](datasets/global%20air%20pollution%20dataset.csv): Additional dataset, city-level air quality metrics.

---

## Approach & Methodology

### 1. Data Acquisition & Cleaning

- **Load and inspect** both datasets using `pandas`.
- **Clean problematic columns** (e.g., population density, missing values).
- **Remove rows** with missing target variable (CO₂ emissions).

### 2. Data Harmonization & Feature Engineering

- **Aggregate pollution data** to country-level statistical profiles (mean, median, min, max, std, var for each pollutant).
- **Merge datasets** on `Country`, attaching static pollution profiles to each annual energy record.
- **Standardize country names** and map to regions/continents using ISO-3166 codes.
- **Feature engineering** for time-series forecasting:
  - **Lag features:** Previous years' values.
  - **Rolling window features:** Moving averages and standard deviations.
  - **Difference features:** Year-over-year changes and percent changes.
  - **Regional aggregates:** Compute regional averages and country-vs-region differences.
  - **One-hot encoding** for categorical regional features.

### 3. Baseline Modeling

- **Train/test split** by year (2016–2019 as test set).
- **Model comparison** using time-series cross-validation (`TimeSeriesSplit`) and weighted metrics.
- **Models evaluated:** XGBoost, CatBoost, LightGBM.
- **Feature importance analysis** to interpret model drivers.

### 4. Advanced Modeling: Blending Ensemble

- **Holdout validation:** Split training data into train and blend sets.
- **Train base models** (XGBoost, CatBoost, LightGBM) on train set.
- **Generate meta-features** from base model predictions on blend and test sets.
- **Hill-climbing ensemble:** Iteratively combine base model predictions to minimize RMSE on blend set.
- **Final evaluation** on holdout test set and export predictions.

### 5. Exploratory Data Analysis (EDA)

- **Continental and regional statistics:** Electricity access, renewables, air quality, GDP, CO₂ emissions.
- **Country performance dashboard:** Energy and environmental scores, top/bottom performers.
- **Clustering:** Unsupervised grouping of countries into archetypes.
- **Temporal trends:** Global changes in energy access, renewables, emissions, and GDP.
- **Correlation analysis:** Relationships between energy, pollution, and economic indicators.
- **Air pollution patterns:** Distribution, pollutant-specific trends, and regional hotspots.

---

## Key Insights

- **Electricity from fossil fuels** is the strongest predictor of CO₂ emissions.
- **Renewable energy share** is highest in energy-poor, developing countries (often traditional biomass).
- **Air quality** is worst in fossil-fuel-dependent and industrializing regions.
- **Economic development** does not guarantee clean energy transition—many wealthy, oil-rich nations lag in renewables.
- **Modern renewables** (solar, wind, hydro) are needed to improve both access and air quality.
- **Policy implication:** Integrated strategies are required to balance energy access, economic growth, and environmental sustainability.

---

## How to Run

1. **Clone this repository** and ensure the datasets are in the `datasets/` folder.
2. **Install dependencies** (see the top of the notebook for required packages):
    ```sh
    pip install -r requirements.txt
    ```
    Or install directly in the notebook:
    ```python
    pip install country_converter pandas numpy seaborn plotly scikit-learn xgboost lightgbm catboost missingno
    ```
3. **Open and run** [`Energy_Pollution_Nexus.ipynb`](Energy_Pollution_Nexus.ipynb) in Jupyter or VS Code.
4. **Follow the notebook sections** for data exploration, modeling, and results.

---

## Team Members

| Name                              | GitHub Profile                                  |
|------------------------------------|-------------------------------------------------|
| Rahardi Salim                     | [@RahardiSalim](https://github.com/RahardiSalim) |
| Christian Yudistira Hermawan      | [@Nadekoooo](https://github.com/Nadekoooo)       |
| Vincent Davis Leonard Tjoeng      | [@Vincent-Davis](https://github.com/Vincent-Davis) |

---

## Repository Structure

```
Energy_Pollution_Nexus.ipynb   # Main notebook (analysis, modeling, EDA)
README.md                      # Project documentation
datasets/
    global air pollution dataset.csv
    global-data-on-sustainable-energy (1).csv
```

---

## License

This project is for academic and competition purposes. Please cite appropriately if you use or adapt any part of this work.
