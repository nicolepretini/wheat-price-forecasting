# Wheat Price Forecasting (Time Series)

## Project Overview
This project focuses on forecasting **global monthly wheat prices** using
time-series data and proper temporal validation strategies.

The objective is not to build the most complex model possible, but to demonstrate
a **correct, interpretable, and realistic forecasting workflow** that can be
trusted in applied settings.

---

## Data
- Monthly global wheat prices (USD/ton)
- Time span: ~2000–2023
- Source: FAO-style aggregated global price series

The dataset is large enough to capture long-term trends, seasonality, and regime
changes, while remaining manageable for transparent modeling.

---

## Methodology

### 1. Exploratory Data Analysis (EDA)
We first inspected the raw time series to identify:
- Long-term upward trend
- Strong annual seasonality
- Increasing volatility in recent years

Rolling averages and monthly aggregation were used to separate trend and seasonal
components.

---

### 2. Train/Test Split (Time-Aware)
To avoid data leakage, the dataset was split chronologically:
- **Training set:** up to December 2018
- **Test set:** January 2019 onward

This simulates a real forecasting scenario where only past information is
available when making predictions.

---

### 3. Forecasting Models

Three models were evaluated, from simple to more expressive:

#### Naive Baseline
- Predicts the last observed value for all future periods
- Serves as a minimal benchmark

#### Seasonal Naive Baseline
- Predicts each month using the price from the same month one year earlier
- Captures recurring annual seasonality

#### Ridge Regression with Lag Features
- Linear regression with L2 regularization
- Uses lagged prices as predictors (1, 3, 6, and 12 months)
- Balances interpretability and predictive power

---

### 4. Evaluation Metrics
Models were evaluated on the test period using:
- **RMSE (Root Mean Squared Error)**
- **MAE (Mean Absolute Error)**

These metrics quantify both average error magnitude and sensitivity to large
forecasting mistakes.

---

## Results

| Model            | RMSE | MAE |
|------------------|------|-----|
| Ridge (lags)     | ~11  | ~8  |
| Seasonal Naive   | ~84  | ~64 |
| Naive            | ~211 | ~173 |

The Ridge model dramatically outperforms both baselines, indicating that wheat
prices are highly predictable from their recent history when proper temporal
structure is used.

---

## Key Takeaways
- Time-aware evaluation is critical in forecasting problems
- Strong baselines (naive and seasonal naive) are essential for honest comparison
- Simple, interpretable models can outperform heuristics by a large margin
- Lag-based features capture most of the predictive signal in this dataset

---

## Limitations
- The model relies exclusively on historical prices
- No exogenous drivers (weather, policy, supply shocks) are included
- Performance may degrade under structural breaks or extreme events

---

## Future Work
- Incorporate exogenous variables (climate, production, trade)
- Explore probabilistic forecasting and uncertainty estimation
- Evaluate robustness under rolling-origin validation

---

## Project Structure
.
├── data/
├── notebooks/
│ ├── 01_eda.ipynb
│ └── 02_forecasting.ipynb
├── outputs/
│ └── figures/
├── README.md
└── requirements.txt