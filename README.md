# Sephora-Merchandise-Analysis

Transaction-level merchandising analysis focused on **brand performance**, **category seasonality**, **SKU-level winners**, **customer behavior**, **discount impact**, and **channel mix**.

The main work is in the notebook: `Sephora_Analysis.ipynb`.  
A dashboard is in progress (coming next).

---

## What this project covers

### 1) Data cleaning (fixes common retail data issues)
The dataset (`sephora_noisy_data.csv`) includes missing values and inconsistent formatting. The notebook cleans and standardizes:

- **`order_date`**: parsed to real dates (invalid dates coerced to null)
- **`client_id`**: removes malformed IDs (keeps expected format)
- **`category`**: drops rows where category is missing (can’t be used for merchandising rollups)
- **`product_name`**: fills missing names with `"Unknown Product"`
- **`unit_price` / `units_sold`**: handles missing values so revenue metrics don’t break
- **`gross_revenue` / `net_revenue`**: recomputes revenue fields to ensure consistency  
  - `gross_revenue = unit_price * units_sold`  
  - `net_revenue` recalculated using discount percentage

---

### 2) Feature engineering
Adds fields used for trend and segmentation analysis:

- Date parts from `order_date`: **month**, **weekday**, **quarter**
- **Price tier buckets**: `Budget`, `Mid`, `Premium`, `Luxury`
- **Holiday season flag** for seasonal comparisons

---

### 3) Core merchandising analysis

#### Brand performance
KPIs per brand:
- Total **net revenue**
- Total **units sold**
- Average **discount %**
- Combined KPI summary table for quick ranking and comparison

Notebook highlights (from the current run):
- Rare Beauty leads on revenue (about **$63.7K**) and units (about **1,521**)
- Discount behavior is clustered across brands (roughly mid-teens % on average)

#### Category trend and seasonality
Monthly net revenue trend by category (used to spot seasonal spikes and dips).

Notebook highlights:
- **Fragrance** spikes around **Sep–Oct**
- **Makeup** peaks around **May–Jun**
- **Skincare** is steadier with a mid-year dip and year-end pickup
- **Haircare** is lowest and relatively stable

#### SKU-level product analysis
Identifies top-performing products by revenue and units to support assortment decisions.

Notebook highlights:
- Fragrance products dominate the highest SKU-level revenue list
- Skincare has several strong performers
- Makeup revenue is spread across more SKUs

#### Client behavior analytics
Looks at how customers behave and how often they come back:
- Revenue by **client segment**
- **Repeat purchase frequency** (how many customers buy 1x, 2x, 3x…)

Notebook highlights:
- Most customers buy only once → clear retention opportunity

#### Discount impact
Explores how discounting relates to:
- Units sold
- Revenue

#### Channel analysis
Compares performance across channels (online vs in-store).

Notebook highlights:
- Online revenue is slightly higher, but overall the split is fairly balanced

---

## Dataset

Expected file: `sephora_noisy_data.csv`

The notebook uses these fields (at minimum):

- `order_id`
- `order_date`
- `client_id`
- `client_segment`
- `channel`
- `category`
- `brand`
- `product_name` (SKU)
- `unit_price`
- `units_sold`
- `discount_pct`
- `gross_revenue`
- `net_revenue`

> If you’re publishing this repo publicly, keep the raw dataset out of version control if it contains any sensitive or proprietary content. If it’s synthetic, note that clearly in the repo.

---

## Repo structure (recommended)

```text
sephora-merchandising-analysis/
├─ data/
│  ├─ sephora_noisy_data.csv
├─ notebooks/
│  ├─ Sephora_Analysis.ipynb
├─ dashboard/                    # in progress
│  ├─ (tableau|powerbi|streamlit)/...
├─ images/                       # charts/screenshots for README + dashboard
├─ requirements.txt
└─ README.md
