## Inventory Intelligence : Demand - Driven Reorder Point 

## Overview
This project analyzes real retail transaction data to help decide two things:
how much stock to keep, and when to reorder it.

## Problem
Businesses lose money two ways — holding too much inventory (extra cost) 
or too little (lost sales). This project builds a simple, data-driven way 
to find the right balance.

## Dataset
- **Source:** UCI Online Retail II dataset
- **Size:** 1 million transactions across 2 years (2009–2011)
- **Details:** Real UK-based online retail transactions, including 
               product codes, quantities, prices, and dates

## Approach
1. Cleaned and combined raw transaction data (Python, Pandas)
2. Calculated daily demand per product
3. Calculated average demand and demand variability per product
4. Applied standard inventory formulas:
   - Safety Stock
   - Reorder Point (ROP)
5. Simulated current stock levels (real-time stock data not available 
   in source dataset)
6. Classified products using ABC analysis based on revenue contribution
7. Built an interactive Power BI dashboard

## Key Assumptions
- Lead time: 7 days (industry-standard placeholder, no supplier data available)
- Service level: 95% (Z = 1.65)
- Current stock: simulated, since dataset has no live inventory data
- Unit price: estimated from revenue ÷ quantity sold (no direct cost column)

All assumptions are clearly documented since real-world data wasn't 
available for every input — this is a common and honest approach 
in analytics projects.

## Dashboard Features
- KPI cards: Total SKUs, SKUs needing reorder, estimated inventory value
- Reorder alert table with ABC priority
- ABC revenue breakdown chart
- Top products by demand
- Interactive filters by category and reorder status

## Tools Used
- Python (Pandas, NumPy)
- Power BI (DAX, data modeling)
- Excel (source data)

## Key Insight
- **4,746 SKUs** analyzed across £27.56M in total revenue
- **25% of SKUs (Category A, 1,171 products)** generated **80% of revenue 
  (£22.05M)** — a small share of the catalog drives most of the business
- **Category B (1,488 SKUs, 31%)** contributed 15% of revenue (£4.14M) — 
  moderate priority for inventory control
- **Category C (2,972 SKUs, 63%)** contributed just 5% of revenue (£1.38M) — 
  lowest priority, can run leaner reorder rules
- **95.4% of SKUs** were flagged for reorder under simulated stock levels — 
  a result of the narrow simulated stock range (1–19 days of stock), not an 
  actual shortage. With real stock data, this number would likely be lower
- **Estimated inventory value: £378.17K** across all products, based on 
  simulated stock × historical average selling price

## Recommendations
- Prioritize Category A first. These 1,171 SKUs (25% of catalog) drive 80% of revenue (£22.05M) — reorder accuracy matters most here, since a stockout on these products has the biggest revenue impact.
- Loosen control on Category C. 2,972 SKUs (63% of catalog) contribute just 5% of revenue (£1.38M) — tight reorder monitoring here isn't worth the operational effort; simpler, less frequent review is enough
- Replace simulated stock with real inventory data. The 95.4% reorder-flag rate is inflated by the stock simulation assumption (1–19 days of stock range), not a real shortage. Connecting this to actual warehouse/ERP data would make the reorder signal trustworthy for real decisions.
- Validate the 7-day lead time assumption. This was a placeholder due to missing supplier data. Real lead times likely vary by product — using actual figures would make safety stock and reorder points meaningfully more accurate.
- Improve demand variability calculation. Current variability only considers days with sales. Including zero-sale days would likely raise variability estimates for slow-moving products, giving more realistic safety stock for those SKUs.
- 
## Files
- `online_retail_II.csv`- Raw dataset
- `cleaned_retail.csv` - Cleaned transaction data
- `daily_demand.csv` - Daily demand per product
- `final_inventory_with_abc.csv` - Final analysis with reorder points and ABC tags
- `Insights Visualization.csv` - Power BI dashboard file

