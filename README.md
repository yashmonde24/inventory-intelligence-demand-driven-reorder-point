# Inventory Intelligence: Demand-Driven Reorder Point Optimization

## 1. Background and Overview
Every retailer deals with the same tension — hold too much stock and cash 
gets stuck on shelves, hold too little and you lose sales when items run out. 
Most businesses don't have a clean system to catch this in time.

This project builds that system from scratch, using real transaction data 
from a UK-based online retailer. The goal was simple: for every product, 
know how much stock to keep, and know exactly when to reorder — before 
it becomes a problem.

## 2. Data Structure Overview
- **Source:** UCI Online Retail II dataset
- **Scale:** ~1 million transactions, spanning 2 years (2009–2011)
- **Grain:** One row per invoice line item — product code, quantity, price, 
  date, customer, and country
- **Processing:** Raw transactions were cleaned, then aggregated up to daily 
  demand per product, then further summarized into per-SKU metrics (demand, 
  variability, revenue) — three layers, each feeding the next

## 3. Executive Summary
Across 4,746 products and £27.56M in revenue, one pattern stood out clearly: 
**a small slice of the catalog carries the business.** Just 25% of SKUs 
generate 80% of revenue. That single fact should shape how inventory gets 
managed — not every product deserves the same level of attention.

The dashboard also flagged that most SKUs currently sit below their 
reorder point — though this needs a caveat, covered in Section 6.

## 4. Insights Deep Dive
- **Revenue is concentrated, not spread out.** Category A — 1,171 SKUs 
  (25% of catalog) — drives £22.05M, or 80% of total revenue
- **The long tail is real.** Category C — 2,972 SKUs (63% of catalog) — 
  contributes just £1.38M, only 5% of revenue. Nearly two-thirds of the 
  product list barely moves the needle
- **Category B sits in between** — 1,488 SKUs (31%) generating £4.14M (15%), 
  a moderate-priority middle ground
- **95.4% of SKUs were flagged for reorder** — this number is high because 
  of a data limitation (see Assumptions), not because the business is 
  actually in a stock crisis
- **Estimated inventory value: £378.17K**, calculated from simulated stock 
  levels multiplied by each product's historical average selling price

## 5. Recommendations
- **Protect Category A first.** These 1,171 SKUs carry 80% of revenue — 
  a stockout here costs the most, so reorder accuracy should be reviewed 
  most often for this group
- **Ease up on Category C.** With only 5% revenue share across 2,972 SKUs, 
  tight monitoring isn't worth the effort — a simpler, less frequent review 
  cycle is enough
- **Plug in real stock data.** The 95.4% reorder rate is inflated by 
  simulated stock assumptions. Connecting this model to actual warehouse 
  or ERP data would make the reorder signal something the business can 
  actually act on
- **Get real lead times from suppliers.** The current 7-day assumption is 
  a placeholder. Lead time likely varies by product, and using real figures 
  would sharpen the safety stock and reorder point numbers
- **Rework the variability calculation.** Right now, demand variability only 
  looks at days with sales. Factoring in zero-sale days would give a more 
  honest — likely higher — variability estimate, especially for slow-moving 
  products

## 6. Assumptions and Limitations
- **Lead time (7 days):** placeholder, since the dataset has no supplier data
- **Service level (95%, Z = 1.65):** a standard starting point, not 
  business-specific
- **Current stock:** simulated, since the dataset has no live inventory feed 
  — this is the main reason the reorder-flag rate looks high
- **Unit price:** estimated as revenue ÷ quantity sold, since there's no 
  direct cost column in the source data

These aren't hidden — they're the honest boundaries of what this dataset 
can support. Every one of them is a clear next step if this were handed 
off to a live business.

## 7. Future Enhancements
- Replace simulated stock with a real, live inventory feed
- Bring in actual supplier lead times instead of a fixed assumption
- Recalculate demand variability including zero-sale days
- Add a cost column (if available) instead of estimating unit price from revenue
- Extend the model to forecast future demand, not just describe past demand

## 8. Deliverables
- `online_retail_II.csv` — raw dataset
- `cleaned_retail.csv` — cleaned transaction data
- `daily_demand.csv` — daily demand per product
- `final_inventory_with_abc.csv` — final analysis with reorder points and ABC tags
- `Inventory_Dashboard.pbix` — Power BI dashboard file

## 9. Outcomes Preview 
- Dashboard : https://github.com/yashmonde24/inventory-intelligence-demand-driven-reorder-point/blob/main/powerbi/Dashboard.pdf

