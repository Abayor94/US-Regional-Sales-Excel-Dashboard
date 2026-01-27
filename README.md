# US Regional Sales Performance Dashboard (Excel)
*Excel · Power Query · PivotTables · Sales & Operations Analytics*

## Project Overview
This project is an Excel dashboard analyzing U.S. sales performance across channels, products, discount levels, warehouses, and fulfillment timelines to identify revenue/profit drivers and operational improvement opportunities. 
The workflow is built to be reproducible: data cleaning + feature engineering are handled in **Power Query**, then summarized with **PivotTables/PivotCharts** into a dashboard with KPI cards and visuals.
---

## Problem Statement
Sales teams and operations leaders need visibility into:
- Which channels and products drive **Net Sales** and **Profit**
- Whether discounting improves volume but hurts profitability
- Which warehouses contribute most to performance
- Whether shipping and delivery timelines vary by channel

This analysis answers those questions using an anonymized “Excel capstone dataset” of order-level transactions. 

---

## Business Questions Answered
1. Which sales channel generates the most Net Sales and Profit?
2. How do sales and volume trend by year (2018–2020)?
3. Which products contribute most to revenue?
4. Do discounts increase sales or reduce profit?
5. Which warehouses generate the highest revenue and profit?
6. Are there shipping/delivery delays by channel?

---

## KPI Snapshot (All Channels)
- **Net Sales:** $73.1M  
- **Profit:** $21.3M  
- **Gross Margin:** 29.2%  
- **Orders:** 7,991  
- **AOV:** ~$9K  
- **Avg Days to Ship:** 15.17  
- **Avg Days to Deliver:** 5.50 

---

## Key Findings
- **In-Store** is the top channel by revenue and profit.
- **2019** shows a major growth jump vs 2018; **2020** is relatively flat vs 2019.
- Discounts **above 30%** are loss-making (negative profit overall).
- Revenue/profit is concentrated in a small number of warehouses and products.
- Fulfillment averages are similar across channels; major delays are better found by outlier tracking.
  
**Business value:**  
This dashboard helps commercial and ops teams set discount guardrails, prioritize high-performing channels and warehouses, and monitor fulfillment timelines to reduce margin erosion and operational slippage. 

---

## Tools & Technologies

| Category | Tools |
|--------|------|
| Data cleaning + feature engineering | Power Query |
| Analysis + dashboard build | Excel PivotTables & PivotCharts |
| Dashboard design | KPI cards + visuals |

---

## Data Preparation (Power Query)
All cleaning and feature engineering were done in Power Query to keep the workflow reproducible (no manual edits). The M code: 
- Enforces data types (dates, text, integers, decimals)
- Cleans numeric columns (removes symbols like quotes, commas, percent signs)
- Removes duplicate OrderNumbers (to prevent double-counting)
- Flags invalid rows using an `AnomalyFlag` (e.g., qty <= 0 or unit price <= 0)
- Creates core metrics:
  - `SalesRevenue = Quantity × Unit Price`
  - `NetSales = Quantity × Unit Price × (1 − Discount)`
  - `Profit = NetSales − (Quantity × Unit Cost)`
  - `GrossMarginPct = Profit ÷ NetSales`
  - `DaysToShip = ShipDate − OrderDate`
  - `DaysToDeliver = DeliveryDate − ShipDate`
- Creates discount buckets: 0–5%, >5–15%, >15–30%, >30% 
M code file: `powerquery_m_code.txt` 

---

## Recommendations
1. **Discount Guardrails**
   - Default 0–15%
   - Approval required for 15–30%
   - Block/justify >30% because it results in net losses
2. **Channel Mix Strategy**
   - Protect In-Store performance (largest revenue + profit driver)
   - Test controlled Online growth experiments (bundles, targeted promos)
   - Preserve Wholesale margin by limiting deep discounting
3. **Warehouse Monitoring**
   - Track top warehouses monthly and investigate variance drivers
   - Prioritize fixes where high sales do not translate to high profit
4. **Fulfillment SLA Tracking**
   - Define an SLA target and flag late orders
   - Investigate late deliveries by warehouse/channel/product category 

---

## How to Run
1. Download the dataset from the linked source (Google Drive). 
2. Open `US_Regional_Sales_Dashboard_Excel.xlsx`.
3. Refresh Power Query (Data → Refresh All) to reproduce transformations.
4. Review PivotTables/PivotCharts and explore the dashboard visuals.

---

## Files
- `US_Regional_Sales_Dashboard_Excel.xlsx` — interactive workbook (Power Query + pivots + dashboard)
- `powerquery_m_code.txt` — Power Query script used for transformations
- `/Project-Images` — dashboard + pivot screenshots 

---

## Credits
Developed by **Abayomi Israel Kasali**
- LinkedIn: http://www.linkedin.com/in/abayomiisraelkasali  
- GitHub: https://github.com/Abayor94
