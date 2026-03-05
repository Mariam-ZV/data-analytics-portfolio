# Contoso Retail Data Project — Mini Project 02  
## Phase 2: Product Lookup (Numeric & Conditional Segmentation)

### Objective
Build a clean and analysis-ready Product Lookup table using Power Query, focusing on numeric validation, indexing, and conditional business segmentation.

---

## Dataset
Source: Contoso Retail CSV Dataset (100k version)  
Table used: Product  
Rows: 2,517  
Load type: Connection only (prepared for modelling)

---

## Key Transformations

### Numeric Calculations
- **Unit_Profit** = Price − Cost  
- **Margin_Ratio** = Unit_Profit ÷ Price (rounded to 4 decimals)

### Commercial Validation
- **Price_vs_Cost_Check** confirms Price ≥ Cost for all products  
- No loss-making products detected

### Indexing
- **Product_Index** created from 1 to 2,517 for structural control

### Conditional Segmentation
- **Margin_Category** (Low / Medium / High)
- **Risk_Flag** (flags Low margin products)
- **Value_Tier** (High Value if Price > 1000) → 154 products
- **Profit_Tier** (High Profit if Unit_Profit > 500) → 212 products

---

## 3 Key Insights

1. All products are priced above cost, indicating commercially consistent pricing.
2. Only ~6% of products fall into the High Value category, suggesting a small premium segment.
3. High Profit products (212) exceed High Value products (154), meaning profitability is not driven by price alone.

---

## 3 Risks

1. Missing weight data may affect logistics or shipping cost analysis.
2. Margin thresholds are analyst-defined and may require business alignment.
3. Tier classifications may need adjustment based on market strategy.

---

## 3 Opportunities

1. Extend analysis by aggregating margin tiers by Category and SubCategory.
2. Model discount scenarios to test margin sensitivity.
3. Join with Sales/Orders tables to evaluate profit contribution impact.

---

## Skills Demonstrated

- Power Query data import and audit
- Data typing and validation
- Numeric transformations
- Conditional logic and segmentation
- Index creation
- Structured transformation workflow
