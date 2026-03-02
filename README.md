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

> The most common order on Olist costs around R$50 (mode), but the *average* ticket is R$154 because of large bulk or electronics orders. Reporting only the mean would overstate what a typical customer spends by ~43%.

### Spread — Std Dev & Percentiles

![Dispersion](images/01_dispersion.png)

> A CV of ~100% means the spread is as large as the mean itself — payment values are extremely heterogeneous. The middle 50% of orders (IQR) falls between ~R$43 and R$162, so "average order value" hides a very wide range of customer behaviour.

### Frequency Distributions

![Histograms](images/01_histograms.png)

> Three very different shapes in one dataset: order value is right-skewed (long tail of big purchases), review score is left-skewed (customers are overwhelmingly happy or silent), delivery days is roughly bell-shaped with outliers past 30 days. Each shape calls for a different statistical approach.

### Boxplots & Outliers
~7% of orders sit above the IQR fence.

![Boxplot](images/01_boxplot_violin.png)

> The violin plot reveals that SP and RJ have wider distributions than smaller states — more price diversity, likely more product variety. The boxplot alone would miss this.

### Normality Check
Raw order values are not normal. Log transform brings them close.

![Normality](images/01_normality.png)
![Q-Q Plot](images/01_qqplot.png)

> None of the three key variables are normally distributed. Use log-transformed payment values in models, prefer non-parametric tests for review scores, and note that large n (≥30 per group) partially rescues you via the Central Limit Theorem.

---

## Part 2 — Intermediate Statistics

### How hypothesis testing works
p-value < 0.05 → reject H₀ → the difference is real.

![Hypothesis concept](images/02_hypothesis_concept.png)

> The p-value is **not** the probability that H₀ is true. It's the probability of seeing data this extreme *if* H₀ were true. A small p-value means the observed difference would be very unlikely by chance alone.

### t-Test: Weekend vs Weekday Orders

![t-test](images/02_ttest.png)

> Weekend orders are statistically different from weekday orders, but Cohen's d is small — the practical difference is marginal (~R$5). Statistical significance ≠ business significance. Always check effect size alongside the p-value.

### Chi-Square: Payment Method × Delivery

![Chi-square](images/02_chisquare.png)

> Boleto (Brazil's bank slip payment) has the lowest delivery rate among payment methods. Boleto payments can be cancelled or expire before fulfillment — a known friction point in Brazilian e-commerce. Cramer's V is weak, but the pattern is real and worth investigating.

### Correlation
Longer delivery → lower ratings. Both Pearson and Spearman agree.

![Correlation heatmap](images/02_correlation_heatmap.png)
![Scatter plots](images/02_scatter_correlation.png)

> The delivery–rating correlation (r ≈ −0.25) is real and significant, but not huge. Delivery speed is *one* factor in satisfaction, not the whole story. Product quality, price, and packaging likely matter too — and they're not in this dataset.

### Simple Linear Regression

![Regression](images/02_regression.png)

> R² = 0.04 means delivery time alone explains only 4% of score variance. The model is statistically significant (p < 0.001) but practically weak. Classic signal to add more features — which is exactly what Part 3 does.

---

## Part 3 — Advanced Statistics

### One-Way ANOVA
Credit card orders are significantly higher in value than other payment methods.

![ANOVA](images/03_anova.png)

> Credit card orders average ~R$164, nearly double voucher orders (~R$66). This isn't just about payment preference: credit cards unlock installment payments in Brazil, enabling larger purchases. ANOVA tells us *some* group differs — Tukey HSD tells us *which ones*.

### Multiple Regression
`is_late` is the strongest negative predictor of review score.

![Multiple regression](images/03_multiple_regression.png)

> Even with 7 features, R² is only ~0.11 — roughly 89% of score variance is unexplained by logistics alone. Product quality, price perception, and customer expectations are likely the real drivers, but they're not in this dataset.

### Bootstrap Confidence Intervals
10,000 resamples — no distribution assumption needed.

![Bootstrap](images/03_bootstrap.png)

> With n > 90k orders, the bootstrap CI for the mean is very tight (±~R$1). This shows the law of large numbers at work: large samples give very precise estimates. The bootstrap and the formula-based CI agree closely — the data behaves well at scale.

### A/B Test: On-time vs Late Delivery
On-time delivery significantly boosts customer ratings (small but real effect).

![A/B test](images/03_ab_test.png)

> The effect is significant (p < 0.001) but Cohen's d ≈ 0.3 — medium-small. To detect a small effect (d=0.2) with 80% power, you need ~400 orders per group. With 3,000 per group here, we're well-powered. Every day of delay chips away at customer trust, even if the individual effect is modest.

### Confidence Intervals by State

![Confidence intervals](images/03_confidence_intervals.png)

> States with wide CIs (AP, RO, AC) have fewer orders — less data means more uncertainty. Don't make geographic business decisions based on point estimates alone. States whose CI sits entirely above the national mean are genuinely high-satisfaction markets.

### Kruskal-Wallis: Scores by Month

![Kruskal-Wallis](images/03_kruskal_month.png)

> Review scores dip in certain months — likely correlated with peak demand periods (Black Friday, Christmas) when logistics get strained. Kruskal-Wallis confirms this isn't random noise. A natural follow-up: check whether delivery delays spike in the same months.

---

## Setup

```bash
git clone https://github.com/sualpsudas/olist-statistics-science.git
cd olist-statistics-science
pip install -r requirements.txt
jupyter notebook
```

Data: [Olist Brazilian E-Commerce — Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
