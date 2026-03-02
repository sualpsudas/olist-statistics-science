# 📊 İstatistik Bilimi ile Veri Analizi
### Olist E-Ticaret Verisiyle Temel → İleri Seviye İstatistik

[![Python](https://img.shields.io/badge/Python-3.11-blue.svg)](https://python.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Brezilya'nın en büyük e-ticaret platformu **Olist**'in 100.000+ sipariş verisini kullanarak istatistik biliminin temel kavramlarından ileri seviye tekniklerine kapsamlı bir yolculuk.

---

## 🎯 Bu Proje Ne Öğretir?

İstatistik bilimi; sayılarla hikaye anlatma, veri tabanlı karar verme ve belirsizliği ölçme sanatıdır. Bu proje, gerçek bir e-ticaret veri setiyle istatistiği **uygulamalı** olarak öğretiyor.

---

## 📂 Proje Yapısı

```
olist-statistics-science/
├── notebooks/
│   ├── 01_temel_istatistik.ipynb       # Tanımlayıcı istatistik & görselleştirme
│   ├── 02_orta_istatistik.ipynb        # Hipotez testleri & regresyon
│   └── 03_ileri_istatistik.ipynb       # ANOVA, Bootstrap, A/B Testi
├── data/                                # Olist CSV dosyaları
├── images/                              # Üretilen grafikler
└── requirements.txt
```

---

## 📚 Notebook İçerikleri

### 01 — Temel İstatistik
| Konu | Öğrenilen Şey |
|------|---------------|
| Tanımlayıcı İstatistik | mean, median, std, skewness, kurtosis |
| Merkezi Eğilim | Ortalama vs Medyan vs Mod — ne zaman hangisi? |
| Yayılım Ölçüleri | Varyans, standart sapma, IQR, CV |
| Frekans Dağılımları | Histogram ve KDE eğrisi |
| Boxplot | Çeyrekler ve aykırı değer tespiti |
| Normallik | Shapiro testi, Q-Q plot, log dönüşümü |

### 02 — Orta Seviye İstatistik
| Konu | Öğrenilen Şey |
|------|---------------|
| Hipotez Testi | H₀/H₁, p-değeri, α, Tip I/II hata |
| t-Testi | İki grubun ortalama karşılaştırması |
| Chi-Kare | Kategorik değişkenler arası bağımlılık |
| Korelasyon | Pearson vs Spearman, ısı haritası |
| Basit Regresyon | Y = β₀ + β₁X, kalıntı analizi |

### 03 — İleri Seviye İstatistik
| Konu | Öğrenilen Şey |
|------|---------------|
| ANOVA | 3+ grup karşılaştırma, Tukey HSD post-hoc |
| Çoklu Regresyon | Standar. beta katsayıları, çapraz doğrulama |
| Bootstrap | Dağılımdan bağımsız güven aralığı |
| A/B Testi | Deney tasarımı, etki büyüklüğü, güç analizi |
| Kruskal-Wallis | Parametrik olmayan ANOVA |

---

## 🔬 Kullanılan İstatistiksel Yöntemler

```
Tanımlayıcı          → describe(), skewness, kurtosis, IQR
Normallik            → Shapiro-Wilk, Q-Q plot
Tek Grup             → z-testi, t-testi
İki Grup             → Bağımsız t-testi, Mann-Whitney U
3+ Grup              → ANOVA (F-testi), Kruskal-Wallis
Kategorik            → Chi-Kare, Cramer's V
İlişki               → Pearson r, Spearman ρ
Tahmin               → Basit + Çoklu Doğrusal Regresyon (OLS)
Yeniden Örnekleme    → Bootstrap (10,000 iterasyon)
Deney                → A/B Testi, Güç Analizi, Cohen's d
```

---

## 📊 Dataset

**Olist Brazilian E-Commerce** — Kaggle'da en çok kullanılan e-ticaret veri setlerinden biri.

| Dosya | Açıklama | Boyut |
|-------|----------|-------|
| olist_orders_dataset.csv | Sipariş başlığı | ~100K satır |
| olist_order_payments_dataset.csv | Ödeme detayları | ~100K satır |
| olist_order_reviews_dataset.csv | Müşteri yorumları | ~100K satır |
| olist_customers_dataset.csv | Müşteri bilgileri | ~100K satır |
| olist_products_dataset.csv | Ürün kataloğu | ~32K satır |
| olist_order_items_dataset.csv | Sipariş satırları | ~112K satır |

---

## 🚀 Kurulum

```bash
# Repoyu klonla
git clone https://github.com/kullanici/olist-statistics-science.git
cd olist-statistics-science

# Bağımlılıkları yükle
pip install -r requirements.txt

# Jupyter Notebook başlat
jupyter notebook
```

---

## 💡 İstatistikle Neler Yapabilirsiniz?

| Seviye | Uygulama |
|--------|----------|
| **Temel** | Satış raporları, anomali tespiti, ürün karşılaştırması |
| **Orta** | A/B testi, segment analizi, müşteri davranışı |
| **İleri** | Tahmin modelleri, deney tasarımı, iş kararı optimizasyonu |

---

## 🛠️ Teknolojiler

- **Python 3.11** — Ana dil
- **Pandas / NumPy** — Veri manipülasyonu
- **SciPy / Statsmodels** — İstatistiksel testler
- **Scikit-learn** — Makine öğrenmesi entegrasyonu
- **Matplotlib / Seaborn** — Görselleştirme

---

*Dataset: [Olist Brazilian E-Commerce on Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)*
