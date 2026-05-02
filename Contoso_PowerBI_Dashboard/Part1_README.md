# 📊 Contoso Retail — Executive Summary Dashboard

## 📌 Overview
This page provides a high-level snapshot of business performance, focusing on revenue, profitability, and operational activity. It is designed for quick decision-making by summarising key metrics and highlighting short-term trends.

---

## 🎯 Purpose of This Page

The Executive Summary answers the following business questions:

- How is the business performing overall?
- Are sales, profit, and orders increasing or decreasing?
- What is the short-term (month-over-month) trend?
- Which product categories are driving revenue?
- Which products contribute most to sales and profit?

---

## 📊 Key Metrics (Top KPIs)

- **Total Sales** → Overall revenue generated  
- **Total Profit** → Net profit after costs  
- **Total Orders** → Number of transactions  
- **Total Customers** → Distinct customers  

These KPIs dynamically update based on filters and provide a quick overview of business scale and performance.

---

## 📈 Monthly Trend Analysis

**Visual: Line Chart (Monthly Sales Trend)**  
- Displays sales performance over time using `YearMonth`  
- Helps identify trends, seasonality, and anomalies  
- Includes a trend line for direction analysis  

---

## 📌 Category Performance

**Visual: Bar Chart (Sales by Category)**  
- Shows total sales across product categories  
- Highlights top-performing and underperforming segments  
- Enables quick comparison of category contribution  

---

## 🏆 Product Performance

**Visual: Table (Top Products by Sales)**  
- Lists highest-performing products  
- Includes:  
  - Orders  
  - Sales  
  - Profit  
- Helps identify key revenue drivers  

---

## 📉 Month-over-Month KPIs (Time Intelligence)

Three KPI visuals were created to analyse short-term performance:

### 💰 Monthly Sales
- Current Month Sales  
- Compared against Previous Month (`Sales PM`)  
- Displays % change (MoM)  

### 📈 Monthly Orders
- Current Month Orders  
- Compared against Previous Month (`Orders PM`)  
- Displays % change (MoM)  

### 💸 Monthly Profit
- Current Month Profit  
- Compared against Previous Month (`Profit PM`)  
- Displays % change (MoM)  

---

## ⚙️ DAX Measures Used

### Previous Month Measures
- `Sales PM = CALCULATE([Total Sales], DATEADD(Date_Lookup[Date], -1, MONTH))`  
- `Profit PM = CALCULATE([Total Profit], DATEADD(Date_Lookup[Date], -1, MONTH))`  
- `Orders PM = CALCULATE([Order Count], DATEADD(Date_Lookup[Date], -1, MONTH))`  

### Month-over-Month %
- `Sales MoM % = DIVIDE([Total Sales] - [Sales PM], [Sales PM])`  
- `Profit MoM % = DIVIDE([Total Profit] - [Profit PM], [Profit PM])`  
- `Orders MoM % = DIVIDE([Order Count] - [Orders PM], [Orders PM])`  

---

## ⚠️ Data Handling

- KPI visuals required filtering to exclude blank values:  
  - `Total Sales is not blank`  
  - `Sales PM is not blank`  
  - Same logic applied for Profit and Orders  

This ensures accurate comparison and prevents KPI errors.

---

## 🔍 Key Insight from This Page

- Orders increased month-over-month  
- Sales decreased  
- Profit decreased  

👉 This indicates:  
- Lower average order value  
- Possible discounting or shift to lower-margin products  
- Potential margin compression  

---

## 🧠 Business Interpretation

Despite higher demand (more orders), the business is generating less revenue and profit. This suggests inefficiencies in pricing, product mix, or cost management.

---

## 🚀 Next Steps (Further Analysis)

This page raises key follow-up questions:

- Which categories or products are reducing profitability?  
- Is the decline driven by specific regions or customers?  
- Are discounts or promotions affecting margins?  

Subsequent pages will explore:
- Product-level profitability  
- Customer segmentation  
- Regional performance  
