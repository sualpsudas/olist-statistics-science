# Statistics Science with Real E-Commerce Data

Using 100k+ orders from **Olist** (Brazil's largest e-commerce platform) to explore statistics from the ground up — basic, intermediate, and advanced.

[![Python](https://img.shields.io/badge/Python-3.11-blue.svg)](https://python.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org)

---

## What's inside

| Notebook | Topics |
|---|---|
| [01 Basic](notebooks/01_basic_statistics.ipynb) | Descriptive stats, mean/median/mode, spread, histograms, boxplots, normality |
| [02 Intermediate](notebooks/02_intermediate_statistics.ipynb) | Hypothesis testing, t-test, chi-square, correlation, simple regression |
| [03 Advanced](notebooks/03_advanced_statistics.ipynb) | ANOVA, multiple regression, bootstrap, A/B testing, power analysis |

---

## Part 1 — Basic Statistics

### Mean vs Median vs Mode
On right-skewed data (like order values), mean gets pulled toward the tail. Median is the honest "typical" value.

![Central tendency](images/01_central_tendency.png)

### Spread — Std Dev & Percentiles

![Dispersion](images/01_dispersion.png)

### Frequency Distributions

![Histograms](images/01_histograms.png)

### Boxplots & Outliers
~7% of orders sit above the IQR fence.

![Boxplot](images/01_boxplot_violin.png)

### Normality Check
Raw order values are not normal. Log transform brings them close.

![Normality](images/01_normality.png)
![Q-Q Plot](images/01_qqplot.png)

---

## Part 2 — Intermediate Statistics

### How hypothesis testing works
p-value < 0.05 → reject H₀ → the difference is real.

![Hypothesis concept](images/02_hypothesis_concept.png)

### t-Test: Weekend vs Weekday Orders

![t-test](images/02_ttest.png)

### Chi-Square: Payment Method × Delivery

![Chi-square](images/02_chisquare.png)

### Correlation
Longer delivery → lower ratings. Both Pearson and Spearman agree.

![Correlation heatmap](images/02_correlation_heatmap.png)
![Scatter plots](images/02_scatter_correlation.png)

### Simple Linear Regression

![Regression](images/02_regression.png)

---

## Part 3 — Advanced Statistics

### One-Way ANOVA
Credit card orders are significantly higher in value than other payment methods.

![ANOVA](images/03_anova.png)

### Multiple Regression
`is_late` is the strongest negative predictor of review score.

![Multiple regression](images/03_multiple_regression.png)

### Bootstrap Confidence Intervals
10,000 resamples — no distribution assumption needed.

![Bootstrap](images/03_bootstrap.png)

### A/B Test: On-time vs Late Delivery
On-time delivery significantly boosts customer ratings (small but real effect).

![A/B test](images/03_ab_test.png)

### Confidence Intervals by State

![Confidence intervals](images/03_confidence_intervals.png)

### Kruskal-Wallis: Scores by Month

![Kruskal-Wallis](images/03_kruskal_month.png)

---

## Setup

```bash
git clone https://github.com/sualpsudas/olist-statistics-science.git
cd olist-statistics-science
pip install -r requirements.txt
jupyter notebook
```

Data: [Olist Brazilian E-Commerce — Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
