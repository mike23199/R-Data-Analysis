# Marketing A/B Testing & Causal Inference

[![RPubs](https://img.shields.io/badge/RPubs-Interactive%20Report-red?style=for-the-badge&logo=r)](https://rpubs.com/mike23199/marketing_AB)

> **Live Interactive Report:** [RPubs - A/B Testing & Causal Inference (marketing_AB)](https://rpubs.com/mike23199/marketing_AB)

---

## Project Overview
This repository implements a statistical **A/B Testing & Causal Inference** pipeline in R to evaluate the effectiveness of a digital marketing ad campaign. Using a large-scale experimental dataset of **588,101 users**, the analysis quantifies whether exposing potential customers to an advertisement (`ad`) yields a statistically significant lift in conversion rates compared to a holdout control group exposed to neutral Public Service Announcements (`psa`). 

The study applies two-proportion hypothesis testing, chi-square independence tests, and multivariable logistic regression modeling to isolate causal ad impact from confounding factors such as exposure frequency and timing.

---

## Dataset Architecture & Experimental Groups

* **Dataset Source:** Marketing A/B Testing Dataset (`marketing_AB.csv`).
* **Sample Size ($N$):** 588,101 unique user records.
* **Experimental Groups:**
  * **Treatment Group (`ad`):** ~564,577 users (exposed to marketing campaign ads).
  * **Control Group (`psa`):** ~23,524 users (exposed to neutral Public Service Announcements).
* **Feature Attributes:**
  * `user_id`: Unique passenger/visitor identifier.
  * `test_group`: Categorical assignment (`"ad"` vs `"psa"`).
  * `converted`: Binary target variable (`TRUE` / `1` = purchase completed, `FALSE` / `0` = no purchase).
  * `total_ads`: Continuous numerical (total number of advertisements seen by the user).
  * `most_ads_day`: Categorical (day of the week with peak ad exposure).
  * `most_ads_hour`: Discrete numerical ($0 - 23$, hour of day with peak ad exposure).

---

## Experimental Results & Hypothesis Testing

### 1. Baseline Conversion Rates & Relative Lift
* **Control Group (`psa`) Conversion:** **`1.78%`**
* **Treatment Group (`ad`) Conversion:** **`2.55%`**
* **Absolute Conversion Difference ($\Delta p$):** **`+0.77%`** (percentage points)
* **Relative Lift:** **`+43.2%`** increase in conversion rate for ad-exposed users compared to control:
  $$\text{Relative Lift} = \frac{2.55\% - 1.78\%}{1.78\%} \approx +43.2\%$$

### 2. Statistical Significance Testing (`prop.test` & $\chi^2$)
Two-proportion $Z$-test and Pearson's Chi-Square Test of Independence were conducted to evaluate the null hypothesis $H_0: p_{\text{ad}} = p_{\text{psa}}$:
* **Test Statistic:** $Z \approx 7.37$ ($\chi^2 \approx 54.3$)
* **$p$-value:** **$< 2.2 \times 10^{-16}$** (Highly statistically significant at $\alpha = 0.05$)
* **95% Confidence Interval for Difference:** $[0.0057, 0.0097]$
* **Conclusion:** $H_0$ is strongly rejected. The ad campaign produces a genuine, statistically significant causal improvement in sales conversion.

---

## Multivariable Logistic Regression & Odds Ratios

To control for potential confounding variables (`total_ads`, `most_ads_day`, `most_ads_hour`), a Generalized Linear Model (GLM - Binomial) was estimated:

$$\ln\left(\frac{P(\text{converted}=1)}{1 - P(\text{converted}=1)}\right) = \beta_0 + \beta_1(\text{group}_{\text{ad}}) + \beta_2(\text{total\_ads}) + \beta_3(\text{most\_ads\_day}) + \beta_4(\text{most\_ads\_hour})$$

| Predictor | Coefficient ($\beta$) | Odds Ratio ($e^\beta$) | $p$-value | Interpretation |
| :--- | :---: | :---: | :---: | :--- |
| **`group_ad`** | $+0.368$ | **`1.445`** | **`< 0.001`** | Seeing the ad increases purchase odds by **~44.5%** holding exposure volume and timing constant. |
| **`total_ads`** | $+0.009$ | **`1.009`** | **`< 0.001`** | Higher ad frequency significantly boosts conversion propensity (with diminishing marginal returns). |
| **`most_ads_day`** | *Varies* | *Varies* | **`< 0.01`** | Mondays and Tuesdays exhibit peak conversion sensitivity compared to weekend baselines. |
| **`most_ads_hour`** | *Varies* | *Varies* | **`< 0.001`** | Mid-day hours ($10:00 - 15:00$) show optimal conversion responsiveness. |

---

## Key Business Takeaways
1. **Proven Campaign Efficacy:** The digital ad campaign achieves a statistically verified **+43.2% relative lift** in conversion, proving that marketing exposure directly drives purchasing behavior.
2. **Optimal Ad Frequency:** While increased ad volume (`total_ads`) correlates with higher purchase probability, frequency caps should be established to optimize ad spend and avoid ad fatigue.
3. **Strategic Schedule Optimization:** Reallocating ad budgets toward peak engagement days (Monday/Tuesday) and peak operating hours ($10:00 - 15:00$) maximizes campaign ROI.

---

## Required R Libraries

```r
install.packages(c(
  "tidyverse",  # Data manipulation (dplyr) & plotting (ggplot2)
  "readr",      # Fast CSV file loading
  "janitor",    # Clean column naming & frequency tables
  "broom",      # Tidy statistical test outputs & regression summaries
  "car",        # Variance Inflation Factor diagnostics
  "pROC",       # ROC curve and AUC evaluation
  "rmarkdown",  # Dynamic report rendering
  "knitr"       # Document formatting
))
