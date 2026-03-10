# Contoso Retail Data Project — Mini Project 05  
## Sales Fact Table (Power Query)

### Objective
Prepare and validate the **Sales transactional fact table** using Power Query.  
The goal was to audit the dataset, verify pricing logic, test profitability behaviour, and practise aggregation using **Group By**, ensuring the table is clean and ready for data modelling.

---

## Dataset
Source: Contoso Retail Dataset (CSV)

Table: **Sales**

Rows: **223,974**  
Columns: **13**

---

## Initial Structure

The Sales table contains the following fields:

| Column | Description |
|------|-------------|
| OrderKey | Unique identifier of the order |
| LineNumber | Position of the product within the order |
| OrderDate | Date when the order was placed |
| DeliveryDate | Date when the order was delivered |
| CustomerKey | Foreign key linking to the customer dimension |
| StoreKey | Foreign key linking to the store dimension |
| ProductKey | Foreign key linking to the product dimension |
| Quantity | Number of units sold |
| UnitPrice | List price per unit |
| NetPrice | Actual transaction revenue |
| UnitCost | Cost per unit |
| CurrencyCode | Transaction currency |
| ExchangeRate | Currency conversion rate |

---

## 1. Initial Data Audit

Basic data profiling was performed immediately after importing the dataset.

Checks included:

- Row count verification
- Column profiling
- Column distribution
- Data type inspection

Results:

- **223,974 rows**
- **100% valid values**
- **0 errors**
- **0 empty values**

This confirms the dataset is structurally clean.

---

## 2. Fact Table Grain Validation

The grain of the dataset was verified by checking the uniqueness of:

```
OrderKey + LineNumber
```

Result:

The row count remained unchanged after duplicate testing, confirming that:

**One row represents one product line within an order.**

This establishes the correct transactional grain for the fact table.

---

## 3. Pricing Logic Validation

To understand how revenue is stored in the dataset, validation columns were created.

### Expected Net Price

```
Expected_NetPrice = Quantity × UnitPrice
```

Observation:

Expected values **did not always match NetPrice**.

This indicates that **NetPrice reflects discounted transaction revenue rather than gross list price**.

### Actual Unit Net Price

```
Actual_Unit_NetPrice = NetPrice ÷ Quantity
```

Observation:

Actual selling price per unit is often **lower than UnitPrice**, confirming the presence of **discounted sales transactions**.

---

## 4. Profit Validation

Profitability checks were performed using two validation columns.

### Unit Profit

```
Unit_Profit = UnitPrice − UnitCost
```

Result:

All values were **positive**, indicating products are generally sold above cost.

### Transaction Profit

```
Transaction_Profit = NetPrice − (Quantity × UnitCost)
```

Observation:

Some transactions produced **negative profit values**.

This occurs because **discounted NetPrice can occasionally fall below total cost**, which is realistic in retail scenarios such as promotions or clearance pricing.

---

## 5. Currency Validation

Currency-related fields were inspected.

Distinct currencies observed:

- AUD
- CAD
- EUROPE
- GBP
- USD

ExchangeRate range:

- **Min:** 0.67253  
- **Max:** 1.7253

These values fall within a reasonable currency conversion range.

---

## 6. Aggregation Validation (Group By Practice)

A reference query **Sales_Product_Summary** was created to practise aggregation.

Grouping column:

```
ProductKey
```

Metrics calculated:

- **Transaction_Count** (number of sales rows)
- **Total_Quantity** (sum of Quantity)
- **Total_NetPrice** (sum of NetPrice)

Purpose:

To verify product-level totals and demonstrate aggregation logic similar to SQL `GROUP BY`.

The query was kept as **connection only** for validation purposes and not included in the final dataset.

---

## 7. Fact Table Integrity Check

Foreign keys were inspected to ensure compatibility with dimension tables.

Keys validated:

- OrderKey
- CustomerKey
- ProductKey
- StoreKey

Column profiling confirmed:

- **100% valid values**
- **0 errors**
- **0 empty values**

This confirms referential integrity for the fact table.

---

## 8. Final Cleanup

Temporary validation columns were removed:

- Expected_NetPrice
- Actual_Unit_NetPrice
- Unit_Profit
- Transaction_Profit

The final Sales table was restored to its original **13-column structure**, now fully validated and ready for data modelling.

---

## Final Result

A clean, validated **Sales fact table** prepared for use in:

- Power Pivot
- Data modelling
- Analytical reporting

This step also demonstrated practical use of:

- Power Query data auditing
- Business logic validation
- Profit analysis
- Currency checks
- Aggregation using Group By
