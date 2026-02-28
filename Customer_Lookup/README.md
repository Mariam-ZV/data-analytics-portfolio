---

## Contoso Retail Data Project — Mini Project 01  
### Phase 1: Customer Lookup (Power Query Text Transformation)

**Objective**  
Prepare a clean, structured Customer lookup table using Power Query text tools and professional data preparation practices. The focus was on improving readability, consistency, and analytical usability without altering key identifiers.

**Dataset**  
Source: Contoso Retail CSV Dataset (100k version)  
Tables included in the wider project: Customer, Product, Store, Date, Orders, OrderRows, Sales, CurrencyExchange.

**Workflow Steps**

### Import & Data Audit
- Imported Customer.csv into Power Query.
- Renamed query to `Customer_Lookup`.
- Removed auto-detected data types and set types manually.
- Enabled Column Quality, Column Distribution and Column Profile.
- Switched profiling to entire dataset for accurate validation.

### Text Cleanup
- Applied Trim and Clean functions across all text columns.
- Standardised casing for name-related fields.

### Derived Columns
- Created `FullName` by merging GivenName and Surname.
- Extracted `HouseNumber` from StreetAddress.
- Extracted `StreetName` from StreetAddress.
- Replaced non-numeric conversion errors in HouseNumber with null values.

### Schema Organisation
- Reordered columns logically (keys, names, demographics, address, geography).
- Renamed Applied Steps for clarity and maintainability.

**Result**  
The Customer_Lookup table is now clean, structured, and ready for integration into a relational data model.

**Next Phase**  
Additional lookup tables will be prepared before building relationships and applying DAX analysis.
