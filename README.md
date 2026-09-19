# Time Series Analysis & Forecasting: Johnson & Johnson Quarterly Earnings 

[![RPubs](https://img.shields.io/badge/RPubs-Interactive%20Report-orange?style=for-the-badge&logo=r)](https://rpubs.com/mike23199/JohnsonJohnson)

> **Live Interactive Report:** [RPubs - Johnson & Johnson Time Series Forecasting](https://rpubs.com/mike23199/JohnsonJohnson)

---

## Project Overview
This repository contains a comprehensive **Time Series Analysis and Econometric Forecasting** pipeline implemented in R using the classic `JohnsonJohnson` dataset. The analysis models the historical quarterly earnings per share (EPS) of Johnson & Johnson stock from 1960 to 1980.

The project demonstrates variance stabilization, classical decomposition, stationarity testing, Holt-Winters exponential smoothing, and Box-Jenkins **Seasonal ARIMA (SARIMA)** modeling to capture long-term exponential growth trends and multiplicative quarterly seasonality.

---

## Dataset Overview

* **Dataset Source:** Built-in R time series object (`datasets::JohnsonJohnson` / `astsa`).
* **Time Span:** 84 quarterly observations spanning 21 years (1960 Q1 – 1980 Q4).
* **Target Variable:** Quarterly Earnings per Share (EPS) in USD.
* **Frequency:** $s = 4$ (Quarterly reporting cycle).
* **Key Visual Characteristics:**
  * Strong upward multiplicative trend (earnings increase exponentially over time).
  * Distinct quarterly seasonal pattern with expanding amplitude as mean EPS grows.

---

## Analytical & Modeling Pipeline

```text
Raw TS Plot ➔ Log Transformation ➔ Seasonal Decomposition ➔ Stationarity Tests (ADF/ACF/PACF) ➔ Holt-Winters & SARIMA Fitting ➔ Residual Diagnostics ➔ Multi-Period Forecast
```

### 1. Data Transformation & Stationarity
* **Variance Stabilization:** Applied natural logarithmic transformation ($\ln(Y_t)$) to linearize the exponential trend and convert multiplicative seasonality into additive seasonality.
* **Differencing for Stationarity:**
  * Non-seasonal differencing ($d = 1$) to eliminate overall trend.
  * Seasonal differencing ($D = 1, s = 4$) to remove annual seasonal cycles.
* **Autocorrelation Analysis:** Evaluated Autocorrelation Function (ACF) and Partial Autocorrelation Function (PACF) plots to identify candidate SARIMA orders $(p, d, q) \times (P, D, Q)_4$.

### 2. Time Series Models Evaluated
* **Classical / STL Decomposition:** Separating the series into Trend, Seasonal, and Remainder (Residual) components.
* **Holt-Winters Multiplicative/Additive Exponential Smoothing:** Modeling level, trend, and seasonal components dynamically.
* **Seasonal ARIMA (SARIMA):** Optimal model selection via `auto.arima()` and information criteria (AIC/BIC) minimization.

---

## Model Diagnostics & Forecasting Performance

* **Residual Analysis:** Inspected residual ACF plots and conducted Ljung-Box test diagnostics to confirm that model residuals behave as white noise (no remaining autocorrelation).
* **Out-of-Sample Forecasting:** Generated multi-step ahead point forecasts with 80% and 95% confidence intervals for future quarterly earnings.

| Model Approach | Strengths | Diagnostic Check | Primary Use Case |
| :--- | :--- | :--- | :--- |
| **Log-Linear Trend + Seasonal** | Simple baseline, intuitive trend interpretation | Residual autocorrelation present | Baseline comparison |
| **Holt-Winters Exponential Smoothing** | Adapts dynamically to changing trend/seasonal patterns | Good fit on non-stationary data | Short-term tactical forecasting |
| **SARIMA $(p,d,q) \times (P,D,Q)_4$** | Rigorous statistical framework, accounts for residual autocorrelation | ✅ White noise residuals (Ljung-Box $p > 0.05$) | Optimal long-term econometric forecasting |

---

## Key Takeaways

* **Multiplicative Behavior:** Raw earnings exhibit growing variance alongside the mean level, making log-transformation an essential prerequisite prior to linear modeling or differencing.
* **Seasonal Dominance:** Quarterly financial reporting creates strong, predictable seasonal peaks (typically higher earnings in Q1/Q2) that require explicit seasonal parameters ($s=4$).
* **Robust Forecasting:** SARIMA modeling effectively isolates trend and seasonality, producing narrow confidence bounds and reliable financial projections.

---

## Required R Libraries

To execute the code and reproduce the analysis locally, install the required packages:

```R
install.packages(c(
  "tidyverse", # Data manipulation & ggplot2 visualization
  "forecast",  # Core time series forecasting tools (auto.arima, forecast, HoltWinters)
  "tseries",   # Stationarity testing (adf.test, kpss.test)
  "astsa",     # Applied statistical time series datasets & utilities
  "rmarkdown", # Dynamic HTML report generation
  "knitr"      # Document formatting
))
