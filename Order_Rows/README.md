# Contoso Retail Data Project — Mini Project 04
## Order Rows (Fact Table Preparation with Power Query)

### Objective
Prepare the **Order_Rows** transaction table using Power Query by performing structural validation, data integrity checks, and key relationship validation.  
The goal of this step is to ensure the dataset is **clean, logically consistent, and ready for modelling in a star schema**.

This mini project focuses on practicing **Power Query data validation techniques and Merge (Join) operations**.

---

# Dataset
Source: Contoso Retail Dataset (CSV version)

File used:
```
orderrows.csv
```

Dataset structure:

| Attribute | Value |
|---|---|
Rows | 223,974 |
Columns | 7 |

Columns detected on import:

```
OrderKey
LineNumber
ProductKey
Quantity
UnitPrice
NetPrice
UnitCost
```

Each row represents **one product line within an order**.

---

# Power Query Preparation Steps

## 1. Initial Import and Auditing
The dataset was imported into **Power Query Editor**.

Initial validation steps included:

- Enabled **Column Profiling based on entire dataset**
- Renamed query from `orderrows` → **Order_Rows**
- Verified **data types** for all columns

| Column | Data Type |
|---|---|
OrderKey | Whole Number |
LineNumber | Whole Number |
ProductKey | Whole Number |
Quantity | Whole Number |
UnitPrice | Decimal Number |
NetPrice | Decimal Number |
UnitCost | Decimal Number |

Column Quality check confirmed:

```
100% Valid
0% Errors
```

---

## 2. Structural Validation
The `OrderKey` column was analyzed using **Column Distribution**.

Results:

| Metric | Value |
|---|---|
Distinct OrderKey values | 93,470 |
Unique OrderKey values | 32,399 |

Interpretation:

- Orders can contain **multiple product lines**
- Therefore the same `OrderKey` appears multiple times
- This confirms the dataset behaves like a **true order-line transaction table**

Each row represents **one product purchased within an order**.

---

## 3. Row Uniqueness Validation
To confirm row-level uniqueness, the following composite key was tested:

```
OrderKey + LineNumber
```

Power Query test:

```
Home → Remove Rows → Remove Duplicates
```

Result:

```
0 rows removed
```

Conclusion:

- Each row is uniquely identified by **OrderKey + LineNumber**
- No duplicate order-line records exist

---

## 4. Numeric Validation
A temporary validation column was created to test pricing logic.

Formula used:

```
Expected_NetPrice = UnitPrice × Quantity
```

Observation:

- `NetPrice` does not equal `UnitPrice × Quantity`

Interpretation:

The dataset likely stores:

| Column | Meaning |
|---|---|
UnitPrice | List price per unit |
NetPrice | Actual selling price per unit (after discount) |

The temporary validation column was removed after testing to maintain the original structure.

---

## 5. Referential Integrity Check (Merge Validation)

A **Power Query Merge** was performed to verify that all product keys referenced in the fact table exist in the product dimension.

Merge configuration:

```
Order_Rows.ProductKey
Product_Lookup.ProductKey
Join type: Left Outer
```

Result:

```
223,974 of 223,974 rows matched
```

Conclusion:

- Every `ProductKey` in `Order_Rows` exists in `Product_Lookup`
- No orphan product references were detected

After validation, the merge steps were removed to preserve proper **star schema design**.

---

## 6. Numeric Sanity Check
Final validation of numeric columns confirmed:

| Column | Errors | Empty | Zero |
|---|---|---|---|
Quantity | 0 | 0 | 0 |
UnitPrice | 0 | 0 | 0 |
NetPrice | 0 | 0 | 0 |
UnitCost | 0 | 0 | 0 |

This confirms:

- No missing values
- No corrupted numeric data
- No suspicious zero values

---

# Final Query Configuration

The cleaned table was loaded as:

```
Connection Only
```

This prepares the dataset for later use in:

- Power Pivot
- Data modelling
- Analytical calculations

---

# Result
The **Order_Rows** table is now:

- Structurally validated
- Free of duplicates
- Numerically consistent
- Referentially validated against the Product table
- Ready for integration into a **star schema data model**

---

# Skills Demonstrated

Power Query techniques practiced:

- Data auditing and profiling
- Structural validation
- Composite key validation
- Numeric data verification
- Power Query **Merge (Join) operations**
- Referential integrity checks
- Clean query preparation for data modelling

---

# Project Context

This mini project is part of a larger **Contoso Retail Data Analytics Portfolio Project**, where multiple CSV datasets are prepared and later combined into a full analytical data model.

Completed preparation tables so far:

```
Customer_Lookup
Product_Lookup
Orders
Order_Rows
```

These tables will later be connected using relationships to build a **Power Pivot analytical model**.
