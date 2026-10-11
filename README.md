# Inventory Intelligence: Knowing What to Stock and When to Reorder


## 1. Background and Overview
An online retailer sells thousands of products. If it stocks too much, cash sits unused on shelves. If it stocks too little, customers can't buy and sales are lost.

This project uses two years of real sales history to answer two questions for every product: how much backup stock to keep, and when to place the next order.

Problem: There is no clear, data-based rule for when to reorder, so stock decisions rely on guesswork.

Objective: Build a simple reorder system and a dashboard that shows which products to reorder first and which deserve the most attention.

## 2. Data Structure Overview
- **Source:** UCI Online Retail II dataset, real sales from a UK online gift retailer.
-  **Period** : Dec 2009 to Dec 2011 (739 days).
- **Grain:** One row per invoice line item — product code, quantity, price, 
  date, customer, and country.
- **Cleaning Steps** :
  - Removed cancelled orders and the original orders they reversed.
  - Removed rows with missing product names, or zero/negative quantity or price.
  - Removed non-product codes (postage, manual entries).
  - Merged product codes that differed only by spaces or capital letters.
- **How it was built**: sales lines, then daily sales per product, then one summary row per product.

## 3. Executive Summary
- About 21% of products (1,157 of 5,432) bring in 80% of revenue (£21.98M of £27.48M). Running out of these costs the most.
- 93.6% of products (5,084 of 5,432) fall below their reorder point. This is high because stock levels are simulated, not real (see Section 6).
- Weekday and weekend sales are different, the top seller is slowly declining, and fast vs slow movers need different handling.

## 4. Insights Deep Dive
- Where the money comes from (ABC analysis) :
 - Category A: 1,157 products, £21.98M, 80% of revenue.
 - Category B: 1,462 products, £4.12M, 15% of revenue.
 - Category C: 2,813 products, £1.37M, 5% of revenue. Most of the catalog adds very little.

- What needs reordering :
  - 5,084 of 5,432 products are flagged "Reorder Now". The flag compares simulated stock to each product's reorder point.

- Demand patterns :
  - Weekday and weekend sales differ in a way that is not random (statistical test, p < 0.05).
  - Top seller 85123A (White Hanging Heart T-Light Holder) is slowly declining, about 0.17 units per day. The trend is real but small, explaining under 3% of day-to-day ups and downs.
  - Products were tagged fast or slow moving by how often they are ordered. Almost all  Category A products are fast movers (1,130 of 1,157). Only 27 are slow movers, so check these first for one-off bulk orders.
  - Most Category C products are slow movers (2,438 of 2,813). These are the best candidates for lean stock.
  - 
## 5. Recommendations
- Review reorder points for Category A most often, since stock-outs there cost the most.
- Use simple, less frequent checks for Category C.
- Before reordering a slow mover, check that it has sold recently.
- Keep extra backup stock only for products with unpredictable demand.
- Connect real stock data before using the reorder flags for real decisions.

## 6. Assumptions and Limitations
- **Current stock is simulated**: Each product was given a random 1 to 19 days of stock. The  flags show how the method works, not a real shortage.
- **Lead time is 7 days for every product**: The dataset has no supplier data.
Service level is 95% (Z = 1.65): a common starting point, not set by the business.
- **Demand swings use only days with sales**: This understates risk for slow products.
- **Unit price** is estimated as revenue divided by units sold, so inventory value is an estimate.
- **Results come from one UK retailer** and may not apply to others.

## 7. Future Enhancements
- Use real stock levels and supplier lead times.
- Include zero-sale days when measuring demand swings.
- Forecast future demand, not just describe the past.
- Add product cost data for a true inventory value.

## 8. Deliverables
- `online_retail_II.csv` — raw dataset
- `cleaned_retail.csv` — cleaned transaction data
- `daily_demand.csv` — daily demand per product
- `final_inventory_with_abc.csv` — reorder points, ABC category and flags per product 
- `Inventory_Dashboard.pbix` — Power BI dashboard file

## 9. Outcomes Preview 
- Dashboard : https://github.com/yashmonde24/inventory-intelligence-demand-driven-reorder-point/blob/main/powerbi/Dashboard.pdf

