# Sephora-Merchandise-Analysis

# Sephora Merchandising Analysis (Python)

A merchandising-focused analysis of retail transactions to understand brand performance, category seasonality, top SKUs, customer segments, discount behavior, and channel mix. Dashboard is in progress.

## Data
File: sephora_noisy_data.csv

Columns used:
order_id, order_date, client_id, client_segment, channel, category, brand, product_name, unit_price, units_sold, discount_pct, gross_revenue, net_revenue

## Data issues
- invalid/missing order_date values
- malformed or missing client_id values
- missing category values (breaks category rollups)
- missing product_name values
- missing unit_price or units_sold values
- missing/inconsistent revenue fields

## Cleaning approach
- parsed order_date with to_datetime (invalid values coerced to null)
- standardized client_id by keeping expected IDs (starting with C) and setting invalid IDs to null
- dropped rows with missing category
- filled missing product_name with "Unknown Product"
- handled missing units_sold (filled with 0) and unit_price (filled with median)
- recomputed gross_revenue as units_sold * unit_price
- filled missing net_revenue using gross_revenue when needed

## What the notebook produces
- brand KPI tables (revenue, units, discount)
- monthly category trends for seasonality
- top products by net revenue (excluding "Unknown Product")
- segment revenue and repeat purchase distribution
- discount vs units/revenue views
- channel comparison (online vs in-store)

## Run
- open Sephora_Analysis.ipynb and run all cells
- ensure sephora_noisy_data.csv is available in the working directory

## Author
Lajvi Bhavsar
