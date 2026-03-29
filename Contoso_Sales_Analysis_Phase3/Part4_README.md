# Phase 3 — Part 4: Ranking & Time Foundations

## Objective
Extend the analytical model by introducing ranking logic and building a foundation for time-based analysis.

## Measures Created

### Ranking Measures

- **Product Rank**  
  `RANKX(ALL(Product_Lookup[ProductName]), [Total Sales], , DESC)`  
  Purpose: rank products based on total sales across the entire dataset

- **Country Rank**  
  `RANKX(ALL(Store_Lookup[CountryName]), [Total Sales], , DESC)`  
  Purpose: rank countries by total sales contribution

- **Category Rank**  
  `RANKX(ALL(Product_Lookup[CategoryName]), [Total Sales], , DESC)`  
  Purpose: rank product categories by total sales

---

## Key Concepts Practiced
- ranking measures using RANKX
- difference between global ranking and filtered (local) ranking
- using ALL to remove filters for consistent comparison
- understanding how ranking changes with context

---

## Date Foundations

Basic date measures were created to support time-based analysis:

- **Today Date**  
  `TODAY()`

- **Current DateTime**  
  `NOW()`

- **Current Year**  
  `YEAR(TODAY())`

- **Current Month**  
  `MONTH(TODAY())`

- **Current Day**  
  `DAY(TODAY())`

Purpose: establish a base for time intelligence calculations in the next phase.

---

## Date Table Validation
The Date table was validated to ensure correct behaviour:

- sales grouped correctly by Year and Month
- month sorting fixed using MonthNumber
- no missing or zero-value periods
- total sales consistent across all views (~$218M)

---

## Validation
Measures were tested using PivotTables:
- confirmed correct ranking across products, categories, and countries
- ensured rankings remain stable when expected
- verified correct behaviour under different filters

---

## Key Learning
- RANKX enables comparison across entities within the dataset
- ALL is essential for global ranking logic
- rankings are context-dependent and change with filters
- a properly structured Date table is critical for reliable time analysis

---

## Outcome
- ranking logic successfully implemented across key dimensions
- strong understanding of context-aware comparisons developed
- date structure validated and prepared for time intelligence
- model ready for advanced time-based analysis in the next phase
