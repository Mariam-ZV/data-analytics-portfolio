# Phase 3 — Part 3: CALCULATE, FILTER, ALL (Advanced DAX Context)

## Objective
Develop a deep understanding of filter context in DAX and use it to build dynamic, context-aware business measures.

## Tools Used
- Power Pivot (Data Model)
- DAX: CALCULATE, FILTER, ALL, DIVIDE

## Key Concepts
- filter context determines how measures are evaluated
- CALCULATE modifies filter context
- ALL removes filters for comparison against totals
- FILTER applies row-level conditions
- measures dynamically respond to PivotTables and report filters

## Measures Created

### CALCULATE Baseline
- **Total Sales (CALCULATE Test)**  
  `CALCULATE([Total Sales])`  
  Purpose: confirm CALCULATE returns the same result without additional filters

---

### Fixed Filter Measure
- **Sales UK**  
  `CALCULATE([Total Sales], Store_Lookup[CountryName] = "United Kingdom")`  
  Purpose: enforce a fixed country filter regardless of report context

---

### Removing Filters
- **Sales All Countries**  
  `CALCULATE([Total Sales], ALL(Store_Lookup[CountryName]))`  
  Purpose: calculate total sales independent of country filters

---

### Contribution to Total
- **% of Total Sales**  
  `DIVIDE([Total Sales], [Sales All Countries])`  
  Purpose: calculate each country’s share of total sales

---

### Row-Level Filtering
- **Profitable Sales**  
  `CALCULATE([Total Sales], FILTER(Sales, Sales[NetPrice] > Sales[UnitCost]))`  
  Insight: all transactions are profitable, confirming consistent positive margins

---

### Conditional Business Filtering
- **High Value Sales**  
  `CALCULATE([Total Sales], FILTER(Sales, Sales[NetPrice] >= 1000))`  
  Purpose: isolate revenue from high-value transactions

---

### Share of High-Value Sales
- **% High Value Sales**  
  `DIVIDE([High Value Sales], [Total Sales])`  
  Purpose: measure dependence on premium-priced sales

---

## Validation
All measures were tested using PivotTables:
- verified behaviour across countries and categories
- confirmed logical consistency (no impossible values)
- ensured correct totals (e.g. % of Total = 100%)

## Key Insights
- United States and Online channels dominate total sales contribution
- high-value sales account for approximately 32% of total revenue
- UK, Italy, and US show higher reliance on premium-priced products
- dataset contains no loss-making transactions
- overall profit margins are consistently positive

## Business Interpretation
The business operates with strong and consistent profitability. A significant portion of revenue comes from higher-value products, although reliance on these varies by region, indicating different market behaviours.

## Key Learning
DAX is not just about writing formulas — it is about controlling filter context. Understanding how to add, remove, and manipulate filters is essential for meaningful analysis and real-world data work.
