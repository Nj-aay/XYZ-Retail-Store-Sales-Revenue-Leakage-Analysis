# XYZ-Retail-Store-Sales-Revenue-Leakage-AnalysisProject Overview

XYZ Retail Store is a fictional retail business operating across USA and Canada.

The business was making sales, but management did not have a clear picture of what was happening to the money after a sale was made.

A customer could place an order, return the product, receive a refund, or return an item that eventually had to be thrown away.

So the main question behind this project was:

We are making sales, but where is the money going?

I built a Power BI reporting system that connects sales, customers, products, shipments, returns, refunds, and warehouse activity in one place.

Business Questions

The dashboard was built to answer questions such as:

How much are we selling?
Which branch generates more sales?
Which products sell the most?
How many units are being returned?
Why are customers returning products?
How much money is being refunded?
Which branch has more waste?
Which products have high return activity?
Can the report be refreshed when new data arrives?
Data Sources

The project uses data from several business areas:

Sales
Orders
Order Items
Warehouse
Inventory Movements
Warehouse Adjustments
Shipping
Shipments
Returns
Refunds
Master Data
Products
Customers
Branches
Data Cleaning

The raw data was cleaned using Excel Power Query before being loaded into Power BI.

Some of the cleaning included:

Removing duplicate Order IDs
Cleaning inconsistent text
Standardising data types
Cleaning dates
Handling missing values
Replacing unknown warehouse information with Unknown
Checking product and customer IDs
Cleaning quantities and sales values
Checking return and refund records
Preserving negative inventory movements where they represented stock leaving the warehouse

I kept useful records instead of simply deleting rows because they contained missing or unusual values.

Power BI Data Model

The main relationships were built around:

Customers
    ↓
Orders
    ↓
Order Items
    ↓
Products

And:

Orders
   ↓
Returns
   ↓
Refunds

Warehouse activity was connected to Products and Branches.

This allowed the dashboard to connect what happened during a sale with what happened afterwards.

Dashboard Pages
1. Executive Overview

A high-level view of the business.

Includes:

Total Net Sales
Total Orders
Units Sold
Total Refunds
Trashed Units
Sales by Branch
Top Products
Sales trends
Returns trends
2. Sales Performance

Looks at where sales are coming from.

Includes:

Sales by Customer Type
Sales by Product
Orders by Customer Type
Units Sold by Customer Type
Sales by Branch

Interactive filters allow users to analyse the report by:

Branch
Customer Type
Product
3. Revenue Leakage

Focuses on what happens after a sale.

Includes:

Refunds by Refund Status
Refunds by Branch
Returned Units by Return Reason
Trashed Units by Branch

The purpose is to identify areas where revenue or inventory is being lost.

4. Returns Analysis

Looks deeper into customer returns.

Includes:

Returns by Product
Resellable vs Trashed Returns
Returns by Customer Type
Return Rate by Product
5. Warehouse & Waste

Looks at inventory movement and waste.

Includes:

Trashed Units by Product
Trashed Units by Branch
Inventory Movement by Movement Type
Warehouse Adjustments by Reason
6. Product Profitability

A profitability section was included in the dashboard structure.

However, the available product data did not contain a reliable product-cost field. Because of this, profit figures were not treated as reliable.

A proper product-cost field would need to be added before using this section for financial decisions.

Key Measures

Some of the DAX measures created include:

Total Net Sales =
SUM('stg order_items'[Net sales])
Total Gross Sales =
SUM('stg order_items'[GrossLineSales])
Total Orders =
DISTINCTCOUNT('stg orders'[OrderID])
Units Sold =
SUM('stg order_items'[Quantity])
Total Refunds =
SUM('stg refunds'[RefundAmount])
Returned Units =
SUM('stg returns'[Quantity])
Return Rate =
DIVIDE([Returned Units], [Units Sold], 0)
Trashed Units =
ABS(
    CALCULATE(
        SUM('stg inventory_movements'[Quantity]),
        'stg inventory_movements'[MovementType] = "Trashed"
    )
)
Automation

The goal was to build more than a static dashboard.

The reporting workflow is:

Raw CSV Data
     ↓
Power Query
     ↓
Cleaned Data
     ↓
Power BI Data Model
     ↓
DAX Measures
     ↓
Interactive Dashboard
     ↓
Refresh with New Data

The dashboard was tested by refreshing the model and checking that filters and visuals responded to the underlying data.

The next stage of the automation test is to introduce new September–December transactions and confirm that they flow through the existing pipeline after refresh.

Challenges

This project also involved fixing real modelling and data issues.

Some examples were:

Incorrect table relationships
Incorrect relationship cardinalities
Blank categories in visuals
Refunds not filtering correctly by branch
Missing information required for reliable profit calculations
Data that could not be safely analysed without additional fields

These issues reinforced an important part of data analysis:

A dashboard is only useful when the numbers behind it can be trusted.

Tools Used
Excel
Power Query
Power BI
DAX

What This Project Shows

This project demonstrates my ability to:

Clean messy business data
Work with multiple related datasets
Build a Power BI data model
Create DAX measures
Build interactive dashboards
Investigate data-quality problems
Think about revenue beyond just sales
Design a refreshable reporting workflow
Communicate findings in business terms
Project Goal

The final goal was simple:

Help a retail business understand not only how much it sells, but what happens to that money afterwards.

Sales → Returns → Refunds → Waste

That is the story this dashboard was built to tell.
