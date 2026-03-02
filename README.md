# Statistics Science with Real E-Commerce Data

Using 100k+ orders from **Olist** (Brazil's largest e-commerce platform) to explore statistics from the ground up — basic, intermediate, and advanced.

[![Python](https://img.shields.io/badge/Python-3.11-blue.svg)](https://python.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org)
[![NumPy](https://img.shields.io/badge/NumPy-1.26-013243?logo=numpy&logoColor=white)](https://numpy.org)
[![SciPy](https://img.shields.io/badge/SciPy-1.13-8CAAE6?logo=scipy&logoColor=white)](https://scipy.org)
[![scikit--learn](https://img.shields.io/badge/scikit--learn-1.5-F7931E?logo=scikit-learn&logoColor=white)](https://scikit-learn.org)
[![statsmodels](https://img.shields.io/badge/statsmodels-0.14-lightgrey)](https://www.statsmodels.org)

---

## Dataset

[Olist Brazilian E-Commerce](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) — Kaggle &nbsp;·&nbsp; ~100,000 orders &nbsp;·&nbsp; 9 relational tables &nbsp;·&nbsp; 2016–2018

| Table | Description |
|-------|-------------|
| `orders` | Order lifecycle and timestamps |
| `order_items` | Products, prices, sellers per order |
| `order_payments` | Payment type and value |
| `order_reviews` | Customer review scores and comments |
| `customers` | Customer location data |
| `products` | Product dimensions and category |
| `sellers` | Seller location data |
| `geolocation` | Brazilian zip code coordinates |
| `product_category_name_translation` | PT → EN category names |

---

## Project Structure

```
olist-statistics-science/
├── notebooks/
│   ├── 01_basic_statistics.ipynb       # Descriptive stats, distributions, normality
│   ├── 02_intermediate_statistics.ipynb # Hypothesis tests, correlation, regression
│   └── 03_advanced_statistics.ipynb    # ANOVA, multiple regression, bootstrap, A/B test
├── data/                                # Olist CSV files (not tracked in git)
├── images/                              # 18 charts generated across all 3 notebooks
└── requirements.txt
```

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

## Statistical Methods Covered

| Method | Notebook |
|--------|----------|
| Descriptive statistics (mean, median, mode, std, IQR, CV) | 01 |
| Skewness & kurtosis | 01 |
| Frequency distributions & KDE | 01 |
| Boxplot & IQR outlier detection | 01 |
| Shapiro-Wilk normality test | 01 |
| Q-Q plot | 01 |
| Log transformation | 01 |
| z-test (one sample) | 02 |
| Independent samples t-test (Welch) | 02 |
| Levene's test (variance equality) | 02 |
| Chi-square independence test | 02 |
| Cramer's V (effect size) | 02 |
| Pearson & Spearman correlation | 02 |
| Simple OLS linear regression | 02 |
| Residual analysis | 02 |
| One-way ANOVA + F-test | 03 |
| Tukey HSD post-hoc test | 03 |
| Kruskal-Wallis (non-parametric ANOVA) | 03 |
| Multiple linear regression (statsmodels OLS) | 03 |
| Standardised beta coefficients | 03 |
| 5-fold cross-validation (R²) | 03 |
| Bootstrap (10,000 resamples) | 03 |
| A/B test design & analysis | 03 |
| Cohen's d (effect size) | 03 |
| Statistical power analysis | 03 |
| 95% Confidence intervals | 03 |

---

## Key Findings

| Finding | Value |
|---------|-------|
| Avg order value (mean) | R$154 — but median is R$108 (right-skewed) |
| Review score distribution | ~57% of customers give 5 stars |
| Avg delivery time | ~12 days (non-normal, long tail) |
| Outlier rate (IQR method) | ~7% of orders |
| Late delivery score | **2.57** vs on-time **4.29** — 1.7-point gap |
| Weekend vs weekday orders | Statistically different, but Cohen's d is small (~R$5) |
| Delivery–rating correlation | r = −0.25 (Pearson), significant at p < 0.001 |
| Simple regression R² | 0.04 — delivery time alone explains 4% of score variance |
| Multiple regression R² | 0.11 — 7 features explain 11% of score variance |
| Top CLV quartile vs bottom | R$382 vs R$43 — 9× gap |
| Bootstrap CI (mean order value) | ±~R$1 at 95% — very tight with n > 90k |

---

## Tech Stack

![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2.2-150458?logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-1.26-013243?logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-3.9-orange)
![Seaborn](https://img.shields.io/badge/Seaborn-0.13-4C72B0)
![SciPy](https://img.shields.io/badge/SciPy-1.13-8CAAE6?logo=scipy&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.5-F7931E?logo=scikit-learn&logoColor=white)
![statsmodels](https://img.shields.io/badge/statsmodels-0.14-lightgrey)

---

## How to Run

```bash
# 1. Clone the repo
git clone https://github.com/sualpsudas/olist-statistics-science.git
cd olist-statistics-science

# 2. Install dependencies
pip install -r requirements.txt

# 3. Download the dataset from Kaggle
# https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce
# Place the CSV files in the data/ folder

# 4. Run any notebook
jupyter notebook notebooks/01_basic_statistics.ipynb
```

---

*Dataset: [Olist @ Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) — CC BY-NC-SA 4.0*
