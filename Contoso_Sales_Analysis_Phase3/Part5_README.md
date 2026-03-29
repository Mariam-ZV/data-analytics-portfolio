# Phase 3 — Part 5: Time Intelligence & Final Validation

## Objective
Complete the model with time-based analysis and validate all measures to ensure accuracy before moving to visualisation.

## Business Question
How is the business performing over time, and how do current results compare with previous periods?

## Measures Created

### Time Intelligence Measures

- **Total Sales YTD**  
  Purpose: cumulative sales from the start of the year to the current date

- **Total Sales MTD**  
  Purpose: cumulative sales from the start of the month to the current date

- **Total Sales QTD**  
  Purpose: cumulative sales from the start of the quarter to the current date

---

### Previous Period Comparison

- **Total Sales LY**  
  Purpose: calculate sales for the same period in the previous year using time intelligence

- **Total Sales LY (DATEADD)**  
  Purpose: alternative LY calculation using DATEADD for validation

---

### Performance Comparison

- **Sales vs LY**  
  Purpose: measure absolute difference between current and last year’s sales

- **% Growth vs LY**  
  `DIVIDE([Sales vs LY], [Total Sales LY])`  
  Purpose: calculate percentage change vs previous year

---

## Key Concepts Practiced
- time intelligence functions (YTD, MTD, QTD)
- SAMEPERIODLASTYEAR vs DATEADD
- dependency on proper date context
- combining time calculations with existing measures
- safe division using DIVIDE()

---

## Validation

All measures were tested using PivotTables across:
- Year
- Month
- Category
- Country

Checks performed:
- correct accumulation behaviour (YTD, MTD, QTD)
- correct reset at period boundaries (month, quarter)
- consistency between LY and DATEADD results
- no unexpected blanks or incorrect growth values

---

## Validation Sheets

- **Validation_YTD**  
  confirmed cumulative yearly totals increase correctly

- **Validation_MTD**  
  confirmed monthly accumulation resets correctly

- **Validation_LY**  
  validated year-over-year comparisons and growth calculations

- **Final_Validation**  
  consolidated key measures to verify overall model consistency

---

## Key Insights
- time intelligence calculations require a valid date context
- without Year or Date filters, comparison measures can return misleading results
- growth varies across categories, countries, and time periods
- model structure directly impacts analytical outcomes

---

## Outcome
- full time intelligence layer implemented
- year-over-year comparison successfully established
- all measures validated and confirmed reliable
- model ready for dashboard development and business storytelling
