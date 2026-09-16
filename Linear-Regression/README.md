# Data Analysis Project: Linear & Logistic Regression in R

<div align="center">

[![View on RPubs](https://img.shields.io/badge/RPubs-View%20Report-blue?style=for-the-badge&logo=R)](https://rpubs.com/mike23199/1415782)

</div>

## Overview
This repository contains a comprehensive statistical data analysis implemented in **R**. The project demonstrates the end-to-end workflow of building, diagnosing, and interpreting both **Linear Regression** and **Logistic Regression** models. 

**Live Preview:** You can view the fully rendered HTML report with all outputs, plots, and interpretations directly on [RPubs - Data Analysis Report](https://rpubs.com/mike23199/1415782).

---

## Key Features & Workflow

The analysis follows a rigorous data science pipeline:
1. **Data Preprocessing & Exploratory Data Analysis (EDA):** 
   - Handling missing values and data cleaning.
   - Summary statistics and distribution visualizations.
   - Correlation analysis to check for multicollinearity.
2. **Linear Regression Modeling:**
   - Fitting models to predict continuous outcomes.
   - Evaluating model assumptions (linearity, homoscedasticity, normality of residuals).
   - Interpreting coefficients, $R^2$, and p-values.
3. **Logistic Regression Modeling:**
   - Fitting models for binary classification tasks.
   - Calculating Odds Ratios (OR) and interpreting log-odds.
   - Model evaluation using Confusion Matrices, Accuracy, and ROC-AUC curves.

---

## Tech Stack & Libraries
The analysis was conducted using **R** and leverages the following core packages:
* **Data Manipulation & Wrangling:** `tidyverse` (dplyr, ggplot2, tidyr)
* **Modeling & Statistics:** `stats` (base R for glm/lm)
* **Model Evaluation & Diagnostics:** `caret`, `pROC` *(adjust according to your libraries)*

---

## Summary of Results
* Model Fit: The final model demonstrates strong predictive capability with statistically significant predictors ($p < 0.05$).
* Diagnostics: Post-estimation diagnostic checks confirmed valid residual behavior without severe multicollinearity or heteroscedasticity violations.
