# Charts

This folder contains every chart and the dashboard from `cohort_analiz_ədalət_sadıqov.ipynb`, exported as static PNGs (via Plotly + Kaleido) so they render directly on GitHub.

---

## 00 — Dashboard
![Dashboard](00_dashboard.png)

Consolidated view (unfiltered / "All" scope): total revenue, total orders, total customers, AOV, and repeat rate, alongside revenue by category, revenue by region, customer segment distribution (RFM), monthly revenue trend, and orders by payment method. In the notebook this is interactive (region/category slicers via `ipywidgets`); here it is a static snapshot of the default view.

---

## 01 — Monthly Unique Orders per Cohort
![Monthly unique orders](01_monthly_unique_orders.png)

Number of unique orders placed by each monthly acquisition cohort. **2020-12 is the clear peak**, followed by a sharp drop in 2021-01/02, with a smaller secondary wave in 2021-04 and 2021-06.

## 02 — Monthly Unique Customers per Cohort
![Monthly unique customers](02_monthly_unique_customers.png)

Same pattern as above, at the customer level: the Dec-2020 cohort is 3–9x larger than any other month, pointing to a one-off seasonal campaign rather than sustained organic growth.

## 03 — Monthly Total Revenue per Cohort
![Monthly total revenue](03_monthly_total_revenue.png)

Revenue mirrors the order/customer volume pattern — confirming the Dec-2020 spike was a volume effect, not a value effect.

## 04 — ARPU Lifetime Heatmap (Monthly Cohorts)
![ARPU heatmap](04_arpu_lifetime_heatmap.png)

Average Revenue Per User for each cohort at each month of lifetime. ARPU tends to **rise** with lifetime despite low retention — the few customers who do return spend more per person than first-time buyers. Low retention, but high value among the retained.

## 05 — Weekly Retention Heatmap
![Weekly retention heatmap](05_weekly_retention_heatmap.png)

Retention rate (%) for each weekly cohort across lifetime weeks. Average retention collapses from 100% (week 0) → ~6.5% (week 1) → ~6.0% (week 2) — roughly 94% of customers never return after their first purchase.

## 06 — Weekly Churn Rate Heatmap
![Weekly churn heatmap](06_weekly_churn_heatmap.png)

The mirror image of retention (`churn = 1 − retention`). Churn stabilizes above 90% after week 1, meaning that once a customer is lost, they almost never come back.

## 07 — Category Revenue, Colored by Repeat-Customer Rate
![Category revenue](07_category_revenue_repeat_rate.png)

Net revenue by product category, colored by that category's repeat-purchase rate. Just 3 of 15 categories — `Mobiles & Tablets`, `Appliances`, `Entertainment` — generate 82.3% of total revenue (`Mobiles & Tablets` alone: 47.4%). `Men's Fashion` leads customer **acquisition** (10,595 unique customers) despite low AOV, making it a strong entry-point category, while `Mobiles & Tablets` leads both revenue and repeat-purchase rate (40.3%).

## 08 — RFM Segment Map
![RFM segment map](08_rfm_segment_map.png)

Bubble chart of customer segments (Recency vs. Frequency; bubble size = customer count; color = revenue share). `Champions` (12.4% of customers) generate 44.5% of revenue; `Champions + Can't Lose Them` (21.0% of customers) generate 67.3% of revenue. Segment size and segment value are not the same thing — `Promising` and `Hibernating/Lost` together make up over a third of customers but only 1.9% of revenue.

## 09 — Geographic Analysis (Revenue & Repeat Rate by Region)
![Geographic analysis](09_geographic_revenue_repeat_rate.png)

Revenue and repeat-purchase rate by region. Revenue is roughly proportional to customer base — `South` leads with 37.6% of revenue and 37.0% of customers — and AOV (1,730–1,916) plus repeat rate (34.8%–35.7%) are similar across all four regions. No meaningful region-specific behavioral difference was found; geographic targeting should be driven by market size, not by assumed regional differences.

## 10 — Spearman Correlation Matrix (Customer-Level Metrics)
![Correlation matrix](10_spearman_correlation_matrix.png)

Spearman correlation across customer-level metrics (total revenue, order count, AOV, quantity, SKU diversity, etc.). AOV correlates more strongly with total revenue (ρ = 0.94) than order count does (ρ = 0.60) — revenue is driven more by how much customers spend per order than by how often they order. **Correlation does not imply causation** — these are associations within the observed data only.

## 11 — Monthly Orders and AOV
![Monthly orders and AOV](11_monthly_orders_aov.png)

Order volume (bars) vs. average order value (line) by month, on dual axes — used to check whether volume swings were accompanied by value swings (they largely were not).

## 12 — Seasonality / Anomaly Detection
![Seasonality anomaly detection](12_seasonality_anomaly_detection.png)

Monthly order counts flagged for anomalies using a z-score threshold (|z| > 0.8). Two months stand out: **2020-12** (z = 2.82, the campaign spike) and **2021-04** (z = 0.89, a smaller secondary wave).

---

### Key takeaways across all charts
- **Retention is the core problem**, not acquisition: ~94% of customers churn after one purchase.
- **Revenue is concentrated** in a few categories, a few customer segments (Champions), and one acquisition spike (Dec-2020).
- **Geography and gender show no meaningful behavioral difference**; payment method does (Cramér's V = 0.29, p < 0.001) — `cod` has the lowest repeat rate, `easypay_voucher` the highest.

Full methodology, statistical tests, and business recommendations are in the notebook: [`cohort_analiz_ədalət_sadıqov.ipynb`](../cohort_analiz_ədalət_sadıqov.ipynb).

