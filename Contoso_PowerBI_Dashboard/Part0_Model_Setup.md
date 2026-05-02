# Phase 4 — Power BI Model Setup

## Importing Phase 3 Model into Power BI
I imported the Phase 3 Excel model directly into Power BI to preserve all existing work (tables, relationships, and measures).

**Path:**  
Blank Report → Import → Power Query, Power Pivot, Power View → Select Phase 3 Excel file → Open

This method brings in:
- All tables (already cleaned)
- The data model (relationships already built)
- All DAX measures

This avoids rebuilding the model from scratch and ensures consistency with previous work.

---

## Model View Organisation
The model was rearranged visually for clarity:

**Lookup (dimension) tables placed at the top:**
- Customer_Lookup
- Product_Lookup
- Store_Lookup
- Date_Lookup

**Fact tables placed at the bottom:**
- Sales
- Orders
- Order_Rows
- Currency_Exchange

This improves readability and reflects proper analytical structure.

---

## Data Model Structure (Schema Type)
This is not a pure star schema — but it is still correct.

**What the model is:**  
A multi-fact (constellation-style) model with shared dimensions

**Structure:**
- Shared dimension tables:
  - Customer_Lookup
  - Product_Lookup
  - Store_Lookup
  - Date_Lookup

- Multiple fact-like tables:
  - Sales (main fact)
  - Orders
  - Order_Rows

All fact tables share the same dimensions.

### Currency_Exchange
This is not a main fact table.

It is a:
- Supporting / auxiliary table

Used for:
- Currency conversion
- Time-based exchange rate lookup
- DAX calculations (not direct reporting)

Connected to:
- Date_Lookup

**Summary:**
Multi-fact model with shared dimensions + supporting exchange table

**Key takeaway:**
- Not a strict star schema
- More advanced than basic models
- Still clean and widely used in real-world BI

---

## Relationships in the Model

**Sales**
- Customer_Lookup (CustomerKey)
- Product_Lookup (ProductKey)
- Store_Lookup (StoreKey)
- Date_Lookup (OrderDate)

**Orders**
- Customer_Lookup (CustomerKey)
- Store_Lookup (StoreKey)
- Date_Lookup (OrderDate)

**Order_Rows**
- Orders (OrderKey)
- Product_Lookup (ProductKey)

**Currency_Exchange**
- Date_Lookup (Date)

Lookup tables filter fact tables (correct modelling practice).

---

## Measure Table Creation & Organisation

A dedicated Measure Table was created:

- All measures moved into one place
- Removed clutter from fact tables
- Improved usability during report building

---

## Measure Grouping (Display Folders)

Measures were organised into folders:
- Sales
- Profit
- Time Intelligence
- Ranking
- Segmentation
- Orders / Quantity
- Date

This improves navigation and keeps the model clean.

---

## Hiding Technical Columns (Best Practice)

Hidden fields:
- CustomerKey
- ProductKey
- StoreKey
- OrderKey
- Date keys (where not needed)

**Reason:**
- Prevents confusion
- Keeps report view clean
- Avoids misuse in visuals

---

## Data Formatting & Data Categories

### Formatting
- Date columns → shortened format
- Price / Cost → currency format
- Numeric fields validated

### Data Categories (Geospatial)

Assigned:
- City → City
- StateFull → State/Province
- CountryFull → Country
- Continent → Continent
- ZipCode → Postal Code
- Latitude → Latitude
- Longitude → Longitude

Not assigned:
- Codes (e.g., DE, BY)
- Partial addresses (Street, HouseNumber)

Only human-readable geography fields were categorised.

---

## Handling Missing Data

- Weight / WeightUnit contain blanks
- No changes applied

**Reason:**
- No errors present
- Not relevant to analysis
- Avoid unnecessary manipulation

---

## Hierarchies Creation

Hierarchies were created only in lookup tables.

### Geography Hierarchy
Continent → CountryFull → StateFull → City → (optional ZipCode)

### Date Hierarchy
Year → Quarter → Month → Date  
- Replaces auto date hierarchy  
- Uses Date_Lookup

### Product Hierarchy
CategoryName → SubCategoryName → ProductName  
- Brand excluded for simplicity

**Principle:**
Hierarchies are for drill-down analysis, not data storage

---

## Additional Modelling Decisions

- No hierarchies in fact tables
- Used Date_Lookup instead of Order_* fields
- Month sorted by MonthNumber
- Clear separation between:
  - Dimensions (lookup tables)
  - Facts (transaction tables)

---

## Final State

The model is:
- Structured (star-based)
- Clean (hidden fields, no clutter)
- Scalable (measure table + folders)
- Analysis-ready (hierarchies + categories)
- Aligned with best practices

This is a professional BI model setup.
