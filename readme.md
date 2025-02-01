# XGBoost-Based Time Series Forecasting with Bootstrapped Confidence Intervals

## Overview
This script performs **time series forecasting** for revenue data using **XGBoost regression**, incorporating **rolling forecast validation**, **hyperparameter tuning**, and **bootstrapped confidence intervals**. It forecasts the next 12 months of revenue and visualizes the predictions with uncertainty bounds.

The key file for running this script is `main.ipynb`.

---

## **1. Load and Prepare Data**
- Reads an **Excel file** (`Connect_analyst_priklad.xlsx`)
- Converts the `ACCOUNTING_MONTH_KEY` column into a **datetime format**.
- Aggregates revenue at a **monthly level**.
- Creates **time-based features**:
  - `Year`
  - `Month`
  - `Year_squared` (to capture potential **quadratic trends** in revenue).

---

## **2. Define Features and Target**
- **X (Features):** `Year`, `Month`, `Year_squared`
- **y (Target):** `Revenue`

---

## **3. Rolling Forecast Split**
A **custom function (`rolling_forecast_split`)** is implemented to:
- Perform **expanding window validation**, where the model is trained on increasing historical data.
- Uses an **initial training window of 12 months**, expanding by 3 months at each step.

---

## **4. Hyperparameter Tuning for XGBoost**
- Uses `GridSearchCV` to find the **best parameters** for the `XGBRegressor` model.
- Parameters tuned:
  - `n_estimators`: `[300, 500]`
  - `learning_rate`: `[0.01, 0.05]`
  - `max_depth`: `[3, 5]`
- The best model is selected based on **Mean Absolute Error (MAE)**.

---

## **5. Model Evaluation**
- The **rolling forecast approach** is used to evaluate model performance.
- Computes multiple error metrics:
  - **Mean Absolute Error (MAE)**
  - **Root Mean Squared Error (RMSE)**
  - **Mean Absolute Percentage Error (MAPE)**
  - **Mean Percentage Error (MPE)**
  - **R-squared (R²)**

---

## **6. Forecasting the Next 12 Months**
- Generates **future dates** for the next 12 months.
- Uses the trained XGBoost model to **predict revenue** for future periods.

---

## **7. Bootstrapped Confidence Intervals**
- **Bootstrap sampling (1000 iterations)** is used to estimate the uncertainty of predictions.
- Generates **upper and lower bounds** (95% confidence intervals).

---

## **8. Visualization of Forecast**
- **Plots historical revenue** alongside **forecasted values**.
- Includes **confidence intervals** to quantify prediction uncertainty.

---

## **Final Output**
- A **DataFrame** displaying predicted revenue and confidence intervals.
- A **time series plot** comparing historical data with forecasted values.
---
