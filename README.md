# Inventory_analysis


## Overview
This project analyzes real-world retail transaction data to identify which products matter most to the business, and calculates when each product should be reordered to avoid stockouts.

## Dataset
"Dataset: Online Retail.xlsx (included in this repo, originally sourced from the UCI Machine Learning Repository)" — 541,909 transactions from a UK-based online gift retailer (Dec 2010 – Dec 2011).

## Steps Performed
1. **Data Cleaning** — Removed cancellations and invalid entries (negative Quantity/UnitPrice). Reduced dataset from 541,909 to 530,104 valid rows.
2. **Revenue Analysis** — Calculated total revenue per product, and removed non-product codes (postage, manual adjustments) to isolate genuine inventory items.
3. **ABC Analysis** — Classified all 3,922 products by revenue contribution:
   - Category A: 825 products (drive 80% of revenue)
   - Category B: 980 products (next 15%)
   - Category C: 2,112 products (remaining 5%)
4. **Reorder Point & Safety Stock** — Calculated demand statistics per product (average + variability of daily demand), then computed Safety Stock and Reorder Point using a 7-day lead time assumption and 95% service level (Z=1.65).
5. **Reliability Filter** — Restricted analysis to products with at least 10 days of sales history (3,149 of 3,922 products), to avoid unreliable statistics from sparse data.
6. **Visualization** — Plotted the top 10 products by Reorder Point.

## Key Findings
- Roughly 21% of products (825 of 3,922) drive 80% of total revenue — inventory management effort should be concentrated there.
- Product `23166` (Medium Ceramic Top Storage Jar) showed an unusually high Reorder Point (~33,337 units), traced back to one large bulk order skewing its demand variability — a reminder that raw statistical outputs should be sanity-checked against real-world context before acting on them.

## Assumptions
- Lead time: 7 days (not present in the original dataset, assumed for calculation purposes)
- Service level: 95%

## Tools Used
Python, pandas, matplotlib

## How to Run
```bash
pip install pandas matplotlib openpyxl
python inventory_analysis.py
```

## Files
- `inventory_analysis.py` — full analysis script
- `reorder_point_chart.png` — output visualization
- `Online Retail.xlsx` — dataset (or see download link above)
