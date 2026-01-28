# Sephora-Merchandise-Analysis

An analysis of retail transactions to understand brand performance, category seasonality, top SKUs, customer segments and discount behavior


## Project goals

This analysis answers practical merchandising questions:

- Which brands drive the most revenue and volume?
- How do categories trend over time (seasonality and monthly patterns)?
- What are the top SKUs contributing to revenue?
- How do client segments behave (spend and repeat purchases)?
- Do discounts actually increase units sold or mainly reduce revenue?
- How does performance differ by channel (online vs in-store)?

## Data
Input file: sephora_data.csv

Key fields used:
order_date, client_id, client_segment, channel, category, brand, product_name,
unit_price, units_sold, discount_pct, gross_revenue, net_revenue

## What was wrong with the dataset
- order_date had missing values and invalid date strings
- client_id contained malformed IDs (example: ID-57) and missing values
- category had missing values (breaks merchandising rollups)
- product_name had missing values
- unit_price and units_sold had missing values (breaks revenue math)
- revenue fields were missing or inconsistent in some rows


## Data Cleaning Approach
- parsed order_date with to_datetime (invalid values coerced to null)
- standardized client_id by keeping expected IDs (starting with C) and setting invalid IDs to null
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

