# Decision Tree & CART Method Analysis in R

[![RPubs](https://img.shields.io/badge/RPubs-Interactive%20Report-green?style=for-the-badge&logo=r)](https://rpubs.com/mike23199/decision_tree)

> 📊 **Live Interactive Report:** [RPubs - Decision Tree & CART Method](https://rpubs.com/mike23199/decision_tree)

---

## Project Overview
This repository implements a **Supervised Machine Learning** pipeline in R focused on **Decision Trees** using the **CART (Classification and Regression Trees)** algorithm. 

The study demonstrates recursive binary splitting for decision making, evaluating how non-parametric decision boundaries segment observations based on feature rules, while addressing model complexity, tree pruning, and out-of-sample generalization.

---

## Methodology & CART Algorithm

```text
Raw Data ➔ EDA & Feature Encoding ➔ Train/Test Split ➔ Full Tree Growth ➔ Complexity Parameter (cp) Pruning ➔ Visual Tree Plot ➔ Model 
```

### Key Analytical Steps:
* **Splitting Criteria (Gini Impurity Index):** Used as the primary measure of node homogeneity during recursive binary splits:
  $$Gini = 1 - \sum_{i=1}^{k} p_i^2$$
* **Cost-Complexity Pruning ($cp$):** Growing an unconstrained decision tree leads to overfitting. Cross-validation is applied to inspect the relative error vs. size of tree trade-off, selecting the optimal Complexity Parameter ($cp$) to prune redundant branches without sacrificing predictive accuracy.
* **Tree Visualization & Interpretation:** Graphical rendering of decision nodes, splitting conditions, class proportions, and terminal leaf nodes using high-resolution tree plots (`rpart.plot`).

---

## Model Evaluation & Metrics

The decision tree model is evaluated on a holdout Test Dataset to measure classification accuracy and generalization capacity:

* **Confusion Matrix Analysis:** Assessing True Positives (TP), True Negatives (TN), False Positives (FP), and False Negatives (FN).
* **Performance Indicators:**
  * **Accuracy:** Overall proportion of correctly classified instances compared against baseline models.
  * **Sensitivity (Recall):** True Positive Rate across decision classes.
  * **Specificity:** True Negative Rate per decision leaf.
* **Variable Importance (VIP):** Quantifying the relative contribution of each feature based on the overall reduction of Gini impurity across all splits.

---

## Key Takeaways

* **High Interpretability:** Decision Trees generate clear, rule-based logic ($IF-THEN$ statements) that business stakeholders and non-technical decision-makers can easily digest.
* **Non-Parametric Flexibility:** No assumptions regarding feature normality, linearity, or homoscedasticity are required, allowing the algorithm to capture non-linear relationships effortlessly.
* **Pruning is Crucial:** Unpruned trees overfit noise in the training set. Applying optimal $cp$ pruning significantly improves out-of-sample accuracy on unseen test data.

---

## Required R Libraries

Install all necessary packages for Decision Tree estimation and visualization:

```R
install.packages(c(
  "tidyverse",   # Data manipulation (dplyr) & plotting (ggplot2)
  "readr",       # CSV file loading
  "caTools",     # Data partitioning (Train/Test split)
  "rpart",       # Core CART Decision Tree modeling engine
  "rpart.plot",  # High-quality decision tree visual plotting
  "caret",       # Model tuning, cross-validation & confusion matrix
  "rmarkdown",   # Dynamic HTML report knitting
  "knitr"        # Report formatting
))
