# Titanic Survival Prediction: Binary Logistic Regression in R

[![RPubs](https://img.shields.io/badge/RPubs-Interactive%20Report-red?style=for-the-badge&logo=r)](https://rpubs.com/mike23199/Titanic_logistic_regression)

 **Live Interactive Report:** [RPubs - Titanic Logistic Regression Analysis](https://rpubs.com/mike23199/Titanic_logistic_regression)

---

## Project Overview
This repository contains a binary classification analysis using **Logistic Regression (Generalized Linear Model - GLM)** in R to predict passenger survival on the Titanic. The study evaluates demographic features and travel information to quantify survival odds and assess classification performance using evaluation metrics (Confusion Matrix, ROC Curve, AUC).

---

## Dataset & Preprocessing

* **Dataset Size:** 891 passenger records and 12 variables (`PassengerId`, `Survived`, `Pclass`, `Name`, `Sex`, `Age`, `SibSp`, `Parch`, `Ticket`, `Fare`, `Cabin`, `Embarked`).
* **Factor Conversion:** Categorical predictors (`Survived`, `Pclass`, `Sex`, `Embarked`) were encoded as factor variables prior to modeling.
* **Train / Test Split:** Data was partitioned into **65% Training set** ($N = 579$) and **35% Test set** ($N = 312$) using `caTools::sample.split` with `set.seed(999)`.

---

## Model Estimation & Statistical Significance

A logit model was fitted using maximum likelihood estimation (`family = "binomial"`):

$$\text{logit}(P(\text{Survived}=1)) = \beta_0 + \beta_1(\text{Pclass}) + \beta_2(\text{Sex}) + \beta_3(\text{Age}) + \beta_4(\text{SibSp}) + \beta_5(\text{Parch}) + \beta_6(\text{Fare}) + \beta_7(\text{Embarked})$$

*Note: 117 observations were automatically excluded from initial training due to missing values (`NA`s) in `Age`.*

### Predictor Significance Summary:
* **`Sexmale` ($\beta = -2.3845, p < 2 \times 10^{-16}$):** Most dominant predictor. Male passengers had significantly lower log-odds of survival.
* **`Pclass2` ($\beta = -1.4361, p = 0.00091$) & `Pclass3` ($\beta = -2.5102, p = 2.61 \times 10^{-8}$):** Strong negative association with survival compared to 1st class.
* **`Age` ($\beta = -0.0525, p = 4.85 \times 10^{-7}$):** Statistically significant negative impact (older passengers had reduced survival probabilities).
* **`SibSp` ($\beta = -0.3699, p = 0.0195$):** Moderate statistical significance ($p < 0.05$).
* **Non-Significant Variables:** `Parch` ($p = 0.482$), `Fare` ($p = 0.552$), and `Embarked` ($p > 0.36$) showed no statistically significant independent effect when controlling for the other predictors.

---

## Model Evaluation & Confusion Matrix

Predictions were generated on the holdout Test Set using a classification threshold probability of **$0.50$** (evaluating $N = 250$ complete test cases):

```text
               Predicted FALSE   Predicted TRUE
Actual FALSE         126 (TN)          22 (FP)
Actual TRUE           22 (FN)          80 (TP)
```

---

## Model Accuracy
* 82.4% ($\frac{126 + 80}{250}$) vs. 61.5% Baseline Accuracy (predicting the majority class: non-survival).
* Sensitivity (True Positive Rate): 78.4% ($\frac{80}{80 + 22}$) — Ability to correctly identify actual survivors.
* Specificity (True Negative Rate): 85.1% ($\frac{126}{126 + 22}$) — Ability to correctly identify non-survivors.
* Error Symmetry: Equal number of false positives ($22$) and false negatives ($22$), indicating a balanced decision boundary at $p = 0.5$.

---

## ROC Curve & AUC Analysis
To plot the Receiver Operating Characteristic (ROC) curve via the ROCR package, missing cases were filtered (na.omit), leaving $N = 108$ training observations (Train2) and $N = 75$ testing observations (Test2).
* Area Under the Curve (AUC): 0.7099 (~71% discriminative capability).
* Sample Size Trade-off: While complete-case analysis was necessary for generating the ROC performance object, reducing the training size to 108 records limited statistical power, resulting in a slightly lower AUC compared to the main model.

---

## Key Takeaways
* Substantial Lift Over Baseline: The model achieved 82.4% accuracy, outperforming the baseline rule (61.5%) by +20.9%, confirming that socio-demographic features hold strong predictive capability.
* Historical Validation: Statistical coefficients strongly corroborate the historical "women and children first" protocol and socio-economic priority during evacuation.
* Missing Data Impact: Deleting observations with missing age values significantly reduces training size and predictive resolution, highlighting the importance of imputation strategies in future iterations.
