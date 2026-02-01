# Excel Mastery Assignment-Sales Operations & Analytics

Project overview
- Role: Analyst cleaning, enriching, analyzing multi-regional electronics distributor transactional data.
- Dataset uded: (https://github.com/Mburu9anda/Data-Analysis-Project)
- Excel sheet used:(https://github.com/Mburu9anda/Data-Analysis-Project/blob/main/Excel_Assignment%20and%20Brief%20(Recovered).xlsx) 
- Deliverables: cleaned staging table, calculated columns, standardized dimensions, PivotTables, and an interactive dashboard.
- Dashboard picture: https://github.com/Mburu9anda/Data-Analysis-Project/blob/main/Screenshot%202026-02-01%20140106.png

Part A — Data cleaning & preparation
1) Staging table 
- Duplicates removal
  - Criteria: used the order ID to check for duplicates
  - Action: searched file for duplicates and none found.
- Data types
  - Converted OrderDate and RequiredDate to Date type; numeric columns (Quantity, UnitPrice, UnitCost, DiscountPct) to Number.
- Missing values
  - City to "Unknown"
  - Salesperson to "Unassigned"
  - Channel to "Unspecified"
  - Rationale: conservative placeholders to preserve records and enable grouping without fabricating values.
- Suspicious UnitPrice & DiscountPct
  - Flagging: conditional formatting for UnitPrice < 0 and DiscountPct > 0.30.
  - Correction: negative UnitPrice converted to absolute value (ABS) where appropriate; discounts >30% left flagged for business review.
- RequiredDate vs OrderDate
  - Rule: if RequiredDate < OrderDate then set RequiredDate = OrderDate + 7 days (implemented with IF). Rationale: conservative default lead time.
- LeadTimeDays
  - Derived column = RequiredDate − OrderDate (in days).

2) Calculated columns (in Excel)
- GrossRevenue = UnitPrice × Quantity × (1 − DiscountPct)
- CostOfGoods = UnitCost × Quantity
- GrossProfit = GrossRevenue − CostOfGoods
- MarginPct = IF(GrossRevenue = 0, 0, GrossProfit / GrossRevenue)

3) Standardized dimensions
- Month: MMM-YYYY from OrderDate (i.e Jan-2026)
- Quarter: label (Q1,Q2,Q3,Q4) derived from OrderDate month
- Region hierarchy: Region → Country → City (PivotTables)
- ProductCategory: standardized category text
- PriceBand: Low/Medium/High using quantiles per product set

Part B — Analyses (implemented with PivotTables)
4) Cohort analysis-first-time sales by Country and Month

5) ABC analysis by SKU within ProductCategory (GrossRevenue)
- Implementation: In pivot tablesPer category, sorted SKUs by GrossRevenue, computed cumulative% revenue and classified the categories using conditional formating for classes:
  - A = top 80%, B = next 15%, C = last 5%

6) Salesperson productivity
- Metrics per salesperson:
  - Revenue per Order = Total Revenue / Number of Orders
  - Orders per Month = Count(Orders) / Distinct Months active
  - GrossProfit per Order = Total GrossProfit / Number of Orders
- Visual: highlighted top 3 and bottom 3 performers.

7) Channel mix & cannibalization
- Revenue share by Channel × Region (PivotTable + stacked charts).
- Cannibalization signal: regions where online revenue increases while retail decreases over comparable periods; flagged Europe and Americas based on YoY/MoM comparisons.

8) Service level proxy (LeadTimeDays)
- Metric: % of orders meeting a 7-day lead time target by Country and ProductCategory.
- Implementation: in the column (LeadTimeDays ≤ 7); PivotTable shows percent meeting target.

9) Price compliance
- Checks included: compare UnitPrice to derived PriceBand; flag deviations beyond tolerance for review.

Dashboard & interactive elements
- PivotTables, slicers (Region, Country, Month, Channel, ProductCategory), and charts:
  - KPIs: Total Revenue, GrossProfit, Margin%
  - Trend charts: Revenue by Month, Channel mix by Region
  - Cohort heatmap: revenue by months-since-first
  - ABC SKU distribution and top SKUs table
  - Salesperson productivity with conditional formatting
  - Service level % meeting 7-day target
- Slicers linked to PivotTables by reporting connection for dynamic filtering.

Insights derived from the Dashboard
- In Africa, A lot of profits was collected from Distribution sales and it was a bit evenly distributed
- In America, we can note that there was high profits from both direct and online sales. 	
- In Asia direct sales were doing very well and recorded high profits			
- In Europe, direct sales were doing very well and recorded high profits			
- November had the lowest share of revenue collected and July was the best doing month	
- Accessories (ACC-7713) had the highest number of revenue collected			
- Europe had the highest number of profits despite being not the region with the highest revenue collected
- Asia was the highest in revenue collection					











