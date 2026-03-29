# Phase 3 — Part 2: KPI & Business Logic

## Objective
Transform foundational measures into meaningful business KPIs and introduce logic-based analysis using DAX.

## Measures Created

### KPI Measures

- **Profit Margin %**  
  Definition: Percentage of profit relative to total sales  
  `Profit Margin % := DIVIDE([Total Profit], [Total Sales])`

- **Average Order Value (AOV)**  
  Definition: Average revenue generated per order  
  `Average Order Value := DIVIDE([Total Sales], [Order Count])`

- **Average Quantity per Order**  
  Definition: Average number of items sold per order  
  `Average Quantity per Order := DIVIDE([Total Quantity], [Order Count])`

---

### Logic-Based Measures

- **Profit Status**  
  Definition: Classifies overall profitability  
  `Profit Status := IF([Total Profit] > 0, "Profitable", "Loss-Making")`

- **Sales Band**  
  Definition: Groups sales into performance categories  

  Logic:
  - Low: < 1,000,000  
  - Medium: 1,000,000 – 5,000,000  
  - High: > 5,000,000  

  `Sales Band :=  
  SWITCH(  
      TRUE(),  
      [Total Sales] < 1000000, "Low",  
      [Total Sales] < 5000000, "Medium",  
      "High"  
  )`

---

## Key Concepts Practiced
- building ratio measures using DIVIDE()
- understanding filter context in measures
- converting raw aggregations into business KPIs
- creating logic-based measures using IF and SWITCH(TRUE())
- recognising how model structure affects results

## Validation
Measures were tested using PivotTables across multiple levels:
- country level (high-level validation)
- product level (granular behaviour)

Checks performed:
- no blank values
- no divide-by-zero errors
- no unrealistic or negative margins
- consistent Sales Band classification
- Profit Status aligned with Total Profit

## Important Insight
Average Order Value is not reliable at product level.

Reason:
Product filters the Sales table but does not directly filter the Orders table, causing Order Count to remain unchanged and leading to misleading results.

This highlights the importance of filter context and model relationships.

## Outcome
- foundational measures were transformed into meaningful business KPIs
- measures behave consistently across valid contexts
- early business insights can be extracted from the model
- groundwork established for advanced DAX techniques in the next phase
