# Contoso Retail Project — Phase 3: DAX Analysis & Business Insights

## Overview
This phase focuses on building analytical capabilities using DAX within a structured star schema model. The objective was to move beyond basic reporting and develop dynamic, context-aware measures that reflect real business performance.

The result is a fully validated analytical model capable of supporting decision-making, performance tracking, and time-based analysis.

---

## Key Areas Covered

### 1. Foundation Measures
Established core metrics directly from the Sales fact table:
- Total Sales
- Total Cost
- Total Profit
- Total Quantity
- Order Count
- Distinct Customers
- Products Sold

Focus:
Accurate business logic using row-level calculations (Quantity × Price/Cost) and correct aggregation techniques.

---

### 2. KPI Development
Transformed raw measures into meaningful business indicators:
- Profit Margin %
- Average Order Value
- Average Quantity per Order

Introduced logic-based classification:
- Profit Status (Profitable vs Loss-Making)
- Sales Band (Low / Medium / High)

Focus:
Understanding how measures behave under different filter contexts and ensuring reliable KPI interpretation.

---

### 3. Advanced DAX (Context Control)
Built context-aware measures using:
- CALCULATE
- FILTER
- ALL

Examples:
- Sales by specific country (Sales UK)
- % of Total Sales
- High Value Sales and contribution %

Focus:
Controlling filter context to produce meaningful and accurate comparisons across the business.

---

### 4. Ranking & Comparative Analysis
Implemented ranking logic across key dimensions:
- Product Rank
- Country Rank
- Category Rank

Focus:
Using RANKX and ALL to compare performance across the full dataset while understanding context-dependent behaviour.

---

### 5. Time Intelligence & Trend Analysis
Developed time-based measures:
- Year-to-Date (YTD)
- Month-to-Date (MTD)
- Quarter-to-Date (QTD)
- Same Period Last Year (LY)
- % Growth vs LY

Focus:
Analysing performance over time and enabling year-over-year comparison.

---

## Validation Approach
All measures were systematically validated using PivotTables:

- tested across multiple dimensions (country, product, category, time)
- checked for logical consistency and accuracy
- verified aggregation behaviour and context interactions
- confirmed correct time-based calculations

Dedicated validation sheets were created to ensure reliability:
- YTD validation
- MTD validation
- Year-over-Year validation
- Final consolidated validation

---

## Key Insights

- The business operates with consistently positive profit margins
- High-value transactions contribute significantly to total revenue
- Sales performance varies by region, indicating different market behaviours
- Time-based analysis reveals fluctuations across periods and categories
- Model structure and filter context directly impact analytical results

---

## Key Learnings

- DAX is fundamentally about controlling filter context, not just writing formulas
- Business logic must be accurately reflected in calculations
- Relationships between tables directly influence measure behaviour
- Validation is essential to ensure reliable analysis
- Small modelling decisions can significantly impact results

---

## Outcome

- Fully functional analytical data model (star schema)
- Core and advanced DAX measures implemented
- KPI layer established for business reporting
- Time intelligence successfully integrated
- Model validated and ready for dashboard development

---

## Next Step
Phase 4 will focus on:
- building interactive dashboards
- applying data visualisation best practices
- translating analysis into clear business storytelling
