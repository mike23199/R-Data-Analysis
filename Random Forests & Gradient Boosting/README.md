# Random Forests & Gradient Boosting: Ensemble Machine Learning in R

[![RPubs](https://img.shields.io/badge/RPubs-Interactive%20Report-purple?style=for-the-badge&logo=r)](https://rpubs.com/mike23199/random_forest)

> **Live Interactive Report:** [RPubs - Random Forests & Gradient Boosting Analysis](https://rpubs.com/mike23199/random_forest)

---

## Project Overview
This repository implements an advanced **Ensemble Machine Learning** pipeline in R, evaluating and comparing two state-of-the-art tree-based ensemble paradigms: **Random Forests (Bagging)** and **Gradient Boosting Machines (Boosting)**. 

The primary objective is to demonstrate how aggregating multiple decision trees optimizes predictive performance, reduces variance, controls overfitting, and surfaces critical variable importance metrics compared to individual Decision Trees.

---

## ⚙️ Algorithmic Framework & Methodology

```text
Data Preprocessing ➔ Train/Test Partitioning ➔ Random Forest Fitting (OOB Error) ➔ Gradient Boosting Tuning ➔ Comparative VIP Analysis
```

### 1. Random Forest (Bagging Engine)
* **Mechanism:** Constructs a parallel ensemble of decorrelated decision trees via Bootstrap Aggregation (Bagging) combined with feature sub-selection at each split.
* **Out-of-Bag (OOB) Validation:** Leverages OOB observations (~37% left-out data per bootstrap sample) for unbiased internal cross-validation and generalization error estimation.
* **Key Hyperparameters:**
  * `ntree`: Total number of decision trees in the forest (e.g., 500).
  * `mtry`: Number of features randomly sampled as candidates at each split ($\approx \sqrt{p}$).

### 2. Gradient Boosting Machine (Boosting Engine)
* **Mechanism:** Sequential ensemble approach where each consecutive decision tree is trained on the residual errors (pseudo-residuals) of previous models, minimizing loss via Gradient Descent.
* **Key Hyperparameters:**
  * `n.trees` / `nrounds`: Number of boosting iterations.
  * `interaction.depth`: Maximum depth of individual decision trees.
  * `shrinkage` ($\eta$): Learning rate scaling parameter controlling individual tree contributions.

---

## Model Evaluation & Comparative Performance

The ensemble models were trained on partitioned data and evaluated across standard classification/regression diagnostic metrics:

| Diagnostic Feature | Single Decision Tree (CART) | Random Forest (Bagging) | Gradient Boosting (GBM) |
| :--- | :--- | :--- | :--- |
| **Learner Type** | Base Weak Learner | Parallel Ensemble | Sequential Ensemble |
| **Variance & Overfitting** | High Variance | Low Variance (Averaging effect) | Low Variance & Low Bias |
| **Out-of-Sample Accuracy** | Baseline (~80%) | High (~85% – 90%) | Superior (~88% – 92%) |
| **Feature Importance (VIP)** | Gini Impurity Split | Mean Decrease Gini / Accuracy | Relative Influence (%) |
| **Model Explainability** | Direct Tree Rules | Variable Importance Plots | Partial Dependence Plots (PDP) |

---

## Key Takeaways

* **Ensemble Superiority:** Both Random Forests and Gradient Boosting significantly outperform individual CART Decision Trees by mitigating individual tree variance and capturing complex non-linear feature interactions.
* **Variable Importance (VIP):** Feature importance metrics provide clear ranking of the key predictive drivers, offering model explainability for stakeholder decisions.
* **Hyperparameter Sensitivity:**
  * **Random Forest:** Highly robust out-of-the-box with low risk of overfitting as `ntree` increases.
  * **Gradient Boosting:** Achieves higher accuracy ceilings but requires careful hyperparameter tuning (`shrinkage` and `interaction.depth`) to avoid overfitting noisy data.

---

## Required R Libraries

To execute the code and reproduce the analysis locally, install the required packages:

```R
install.packages(c(
  "tidyverse",    # Data transformation (dplyr) & plotting (ggplot2)
  "readr",        # Fast CSV ingestion
  "caTools",      # Train/Test data splitting
  "randomForest", # Core Random Forest implementation
  "gbm",          # Generalized Boosted Regression Models
  "caret",        # Model training & hyperparameter grid search
  "pROC",         # ROC curves & AUC evaluation metrics
  "vip",          # Variable Importance Visualization
  "rmarkdown",    # Dynamic HTML report rendering
  "knitr"         # Document formatting
))
