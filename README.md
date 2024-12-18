# LITA CAPSTONE PROJECT 1
## Project Title: Sales-Performance-Analysis-for-LITA-Store
---
### Table of Content

[Project Overview](#project-overview)

[Data Sources](#data-sources)

[Tools](#tools)

[Analysis Workflow](#analysis-workflow)

[Exploratory Data Analysis](#exploratory-data-analysis)

[Data Analysis](#data-analysis)

[Data Visualizations](#data-visualizations)

[Findings](#findings)

[Recommendations](#recommendations)

[Limitations and Learnings](#limitations-and-learnings)

[References](#references)

### Project Overview
---
This project presents the results of LITA store sales analysis aimed at addressing the issue of low turnover of some products and regional areas. The analysis aims to generate insight into the sales performance of LITA store, by analyzing various parameters in the data received to uncover key insights such as top-selling products, regional performance, and monthly sales trends. I seek to gather enough insight to identify trends, make data-driven recommendations and gain a deeper understanding of the store's performance.

### Data Sources
---
The primary source of data used here is Sales_Data.csv. This dataset was given to me by Incubator Hub and similar dataset can also be gotten from any open data source online.

### Tools
---
- Ms Excel [Download Here](https://www.microsoft.com)
   - Data Cleaning
   - Pivot Table Analysis
- SQL - Quering and Analysis
- PowerBi - Data Visualization
- GitHub -  Portfolio building

### Analysis Workflow
---
#### Data Preparation in Excel
- Data Cleaning: Removing duplicates
- Basic Calculations:
   1. Using pivot tables to summarize total sales by product, region, and month.
   2. Using Excel formulas to calculate metrics such as average sales per product, total revenue by region, and total revenue by product.
   3. Creating a column for the total revenue by multiplying Quantity and Unit Price

#### SQL Queries and Data Analysis
- Data Import: Importing the cleaned Excel data into SQL Server.
- Data Transformation: Using SQL queries to filter, group, and aggregate data.

#### Power BI Dashboard Development
- Data Import: Importing the raw data into PowerBi
- Data Transformation: Removing duplicates and blank rows, as well as creating measures
- Visualizations: Creating visuals such as column charts, bar charts, donut chart, and cards represent sales data.

### Exploratory Data Analysis
---
EDA involved the exploring of the Data to answer some questions about the data such as;
- What is the total sales for each product category?
- What is the total revenue per product?
- What are the the top-performing products?
- What is the percentage of total sales contributed by each region?

### Data Analysis
---
This includes some queries I worked with during the analysis. Example:

---Retrieve total sales of each product category---
``` sql
SELECT Product, SUM(Quantity * UnitPrice) AS TotalRevenue
FROM SalesData
GROUP BY Product
ORDER BY TotalRevenue DESC;
```
---Number of sales transaction in each region---
```SQL
SELECT Region, COUNT(Quantity * UnitPrice) AS Number_of_Sales_Transaction
FROM SalesData
GROUP BY Region;
```
--- Highest-selling product by total sales value---
```SQL
SELECT TOP 1 Product, SUM(Quantity * UnitPrice) AS TotalSales
FROM SalesData
GROUP BY Product
ORDER BY TotalSales DESC;
```
---calculate total revenue per Product---
```sql
SELECT Product, SUM(Quantity * UnitPrice) AS TotalRevenue
FROM SalesData
GROUP BY Product
ORDER BY TotalRevenue DESC;
```
---calculate monthly sales totals for the current year---
```SQL
SELECT 
    DATENAME(MONTH, OrderDate) AS SalesMonth, 
    SUM(Quantity * UnitPrice) AS TotalSales
FROM 
    SalesData
WHERE 
    YEAR(OrderDate) = YEAR(GETDATE())
GROUP BY 
    OrderDate
ORDER BY 
    TotalSales Desc;
```
---find the top 5 customers by total purchase amount---
```sql
SELECT TOP 5 Customer_Id, SUM(Quantity * UnitPrice) AS TotalPurchaseAmount
FROM SalesData
GROUP BY Customer_Id
ORDER BY TotalPurchaseAmount DESC
```
---calculate the percentage of total sales contributed by each region---
``` sql
SELECT 
    Region,
    SUM(CASE WHEN Total_Revenue IS NOT NULL THEN Total_Revenue ELSE 0 END) AS Region_Sales,
   (SUM(CASE WHEN Total_Revenue IS NOT NULL THEN Total_Revenue ELSE 0 END) * 100.0) / 
   (SELECT SUM(CASE WHEN Total_Revenue IS NOT NULL THEN Total_Revenue ELSE 0 END) FROM SalesData) AS Total_Sales_Percentage
FROM 
    SalesData
GROUP BY 
    Region;
```
---identify products with no sales in the last quarter---
```sql
WITH last_quarter AS (
    SELECT 
        DATEADD(QUARTER, -1, GETDATE()) AS startdate,
        GETDATE() AS end_date
),
split_sales AS (
    SELECT 
        TRIM(value) AS product,
        Total_Revenue
    FROM 
        SalesData
    CROSS APPLY STRING_SPLIT(product, ',')  -- Split the product column
)
SELECT 
    DISTINCT product
FROM 
    split_sales
WHERE 
    Total_Revenue >= (SELECT startdate FROM last_quarter) 
    AND Total_Revenue < (SELECT end_date FROM last_quarter)
```
### Data Visualizations
---
<img width="960" alt="SalesData Pivot Table" src="https://github.com/user-attachments/assets/46aff3dc-2a77-436c-8c42-0235b7c8b3c7">

<img width="907" alt="Sales_Dashboard" src="https://github.com/user-attachments/assets/15f053cd-133c-4512-a78d-a4be9ec3aafb">

<img width="960" alt="SalesData Spreadsheet" src="https://github.com/user-attachments/assets/9eb790a3-e476-43ed-99d4-21d3df47f883">

### Findings
At the end of this data analysis , it was determined that;
  1.  The product with the highest total sales value is Shoes with a total sale of 613,380.
  2.  The highest-selling product by total quantity sold is Hat with a total of 15,929.
  3.  East had the highest number of sold products.
  4.  Higher percentage of the total revenue was generated from sales in the South.
  5.  In the current year, February had the highest sales with 298,800 sales.
  6.  The total revenue per product is;

      |PRODUCT|REVENUE|
      |-------|-------|
      |Shoes|613,380|
      |Shirt|485,600|
      |Hat|316,195|
      |Gloves|296,900|
      |Jacket|208,230|
      |Socks|180,785|

### Recommendations
Based on the analysis, we recommend the following actions;
   - Allocate budget toward promoting Gloves, Jackets, and Socks to expand their market share. Running campaigns and discounts during colder months may be effective, as these products align with winter needs and may drive higher purchase volumes.
   - With February identified as the highest sales month, it’s recommended to prepare ahead for similar seasonal demand in upcoming years. Increase inventory levels, especially for top products like Shoes and Shirts, and plan promotional events or discounts in early June to capture customer interest.
   - The East region shows the highest number of sold products, indicating a strong customer base. Allocate additional resources, such as targeted promotions and localized advertising, to further boost engagement in this high-performing region.
   - Since Shoes are the top-selling product by sales, consider prioritizing this product in marketing campaigns and feature it prominently in both online and in-store displays. 
     
### Limitations and Learnings
I had to remove duplicate entries that would have affected the accuracy of my conclusion in the analysis. Through this analysis, I was able to gain more insights in handling data inconsistencies, SQL query optimization, and Power BI performance.

### References
During this analysis, I made reference to the following sources to better my analysis
- [Ladies In Tech Africa Bootcamp||Data Analysis](https://www.youtube.com/live/ZZJiY4Tmtgo?feature=shared)
- [W3Schools online learning](https://pathfinder.w3schools.com/learningpaths)
