# Dataset — `sales.csv`

E-commerce order-line dataset used for the cohort, RFM, and statistical analysis in this repository.

## Overview

| | |
|---|---|
| Rows | 286,392 order lines |
| Columns | 33 |
| Grain | One row per **order item** (an order with 3 products = 3 rows, same `order_id`) |
| Date range | 2020-10-01 → 2021-09-30 (12 months) |
| Unique orders | 201,716 |
| Unique customers | 64,248 |
| File size | ~76 MB |

## Column dictionary

| Column | Type | Description |
|---|---|---|
| `order_id` | int | Order identifier (repeats across multiple item rows in the same order) |
| `order_date` | str (date) | Date the order was placed |
| `status` | str | Order status (`complete`, `received`, `paid`, `closed`, `canceled`, `refunded`, `pending`, etc.) |
| `item_id` | int | Line-item identifier |
| `sku` | str | Product SKU |
| `qty_ordered` | int | Quantity ordered for that line item |
| `price` | float | Unit price |
| `discount_amount` | float | Discount applied to the line item |
| `category` | str | Product category (15 unique values) |
| `payment_method` | str | Payment method used (13 unique values, e.g. `cod`, `Easypay`, `easypay_voucher`, `Payaxis`, `bankalfalah`) |
| `bi_st` | str | Internal status flag |
| `cust_id` | int | Customer identifier |
| `year`, `month` | int, str | Order year / month |
| `ref_num` | int | Reference number |
| `Name Prefix`, `First Name`, `Middle Initial`, `Last Name`, `full_name` | str | Customer name fields |
| `Gender` | str | Customer gender |
| `age` | int | Customer age |
| `E Mail` | str | Customer email |
| `Customer Since` | str (date) | Customer signup/registration date |
| `SSN` | str | Customer identifier field (see note below) |
| `Phone No.` | str | Customer phone number |
| `Place Name`, `County`, `City`, `State`, `Zip` | str/int | Address fields |
| `Region` | str | One of 4 US-style regions (`South`, `Midwest`, `West`, `Northeast`) |
| `User Name` | str | Account username |

## Derived fields used in the analysis

These are **not** in the raw file — they are created inside the notebook:
- `revenue` = `qty_ordered × price − discount_amount`
- `first_order_date`, `cohort_month` — first purchase date/month per customer, used for monthly cohorting
- `order_week`, `first_purchase_week`, `cohort_lifetime_weekly` — used for weekly retention/churn
- RFM `recency`, `frequency`, `monetary` scores and `segment` label

## Data quality notes

- **Only ~49.5% of rows have a "successful" status** (`complete`, `received`, `paid`, `closed`); the rest are canceled/refunded/pending and are excluded before revenue analysis. See the notebook's Data Cleaning section for the exact filter.
- No duplicate rows (full-row or `order_id` + `item_id`) were found.
- No missing values in any column.
- No negative revenue values after cleaning.

## ⚠️ Privacy note

This file includes columns that look like personally identifiable information — `SSN`, `E Mail`, `Phone No.`, full name, and address fields. This is a **synthetic/practice e-commerce dataset**; the values are not verified to be real people's data. Still, before publishing this file in a public repository, double-check the original source's license/terms and consider whether to strip or hash these columns (`SSN`, `E Mail`, `Phone No.`, `full_name`) — they add no value to the cohort/RFM analysis and are the highest-risk columns if the data turns out not to be fully synthetic.

