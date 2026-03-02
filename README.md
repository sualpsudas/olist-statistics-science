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

![Boxplot](images/01_boxplot_violin.png)

### Normality Check

![Normality](images/01_normality.png)
![Q-Q Plot](images/01_qqplot.png)

**Key insights:**
- **Mean vs median** — The most common order costs ~R$50 (mode), but the average is R$154. Reporting only the mean overstates typical spend by ~43%. On skewed data, median is the honest answer.
- **Spread** — A CV of ~100% means the spread is as wide as the mean itself. The middle 50% of orders falls between R$43–R$162, so "average order value" hides an enormous range of customer behaviour.
- **Distributions** — Three very different shapes: order value is right-skewed (big purchases pull the tail), review score is left-skewed (most customers give 5 stars or nothing), delivery days is roughly bell-shaped. Each shape calls for a different statistical approach.
- **Outliers** — ~7% of orders sit above the IQR fence. The violin plot reveals SP and RJ have wider value distributions than smaller states — more product variety. The boxplot alone would miss this.
- **Normality** — None of the three key variables pass the Shapiro-Wilk test. Use log-transformed payment values in models, prefer non-parametric tests for review scores, and note that large n (≥30 per group) partially rescues you via the Central Limit Theorem.

---

## Part 2 — Intermediate Statistics

### How hypothesis testing works

![Hypothesis concept](images/02_hypothesis_concept.png)

### t-Test: Weekend vs Weekday Orders

![t-test](images/02_ttest.png)

### Chi-Square: Payment Method × Delivery

![Chi-square](images/02_chisquare.png)

### Correlation

![Correlation heatmap](images/02_correlation_heatmap.png)
![Scatter plots](images/02_scatter_correlation.png)

### Simple Linear Regression

![Regression](images/02_regression.png)

**Key insights:**
- **p-value** — It's not the probability that H₀ is true. It's the probability of seeing data this extreme *if* H₀ were true. A small p-value means the result would be very unlikely by chance alone.
- **t-test** — Weekend orders are statistically different from weekday orders, but Cohen's d is small — the practical difference is only ~R$5. Statistical significance ≠ business significance. Always check effect size alongside the p-value.
- **Chi-square** — Boleto (Brazil's bank slip) has the lowest delivery rate. Boleto payments can expire before fulfilment — a known friction point in Brazilian e-commerce. Cramer's V is weak, but the pattern is real.
- **Correlation** — The delivery–rating correlation (r ≈ −0.25) is significant but not huge. Delivery speed is *one* factor in satisfaction, not the whole story. Product quality and price perception likely matter more — but they're not in this dataset.
- **Regression** — R² = 0.04 means delivery time alone explains only 4% of score variance. Statistically significant but practically weak. Classic signal to add more features — which is exactly what Part 3 does.

---

## Part 3 — Advanced Statistics

### One-Way ANOVA

![ANOVA](images/03_anova.png)

### Multiple Regression

![Multiple regression](images/03_multiple_regression.png)

### Bootstrap Confidence Intervals

![Bootstrap](images/03_bootstrap.png)

### A/B Test: On-time vs Late Delivery

![A/B test](images/03_ab_test.png)

### Confidence Intervals by State

![Confidence intervals](images/03_confidence_intervals.png)

### Kruskal-Wallis: Scores by Month

![Kruskal-Wallis](images/03_kruskal_month.png)

**Key insights:**
- **ANOVA** — Credit card orders average ~R$164, nearly double voucher orders (~R$66). This isn't just payment preference: credit cards unlock installment payments (parcelamento) in Brazil, enabling larger purchases. ANOVA tells us *some* group differs — Tukey HSD tells us *which ones*.
- **Multiple regression** — Even with 7 features, R² ≈ 0.11 — roughly 89% of score variance is unexplained by logistics alone. Product quality, price perception, and customer expectations are the likely real drivers, but they're not in this dataset.
- **Bootstrap** — With n > 90k orders the 95% CI for the mean is ±~R$1. The law of large numbers at work: large samples give very precise estimates. The bootstrap and the formula-based CI agree closely.
- **A/B test** — On-time delivery is significant (p < 0.001) but Cohen's d ≈ 0.3 — medium-small effect. To detect a small effect (d=0.2) with 80% power you need ~400 orders per group. Every day of delay chips away at customer trust, even if the individual effect is modest.
- **Confidence intervals** — States with wide CIs (AP, RO, AC) have fewer orders — less data means more uncertainty. Don't make geographic decisions on point estimates alone. States whose CI sits entirely above the national mean are genuinely high-satisfaction markets.
- **Kruskal-Wallis** — Review scores dip in peak demand months (Black Friday, Christmas) when logistics get strained. This isn't random noise — confirmed by the test. Natural follow-up: check whether delivery delays spike in the same months.

---

## Setup

```bash
git clone https://github.com/sualpsudas/olist-statistics-science.git
cd olist-statistics-science
pip install -r requirements.txt
jupyter notebook
```

Data: [Olist Brazilian E-Commerce — Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
