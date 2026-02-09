 Retail Sales Performance Analysis – Power BI Dashboard
 Project Overview
This project analyzes the sales and profitability of a nationwide retail company operating across four regions (North, South, East, West). The business sells products across multiple categories such as Electronics, Fashion, and Groceries.

Senior management observed strong revenue growth but inconsistent profit margins across regions and products. This Power BI dashboard is designed to uncover performance gaps and support data-driven decisions for promotions, pricing, and inventory planning.

Objectives
Clean and validate raw sales data

Identify profitable and non-profitable products

Analyze regional and category-wise performance

Evaluate sales vs profit relationships

Support strategic decisions on promotions and discontinuation

 Dataset Description
1. Transactions (Fact Table)
TransactionID

Date

CustomerID

ProductID

StoreID

Quantity

Discount

PaymentMethod

2. Products (Dimension Table)
ProductID

ProductName

Category

SubCategory

UnitPrice

CostPrice

3. Customers (Dimension Table)
CustomerID

FirstName

LastName

Gender

City

BirthDate

JoinDate

4. Stores (Dimension Table)
StoreID

StoreName

City

Region

 Data Cleaning & Preparation
Performed using Power Query:

Removed duplicate TransactionIDs

Handled missing values in critical fields (ProductID, CustomerID, StoreID)

Replaced missing discounts with 0

Validated business rules:

Quantity > 0

UnitPrice ≥ CostPrice

Discount between 0 and 1

Converted date fields to proper Date format

 Data Model (Star Schema)
Fact Table: Transactions

Dimensions: Products, Customers, Stores, Date

Why Star Schema?
Faster query performance

Simpler DAX calculations

Better slicing and filtering

Industry-standard BI modeling approach

 DAX Measures Used
Total Sales
DAX
Copy code
Total Sales =
SUMX (
    Transactions,
    Transactions[Quantity] *
    RELATED ( Products[UnitPrice] ) *
    ( 1 - Transactions[Discount] )
)
Total Profit
DAX
Copy code
Total Profit =
SUMX (
    Transactions,
    ( RELATED ( Products[UnitPrice] ) -
      RELATED ( Products[CostPrice] ) )
    * Transactions[Quantity]
)
Profit Margin %
DAX
Copy code
Profit Margin % =
DIVIDE ( [Total Profit], [Total Sales], 0 ) * 100
 Dashboard Components
KPI Cards
Total Sales

Total Profit

Average Profit Margin %

Visuals
Bar Chart: Total Sales by Region

Bar Chart: Total Profit by Region

Scatter Plot: Sales vs Profit by Category

Table: Product-level Sales, Profit & Margin

Matrix: Category × Subcategory performance

Filters / Slicers
Region

Payment Method

Date

Category

Scatter Plot Analysis
The scatter plot compares Total Sales (X-axis) and Total Profit (Y-axis) with:

Color → Product Category

Size → Quantity Sold

Insights:
Top-right quadrant: High sales & high profit (Star products)

Bottom-left quadrant: Low sales & low profit (Discontinue)

High sales, low profit: Discount or cost issues

Key Insights
Fashion category performs best with high sales and profit

Electronics has strong sales but moderate profit margins

Groceries show low sales and low profitability

East region delivers stable profit margins

North and West regions show margin pressure due to discounts

 Business Recommendations
Promote
High-margin products with moderate sales

Fashion category products

Optimize
Electronics pricing and discount strategies

Discontinue / Reduce
Products with low sales and negative or very low profit margins

Weak-performing grocery products

Inventory Planning
Increase stock in high-margin regions

Reduce inventory for loss-making products

Tools Used
Power BI Desktop

Power Query

DAX (Data Analysis Expressions)

Conclusion
This Power BI dashboard provides a comprehensive view of sales and profitability across regions and categories. By combining a star schema data model, robust DAX calculations, and insightful visuals, the solution enables management to make informed decisions on promotions, pricing strategies, and inventory optimization.
