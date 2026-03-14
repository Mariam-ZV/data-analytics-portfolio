# Contoso Retail Data Project — Mini Project 08  
## Date Lookup — Calendar Dimension Validation (Power Query)

### Objective
Prepare and validate the **Date Lookup table** using Power Query to ensure it can function as a reliable **calendar dimension** in the Contoso Retail data model.

The goal of this mini project is to confirm that the calendar structure is complete, logically consistent, and suitable for building time-based hierarchies used in reporting and DAX analysis.

---

# Dataset
Source: Contoso Retail CSV Dataset (100k version)  
Table used: **date.csv**  

Rows: **4,018**  
Columns: **17**

Load type: **Connection Only (prepared for data modelling)**

---

# Key Validation Steps

## Step 1 — Structural Validation

### Part 1: Date Uniqueness Validation
To ensure the calendar table contains **one row per date**, duplicates were checked on the `Date` column.

Power Query action:
- Selected `Date`
- Applied **Remove Duplicates**

Result:
- No rows removed  
- Row count remained **4,018**

This confirms that each row represents a **unique calendar date**, which is required for a proper date dimension.

---

### Part 2: Date Range Validation

The `Date` column was inspected using **Column Profile (entire dataset)** to confirm the calendar coverage.

Results:

| Minimum Date | Maximum Date |
|---|---|
| 01/01/2016 | 31/12/2026 |

This confirms the dataset contains a **continuous multi-year calendar range** suitable for time-based analysis.

---

# Step 2 — Hierarchy Validation

This step verifies that the **Year → Quarter → Month hierarchy** behaves correctly.

---

### Part 1: Month Sorting Validation

The `Month` column was inspected to ensure the chronological order aligns with `MonthNumber`.

Observation:
- Rows appear in chronological order when browsing the dataset
- However, the filter dropdown lists months **alphabetically** because `Month` is stored as text

This behaviour is expected and will later be corrected in the data model by sorting:

```
Month → by MonthNumber
```

---

### Part 2: Quarter Structure Validation

The columns `Quarter`, `YearQuarter`, and `YearQuarterNumber` were validated by sorting `YearQuarterNumber`.

Example observation:

| Year | Quarter | YearQuarter | YearQuarterNumber |
|---|---|---|---|
| 2016 | Q1 | Q1-2016 | 8065 |

The quarter labels align correctly with their numeric sequence, confirming the quarter hierarchy is structurally consistent.

---

### Part 3: Year–Month Structure Validation

Monthly hierarchy columns were validated:

- `YearMonth`
- `YearMonthShort`
- `YearMonthNumber`
- `Month`
- `MonthNumber`

To confirm consistency, the dataset was filtered to:

```
Month = January
Year = 2016
```

Result:

`YearMonthNumber` remained **24193 for all rows**, confirming that the column acts as a stable numeric identifier for each Year–Month combination.

---

# Step 3 — Calendar Logic Validation

### Day-of-Week Validation

The dataset was filtered to **Monday** to validate weekday alignment.

Observed:

| DayOfWeek | DayOfWeekShort | DayOfWeekNumber |
|---|---|---|
| Monday | Mon | 2 |

The dataset uses the **Excel weekday numbering convention**:

| Day | Number |
|---|---|
| Sunday | 1 |
| Monday | 2 |
| Tuesday | 3 |
| Wednesday | 4 |
| Thursday | 5 |
| Friday | 6 |
| Saturday | 7 |

This structure is consistent and suitable for weekday analysis.

---

### Working Day Logic Validation

Weekend days were inspected to confirm working-day flags.

Observed:

| DayOfWeek | WorkingDay |
|---|---|
| Saturday | 0 |
| Sunday | 0 |

This confirms that weekends are correctly marked as **non-working days**.

The column `WorkingDayNumber` represents a **running index of working days within the calendar year**, which is used for business-day calculations.

---

# Final Structural Alignment

Columns were reordered to align with a logical **calendar hierarchy**:

```
DateKey
Date
Year
YearQuarter
YearQuarterNumber
Quarter
YearMonth
YearMonthShort
YearMonthNumber
Month
MonthShort
MonthNumber
DayOfWeek
DayOfWeekShort
DayOfWeekNumber
WorkingDay
WorkingDayNumber
```

This structure supports the typical analytical hierarchy:

```
Year
 → Quarter
      → Month
           → Day
```

---

# Final Power Query Steps

```
Source
Promoted Headers
Changed Type
Removed Date Duplicates (Validation)
Sorted YearQuarterNumber (Validation)
Reordered Columns (Hierarchy Alignment)
```

---

# Outcome

The **Date Lookup table** is now:

- Structurally validated
- Free of duplicate dates
- Chronologically consistent
- Ready for **Power Pivot relationships**
- Prepared for **time intelligence analysis using DAX**

This table will serve as the **calendar dimension** for the Contoso Retail data model.

---

# Next Phase

The project will now move to **Phase 2 — Data Modelling**, where relationships between lookup tables and fact tables will be created in **Power Pivot** before performing analytical calculations using **DAX**.
