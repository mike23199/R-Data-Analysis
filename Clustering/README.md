# Mall Customers Segmentation: Unsupervised Clustering Analysis in R

[![RPubs](https://img.shields.io/badge/RPubs-Interactive%20Report-blue?style=for-the-badge&logo=r)](https://rpubs.com/mike23199/mall_customers_clustering)

> **Live Interactive Report:** [RPubs - Mall Customers Clustering Analysis](https://rpubs.com/mike23199/mall_customers_clustering)

---

## Project Overview
This repository contains an end-to-end **Unsupervised Machine Learning** pipeline implemented in R to perform **Customer Segmentation**. By leveraging clustering techniques (K-Means & Hierarchical Clustering), the analysis categorizes mall visitors into distinct behavioral personas based on demographic data, annual earnings, and purchasing behavior.

The primary objective is to transform raw retail data into actionable business intelligence, allowing marketing teams to design tailored promotional strategies for each customer segment.

---

## Dataset Architecture

* **Dataset Source:** Kaggle Mall Customers Dataset (`Mall_Customers.csv`).
* **Observations:** 200 customer profiles.
* **Feature Attributes:**
  1. `CustomerID`: Unique visitor identifier *(dropped during modeling)*.
  2. `Gender`: Categorical (`Male` / `Female`).
  3. `Age`: Continuous numerical (years, range: 18 – 70).
  4. `Annual Income (k$)`: Continuous numerical (annual income in thousands of USD, range: \$15k – \$137k).
  5. `Spending Score (1-100)`: Behavioral index assigned by the mall based on customer purchasing history and engagement (range: 1 – 99).

---

## Analytical Workflow & Methodology

```text
Raw Data ➔ EDA & Distribution Plots ➔ Feature Scaling ➔ Optimal K Evaluation ➔ K-Means & Hierarchical Fit ➔ Cluster Profiling
```

---

1. Exploratory Data Analysis (EDA):
   * Summary statistics & missing value check (clean dataset with 0 null values).
   * Feature correlation analysis between Age, Annual Income, and Spending Score.
   * Gender distribution and comparative purchasing patterns.
2. Feature Preprocessing & Scaling:
   * Exclusion of non-informative ID columns (CustomerID).
   * Normalization/Standardization (scale()) of continuous attributes to prevent features with larger numeric scales (e.g., Annual Income) from dominating distance metric calculations (Euclidean distance).
3. Optimal Cluster Selection ($K$):
   * Elbow Method (Total WSS): Evaluating Within-Cluster Sum of Squares across $K \in [1, 10]$ to locate the bend ("elbow point").
   * Silhouette Analysis: Maximizing average silhouette width to measure cluster cohesion and separation quality (factoextra::fviz_nbclust).
4. Model Implementation:
   * K-Means Clustering: Partitioning observations into $K = 5$ optimal clusters using iterative centroid repositioning (set.seed() for reproducibility).
   * Hierarchical Agglomerative Clustering: Dendrogram construction using Euclidean distance and Ward's minimum variance method (hclust(method = "ward.D2")).

---

## Cluster Profiles & Behavioral Personas
The optimal $K=5$ segmentation reveals distinct consumer segments based on the Annual Income vs. Spending Score plane:
| Cluster # | Persona | Income Level | Spending Behavior | Strategic Marketing Action |
| :---: | :--- | :---: | :---: | :--- |
| **1** | **Target / High Rollers** | High | High | **VIP Engagement:** Exclusive product launches, loyalty reward points, personalized concierge services. |
| **2** | **Careful / High Earners** | High | Low | **Incentivized Campaigns:** Targeted discounts, premium membership promotions to boost spending. |
| **3** | **Careless / Big Spenders** | Low | High | **Trend-Driven Offers:** Flash sales, impulse-buy promotions, social media trend marketing. |
| **4** | **Sensible / Budget-Conscious** | Low | Low | **Value Promotions:** Essential discounts, bundle offers, price-sensitive deal alerts. |
| **5** | **Standard / Middle-of-the-Road** | Moderate | Moderate | **Cross-Selling:** General promotions, seasonal sales, broad marketing campaigns. |

---

## Required R Libraries
To execute the clustering script locally, install the required packages:
* "tidyverse",  # Data manipulation (dplyr) & visualization (ggplot2)
* "readr",      # Fast CSV ingestion
* "cluster",    # Core clustering algorithms (kmeans, pam)
* "factoextra", # Cluster visualization & optimal K diagnostics (fviz_cluster, fviz_nbclust)
* "gridExtra",  # Multi-panel plot layouts
* "rmarkdown",  # HTML dynamic report rendering
* "knitr"       # Report formatting
