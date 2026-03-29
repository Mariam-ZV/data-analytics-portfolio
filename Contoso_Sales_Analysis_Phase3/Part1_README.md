# Phase 3 — Part 1: Foundation Measures

## Objective
Build core business measures using DAX to establish a reliable analytical foundation.

## Data Model Context
The **Sales** table was used as the primary fact table, containing:
- Quantity
- NetPrice (actual selling price)
- UnitCost (cost per unit)
- CustomerKey, ProductKey, StoreKey
- OrderDate

## Business Logic
- **NetPrice** represents the actual selling price after discounts → used for revenue
- **UnitCost** represents cost per unit → used for cost calculations
- **Quantity** represents units sold
- Revenue and cost must be calculated at row level (Quantity × Price/Cost)

## Measures Created

### Revenue & Cost
- **Total Sales**  
  `SUMX(Sales, Sales[Quantity] * Sales[NetPrice])`

- **Total Cost**  
  `SUMX(Sales, Sales[Quantity] * Sales[UnitCost])`

- **Total Profit**  
  `[Total Sales] - [Total Cost]`

### Volume
- **Total Quantity**  
  `SUM(Sales[Quantity])`

### Operational KPIs
- **Order Count**  
  `COUNTROWS(Orders)`

- **Distinct Customers**  
  `DISTINCTCOUNT(Sales[CustomerKey])`

- **Products Sold**  
  `DISTINCTCOUNT(Sales[ProductKey])`

## Validation
All measures were tested using PivotTables by:
- checking total values without filters
- analysing results by country, category, and time
- confirming logical relationships (e.g. Sales > Cost, Quantity aligns with Orders)
- identifying anomalies such as blanks or inconsistent values

## Key Concepts Practiced
- SUM vs SUMX (aggregation vs row-level calculation)
- COUNTROWS
- DISTINCTCOUNT
- measure referencing

## Key Learnings
- Business calculations must reflect real logic (Quantity × Price/Cost)
- SUMX is essential for row-level calculations
- Correct table selection (fact vs lookup) impacts results
- Proper formatting improves readability (Currency, Whole Number)
- Validation in PivotTables is critical for accuracy

## Outcome
A clean and reliable KPI foundation was established, enabling deeper analysis in subsequent phases.
