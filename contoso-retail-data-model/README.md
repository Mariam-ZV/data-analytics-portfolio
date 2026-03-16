# Contoso Retail Analytics — Phase 2: Data Modelling (Power Pivot)

## Project Overview
This project is part of a larger data analytics portfolio based on the Contoso Retail dataset. After completing Phase 1 (data preparation using Power Query), the cleaned datasets were loaded into Excel’s Power Pivot data model to construct a structured analytical schema.

The goal of this phase was to design a reliable data model that supports analytical queries, reporting, and future dashboard development.

## Dataset Structure
The model consists of 8 tables prepared during the data cleaning phase:

**Dimension Tables**
- Customer_Lookup
- Product_Lookup
- Store_Lookup
- Date_Lookup

**Fact Tables**
- Orders
- Order_Rows
- Sales
- Currency_Exchange

Dimension tables provide descriptive attributes used to analyse business activity, while fact tables store transactional and measurable data.

## Data Model Design
A **star schema** was implemented in Power Pivot.

Dimension tables were connected to fact tables using one-to-many relationships, ensuring that filtering flows from descriptive dimensions to transactional data.

Relationships created in the model:

Date_Lookup[Date] → Orders[OrderDate]  
Date_Lookup[Date] → Sales[OrderDate]  
Date_Lookup[Date] → Currency_Exchange[Date]

Customer_Lookup[CustomerKey] → Orders[CustomerKey]  
Customer_Lookup[CustomerKey] → Sales[CustomerKey]

Store_Lookup[StoreKey] → Orders[StoreKey]  
Store_Lookup[StoreKey] → Sales[StoreKey]

Product_Lookup[ProductKey] → Order_Rows[ProductKey]  
Product_Lookup[ProductKey] → Sales[ProductKey]

All relationships were validated to ensure correct cardinality (1:*) and proper filtering behaviour.

## Key Concepts Applied
This modelling phase demonstrates several important business intelligence concepts:

- Star schema design
- Fact vs dimension tables
- One-to-many relationships
- Dimensional filtering
- Calendar dimension modelling
- Analytical data modelling in Excel Power Pivot

## Outcome
The result is a fully connected analytical data model that supports multidimensional analysis across customers, products, stores, and time.

This model prepares the dataset for the next stage of the project, which includes:

- DAX calculations
- KPI development
- pivot-based analysis
- analytical dashboard creation

## Tools Used
- Microsoft Excel
- Power Query
- Power Pivot
- GitHub (portfolio documentation)
