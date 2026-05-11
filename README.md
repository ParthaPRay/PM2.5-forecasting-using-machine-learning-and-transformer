# PM2.5 Forecasting for Delhi Air Quality Using Machine Learning, ARIMA-Type Models, and Time-Series Foundation Models

## Overview

This repository presents a PM2.5 forecasting workflow for Delhi air quality using historical air pollution data. The study uses basic machine learning models, classical statistical time-series models, and transfer/foundation time-series models to forecast `pm2_5` values from multivariate air quality indicators.

The dataset used in this work is:

> Nitiraj, K., & Jagadish, T. (2026). *Dataset: Air Quality Dataset for Delhi (2022-08-01 to 2026-02-18)* [Data set]. Zenodo. [https://doi.org/10.5281/zenodo.18673773](https://zenodo.org/records/18673773)

The Zenodo record describes the dataset as historical air quality time-series data for Delhi, covering 2022-08-01 to 2026-02-18, retrieved from the Open-Meteo Air Quality service using the `cams_global` domain. The record was published on February 17, 2026, under a CC0 license.

## Dataset

The dataset file used in this repository is:

```text
air_quality_historical.csv.csv
````

The original dataset contains daily air-quality-related variables for Delhi. For this forecasting experiment, the following date range was selected:

```text
04-08-2022 to 18-02-2026
```

The selected target variable is:

```text
pm2_5
```

The available columns considered in the workflow are:

```text
date
pm10
pm2_5
carbon_monoxide
nitrogen_dioxide
sulphur_dioxide
ozone
aerosol_optical_depth
dust
uv_index
```

## Objective

The main objective of this repository is to build a reproducible PM2.5 forecasting pipeline for Delhi using:

1. basic regression-based machine learning models,
2. ensemble machine learning models,
3. persistence baseline forecasting,
4. ARIMA-type and related statistical time-series models,
5. transfer or foundation time-series forecasting models.

The focus is on methodology, model implementation, and comparative forecasting workflow. This README does not report experimental results.

## Forecasting Target

The forecasting task is defined as:

```text
Predict future PM2.5 concentration values using historical PM2.5 observations and related air quality variables.
```

The primary target column is:

```text
pm2_5
```

The remaining air quality variables may be used as exogenous predictors, lagged variables, rolling-window statistics, or auxiliary features depending on the model family.

## Methodology

### 1. Data Loading

The dataset is loaded from:

```text
air_quality_historical.csv.csv
```

The `date` column is parsed as a datetime column and used as the temporal index for time-series modelling.

### 2. Date Range Selection

Only observations within the following range are selected:

```text
04-08-2022 to 18-02-2026
```

This filtered subset is used for all PM2.5 forecasting experiments.

### 3. Data Preprocessing

The preprocessing workflow includes:

* parsing the `date` column,
* sorting records chronologically,
* checking missing values,
* handling missing or invalid numerical entries,
* selecting the PM2.5 target variable,
* preparing pollutant and atmospheric variables as candidate predictors,
* generating lag-based and rolling-window features where required.


### 4. Train-Test Splitting

Since this is a time-series forecasting problem, the dataset is split chronologically rather than randomly.

A typical split strategy is:

```text
Training set: earlier observations
Testing set: later observations
```

This prevents data leakage and preserves the temporal structure of the forecasting problem.

## Model Families

### A. Baseline Model

The baseline model provides a simple reference point for comparison.

```text
Persistence Baseline
```

In persistence forecasting, the most recent observed PM2.5 value is used as the forecast for the next time step.

### B. Basic Machine Learning Models

The following regression-based models are used:

```text
Linear Regression
ElasticNet Regression
Ridge Regression
```

These models provide interpretable and computationally efficient baselines for PM2.5 forecasting.

### C. Ensemble Machine Learning Models

The following ensemble models are included:

```text
Extra Trees
Random Forest
XGBoost
LightGBM
HistGradientBoosting
```

These models are suitable for capturing nonlinear relationships between PM2.5 and other air quality variables such as PM10, carbon monoxide, nitrogen dioxide, sulphur dioxide, ozone, aerosol optical depth, dust, and UV index.

### D. ARIMA-Type and Statistical Time-Series Models

The following classical and statistical time-series models are used:

```text
SARIMAX(1,0,1) with Exogenous Variables
SARIMA(1,1,1)(1,0,1,7)
AutoRegressive AR(14)
ARIMA(2,1,2)
Unobserved Components Model
Exponential Smoothing Additive
```

These models are designed to capture trend, autoregressive behavior, moving-average structure, seasonality, and temporal dependence in PM2.5 data.

The SARIMAX model also allows the inclusion of exogenous variables such as:

```text
pm10
carbon_monoxide
nitrogen_dioxide
sulphur_dioxide
ozone
aerosol_optical_depth
dust
uv_index
```

### E. Time-Series Transformer and Foundation Models

The workflow also includes modern transfer/foundation time-series forecasting models:

```text
Chronos-2
TimesFM 2.5
```

These models are used to explore the potential of pretrained time-series foundation models for PM2.5 forecasting.

Chronos-2 and TimesFM 2.5 are considered transfer time-series models because they are pretrained on large-scale time-series corpora and can be adapted or directly applied to new forecasting tasks.

## General Workflow

The overall workflow is:

```text
Dataset Loading
        ↓
Date Parsing and Filtering
        ↓
Missing Value Handling
        ↓
Feature Engineering
        ↓
Train-Test Split
        ↓
Model Training
        ↓
Forecast Generation
        ↓
Evaluation
        ↓
Model Comparison
```


## Evaluation Metrics

The forecasting models may be evaluated using standard regression and forecasting metrics such as:

```text
MAE
MSE
RMSE
MAPE
R² Score
```

These metrics help compare the accuracy and error behavior of different model families.

## Reproducibility Notes

To ensure reproducibility:

* keep the original dataset file unchanged,
* document all preprocessing steps,
* avoid random train-test splitting,
* use chronological splitting for forecasting,
* fix random seeds for machine learning models,
* clearly report model configurations,
* save generated forecasts and evaluation tables separately.

## Dataset Citation

Please cite the original dataset as:

```text
Nitiraj, K., & Jagadish, T. (2026). Dataset: Air Quality Dataset for Delhi 
(2022-08-01 to 2026-02-18) [Data set]. Zenodo. 
https://doi.org/10.5281/zenodo.18673773
```

## Acknowledgement

This repository uses the Delhi air quality dataset published on Zenodo by Nitiraj and Jagadish. The dataset supports air quality trend analysis and forecasting research for Delhi using daily pollutant and atmospheric variables.

## License

The original dataset is available under the Creative Commons Zero v1.0 Universal license, as stated in the Zenodo record. Users should follow the licensing terms of the dataset and the licenses of all software libraries used in this repository.


