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
A small percentage of products (Category A) drive the majority of revenue. 
These products need the tightest reorder accuracy, since stockouts here 
are the most costly.

## Files
- `online_retail_II.csv`- Raw dataset
- `cleaned_retail.csv` - Cleaned transaction data
- `daily_demand.csv` - Daily demand per product
- `final_inventory_with_abc.csv` - Final analysis with reorder points and ABC tags
- `Insights Visualization.csv` - Power BI dashboard file

