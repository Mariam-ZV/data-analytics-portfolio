# Contoso Retail Data Project — Mini Project 06  
## Store Lookup — Text Cleaning, Conditional Logic & Data Validation (Power Query)

### Objective
Prepare a clean **Store dimension table** using Power Query by applying text cleaning, handling missing values, creating business logic columns, and validating structural data integrity.  

The Store table represents physical and online store entities and will function as a **lookup (dimension) table** in the analytical data model.

---

# Dataset
Source: Contoso Retail CSV Dataset (100k version)  
Table used: **store.csv**

Rows: **74**

Load type: **Power Query – Connection only**

---

# Initial Data Audit

### Query Setup
The query was renamed from:

store → **Store_Lookup**

This follows dimensional modelling conventions where descriptive entity tables are labelled as lookup tables.

---

### Column Structure Validation

The dataset contains **11 columns**:

| Column | Data Type | Description |
|------|------|------|
| StoreKey | Whole Number | Unique store identifier |
| StoreCode | Whole Number | Internal store code |
| GeoAreaKey | Whole Number | Geographic lookup reference |
| CountryCode | Text | Country abbreviation |
| CountryName | Text | Country name |
| State | Text | Regional location |
| OpenDate | Date | Store opening date |
| CloseDate | Date | Store closing date |
| Description | Text | Store description |
| SquareMeters | Whole Number | Store size |
| Status | Text | Raw operational status |

All column types were validated in Power Query and confirmed to be correct.

---

### Row Count Validation

Using:

Transform → Count Rows

Total rows detected:

**74 stores**

This confirms the dataset loaded completely.

---

### Column Quality Audit

Column profiling was switched to **Entire Dataset** to ensure statistics reflect all rows.

Key findings:

| Column | Valid | Empty | Notes |
|------|------|------|------|
| CloseDate | ~22% | ~78% | Most stores still operating |
| SquareMeters | 99% | 1% | One missing value |
| Status | ~20% | ~80% | Many blank values |
| Other columns | 100% | 0% | No issues |

---

### Primary Key Validation

StoreKey column statistics:

Distinct values: **74**  
Unique values: **74**

This confirms **StoreKey is a valid primary key**.

---

# Data Transformations

## 1. Text Cleaning

Applied **Clean** and **Trim** to all text columns:

- CountryCode  
- CountryName  
- State  
- Description  
- Status  

Tools used:

Transform → Format → Clean  
Transform → Format → Trim  

Purpose:
- Remove hidden characters
- Remove leading and trailing spaces
- Standardise categorical text values

---

## 2. Replace Empty Strings with Null

The **Status column contained empty strings rather than true null values**.

Using:

Transform → Replace Values

Empty strings were replaced with **null values** to ensure correct data interpretation.

---

## 3. Create Analytical Store Status

The raw Status column contained inconsistent information.

A new column **Store_Status** was created using conditional logic based on the CloseDate field.

Logic applied:

- If CloseDate is null → **Open**
- Otherwise → **Closed**

This creates a reliable operational indicator for analytical reporting.

---

## 4. Date Validation

To verify chronological consistency, a validation column **Date_Check** was temporarily created.

Logic applied:

- If CloseDate is null → OK
- If CloseDate ≥ OpenDate → OK
- Otherwise → Error

No errors were detected, confirming **no invalid date relationships**.

The validation column was removed after verification.

---

## 5. Handling Missing Values

One row contained a missing value in **SquareMeters**.

Investigation revealed this row represents the **Online Store entity**:

- StoreKey = 999999  
- CountryName = Online  
- Description = Online Store  

Since online stores have no physical size, the null value was **retained intentionally**.

---

## 6. Remove Redundant Column

After deriving the analytical status column, the original **Status** column was removed to simplify the dimension table structure.

---

## 7. Final Column Structure

Columns were reordered to follow dimensional modelling best practices:

1. StoreKey  
2. StoreCode  
3. GeoAreaKey  
4. CountryCode  
5. CountryName  
6. State  
7. OpenDate  
8. CloseDate  
9. SquareMeters  
10. Description  
11. Store_Status  

---

# Final Validation

Final checks confirmed:

- No column errors
- StoreKey remains unique
- Store_Status contains only two categories:
  - Open
  - Closed

---

# Result

A **clean and validated Store dimension table** prepared for analytical modelling.

The table now contains:

- reliable operational status
- validated date relationships
- standardised text fields
- correct handling of online store entities

This table can now be safely joined with fact tables within the Contoso retail data model.

---

# Skills Practised

Power Query data preparation techniques:

- Text cleaning (Clean & Trim)
- Replacing empty strings with null values
- Conditional columns
- Data validation logic
- Missing value investigation
- Dimension table structuring
- Query transformation documentation
