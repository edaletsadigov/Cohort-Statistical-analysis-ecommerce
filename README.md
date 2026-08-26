# E-Commerce Cohort & Retention Analysis

Cohort, RFM segmentation, and statistical analysis of a 12-month e-commerce order dataset (286K order lines / 64K customers), built in pandas + Plotly.

## 📊 Dashboard

![Sales Performance Dashboard](Charts/00_dashboard.png)

*(Interactive in the notebook — region/category slicers via `ipywidgets`; static snapshot above shows the unfiltered view.)*

## 📈 Charts

| | | |
|---|---|---|
| [Monthly Unique Orders](Charts/01_monthly_unique_orders.png) | [Monthly Unique Customers](Charts/02_monthly_unique_customers.png) | [Monthly Total Revenue](Charts/03_monthly_total_revenue.png) |
| [ARPU Lifetime Heatmap](Charts/04_arpu_lifetime_heatmap.png) | [Weekly Retention Heatmap](Charts/05_weekly_retention_heatmap.png) | [Weekly Churn Heatmap](Charts/06_weekly_churn_heatmap.png) |
| [Category Revenue vs Repeat Rate](Charts/07_category_revenue_repeat_rate.png) | [RFM Segment Map](Charts/08_rfm_segment_map.png) | [Geographic Analysis](Charts/09_geographic_revenue_repeat_rate.png) |
| [Spearman Correlation Matrix](Charts/10_spearman_correlation_matrix.png) | [Monthly Orders & AOV](Charts/11_monthly_orders_aov.png) | [Seasonality Anomaly Detection](Charts/12_seasonality_anomaly_detection.png) |

Full explanation of every chart (what it shows + the takeaway) is in [`Charts/README.md`](Charts/README.md).

## 🗂️ Repository structure

```
.
├── README.md                              ← you are here
├── cohort_analiz_ədalət_sadıqov.ipynb     ← full analysis notebook
├── Charts/
│   ├── README.md                          ← chart-by-chart explanations
│   ├── 00_dashboard.png
│   └── 01–12_*.png                        ← one PNG per chart
└── data/
    ├── README.md                          ← dataset description & column dictionary
    └── sales.csv                          ← raw dataset (286,392 rows)
```

## 🔑 Key findings

1. **Retention is the core problem.** ~94% of customers never return after their first purchase (week 0 → 1 retention drops from 100% to ~6.5%).
2. **Revenue is highly concentrated.** 3 of 15 categories generate 82.3% of revenue; `Champions` (12.4% of customers) generate 44.5% of revenue.
3. **ARPU rises with lifetime** despite low retention — the small group that returns is disproportionately valuable.
4. **December 2020 was a one-off campaign spike**, not repeated organic growth — the acquisition base is otherwise thin.
5. **Payment method correlates with loyalty** (Cramér's V = 0.29, p < 0.001); geography and gender do not.
6. **Revenue is driven more by order value than order frequency** (AOV–revenue ρ = 0.94 vs. order count–revenue ρ = 0.60).

Full methodology, hypothesis tests, and business recommendations: see the [Final Summary](cohort_analiz_ədalət_sadıqov.ipynb) section in the notebook.

## 🛠️ Stack

`pandas` · `numpy` · `plotly` (Express + Graph Objects + FigureWidget) · `scipy.stats` · `ipywidgets`

## ⚠️ Note on the dataset

`data/sales.csv` includes customer name/email/phone/SSN-style columns. This is a synthetic/practice dataset — see [`data/README.md`](data/README.md) for a privacy note before treating it as production data.

