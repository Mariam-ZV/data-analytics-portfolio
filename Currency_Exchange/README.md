# Contoso Retail Data Project — Mini Project 07  
## Currency Exchange — Time-Series Validation & Pivot/Unpivot Practice

### Objective
Prepare a clean **currency exchange fact table** for the Contoso Retail data model while practicing **Pivot and Unpivot transformations in Power Query**.

This dataset contains **daily exchange rates between currency pairs**, which will later support **multi-currency financial analysis** by allowing sales values to be converted between currencies.

---

## Dataset

Source: Contoso Retail CSV Dataset (100k version)  
Table used: `currencyexchange.csv`

Rows: **100,450**  
Columns: **4**

| Column | Data Type | Description |
|------|------|------|
| Date | Date | Exchange rate date |
| Exchange | Decimal | Exchange rate value |
| FromCurrency | Text | Source currency |
| ToCurrency | Text | Target currency |

---

## Initial Data Audit

After importing the dataset into **Power Query**:

- Column data types were verified and confirmed correct
- Row count validated: **100,450 rows**
- Column quality check showed:
  - **100% Valid values**
  - **0 Errors**
  - **0 Empty values**

The dataset structure was confirmed to be complete and consistent.

---

## Date Structure Validation

Column profiling showed:

- Minimum Date: **01/01/2016**
- Maximum Date: **31/12/2026**
- Distinct Dates: **4,018**

This confirms the dataset contains a **multi-year daily time series of currency exchange rates**.

Multiple currency pairs exist for each date, which is expected for a financial exchange dataset.

---

## Currency Relationship Validation

Distinct values were checked for the currency columns.

| Column | Distinct Values |
|------|------|
| FromCurrency | 5 |
| ToCurrency | 5 |

The dataset contains **five currencies**, and the same currency set appears in both columns, confirming consistent currency relationships.

---

## Unpivot Transformation (Normalization Practice)

The columns **FromCurrency** and **ToCurrency** were unpivoted to demonstrate normalization techniques.

Transformation:

```
Transform → Unpivot Columns
```

Resulting structure:

| Date | Exchange | Attribute | Value |

This operation converts categorical columns into rows, expanding the dataset from **100,450 rows to 200,900 rows**.

This step illustrates how wide data can be normalized into a **long analytical structure**.

---

## Pivot Reconstruction

To reconstruct the original column structure:

1. A **temporary Index column** was added to guarantee row uniqueness during pivoting.
2. The **Attribute column was pivoted** to recreate `FromCurrency` and `ToCurrency`.
3. Missing values were reconstructed using **Fill Down** and **Fill Up**.
4. Duplicate rows created during the reconstruction were removed.
5. The temporary **Index column was deleted**.

This restored the dataset to its correct structure and original row count.

Final row count after reconstruction: **100,450**

---

## Final Data Validation

The final dataset was validated to confirm structural integrity.

Checks performed:

- Duplicate check across  
  `Date`, `Exchange`, `FromCurrency`, `ToCurrency`
- Currency consistency verification
- Logical validation confirming that:

```
FromCurrency = ToCurrency → Exchange = 1
```

Example:

| FromCurrency | ToCurrency | Exchange |
|------|------|------|
| AUD | AUD | 1 |
| USD | USD | 1 |

All validation checks passed successfully.

---

## Final Structure

The cleaned table used for modelling:

| Date | Exchange | FromCurrency | ToCurrency |

Rows: **100,450**  
Errors: **0**  
Empty values: **0**

---

## Skills Practiced

- Power Query data auditing
- Column profiling and validation
- Pivot / Unpivot transformations
- Row reconstruction techniques
- Duplicate detection and validation
- Financial time-series data preparation

---

## Role in the Contoso Data Model

The **Currency_Exchange table** functions as a **time-series reference fact table** used for **currency conversion in financial analysis**, enabling sales data recorded in different currencies to be compared consistently across markets.
