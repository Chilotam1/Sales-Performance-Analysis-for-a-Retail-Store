# LITA CAPSTONE PROJECT
## Project Title: Sales-Performance-Analysis-for-a-Retail-Store

### 1.  Project Overview
---
This data analysis project aims to generate insight into the sales performance of a retail store. By analyzing various parameters in the data received, we seek to gather enough insight to identify trends, make data-driven recommendations and gain a deeper understanding of the store's performance.

### 2. Data Sources
---
The primary source of data used here is Sales_Data.csv. This dataset was given to me by Incubator Hub and similar dataset can also be gotten from any open data source online.

### 3. Tools
---
- Ms Excel [Download Here](https://www.microsoft.com)
   - Data Cleaning
   - Pivot Table Analysis
- SQL - Quering and Analysis
- PowerBi - Data Visualization
- GitHub -  Portfolio building

### 4. Analysis Workflow
---
#### 4.1 Data Preparation in Excel
- Data Cleaning: Removing duplicates
- Basic Calculations:
   1. Using pivot tables to summarize total sales by product, region, and month.
   2. Using Excel formulas to calculate metrics such as average sales per product, total revenue by region, and total revenue by product.
   3. Creating a column for the total revenue by multiplying Quantity and Unit Price

#### 4.2 SQL Queries and Data Analysis
- Data Import: Importing the cleaned Excel data into SQL Server.
- Data Transformation: Using SQL queries to filter, group, and aggregate data.

#### 4.3 PowerBi Dashboard Development
- Data Import: Importing the raw data into PowerBi
- Data Transformation: Removing duplicats and blank rows
- Visualizations: Creating visuals such as column charts, bar charts, donut chart, and cards represent sales data.

### 5. Exploratory Data Analysis
---
EDA involved the exploring of the Data to answer some questions about the data such as;
- What is the total sales for each product category?
- What is the total revenue per product?
- What are the the top-performing products?
- What is the percentage of total sales contributed by each region?

### 6. Data Analysis
---
This includes some queries I worked with during the analysis. Example:

``` sql
SELECT Product, SUM(Total_Revenue) AS TotalRevenue
FROM SalesData
GROUP BY Product
ORDER BY TotalRevenue DESC;
```

``` sql
SELECT 
    Region,
    SUM(CASE WHEN Quantity IS NOT NULL THEN Quantity ELSE 0 END) AS Region_Sales,
   (SUM(CASE WHEN Quantity IS NOT NULL THEN Quantity ELSE 0 END) * 100.0) / 
   (SELECT SUM(CASE WHEN Quantity IS NOT NULL THEN Quantity ELSE 0 END) FROM SalesData) AS Total_Sales_Percentage
FROM 
    SalesData
GROUP BY 
    Region;
```
### 7. Data Visualization
---
<img width="960" alt="Sales Dashboard" src="https://github.com/user-attachments/assets/4e25f7da-9663-4d32-87be-e1cd4a130dd9">

<img width="960" alt="SalesData Pivot Table" src="https://github.com/user-attachments/assets/574542c0-43fc-40d1-b87e-92ab46945664">
<img width="960" alt="SalesData Spreadsheet" src="https://github.com/user-attachments/assets/3cc9d5ee-1adb-45c1-bcfa-45add521fa42">

