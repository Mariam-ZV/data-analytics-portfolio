# Contoso Retail Data Project — Mini Project 03  
## Phase 1: Orders Date & Time Tools

### Objective
Prepare the Orders fact table using Power Query with a focus on date transformations, operational metrics, and data validation.

---

## Dataset
Source: Contoso Retail CSV Dataset (100k version)  
Table used: Orders  
Rows: 93,470  
Load type: Connection only (prepared for modelling)

---

## Key Transformations

### Data Validation
- Verified delivery dates occur after order dates
- Created **Delivery_Check** flag for data quality monitoring

### Operational Metric
- **Delivery_Days** = number of days between OrderDate and DeliveryDate

### Date Feature Engineering
Extracted reporting features from OrderDate:
- Order_Year
- Order_Quarter
- Order_Month
- Order_Month_Name
- Order_Weekday_Number
- Order_Weekday_Name

### Calendar Reporting Field
- **Order_YearMonth** created for monthly reporting

### Delivery Performance Segmentation
Orders categorized based on delivery duration:
- Fast (0–2 days)
- Normal (3–5 days)
- Slow (6+ days)

---

## Outcome
A clean **Orders fact table** with validated delivery logic and enriched time features, ready for data modelling and analysis.
