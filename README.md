### LITA_DATA_CAPSTONE_PROJECT-UD
---
### Project Overview
----
The LITA Data Capstone Project aims to enhance data analysis skills by analyzing and visualizing data, presenting insights into key metrics, 
trends, and patterns, building an interactive dashboard, and documenting findings to present a comprehensive report.

### Data Sources
----
The dataset for this analysis was sourced from The Incubator Hub as part of an internal data initiative supporting the LITA Data Capstone Project. This data was provided exclusively for training and analysis purposes, with a focus on exploring key performance metrics, trends, and patterns relevant to E-commerce.

### Dataset Details
----
- Source: The Incubator Hub (Internal Dataset)
- Scope of Data: This dataset includes essential metrics capturing various aspects of sales, customer transactions, product performance, and time-based trends within an E-commerce framework.
- Sample Size: The dataset is a comprehensive sample curated to reflect diverse sales data points and customer interactions, ideal for extracting meaningful insights.
- Data Processing: The data was preprocessed and cleaned, ensuring consistency and accuracy. Processing steps included handling missing values, normalizing fields, and refining the data structure for analysis.
  
### Key Attributes
---
The dataset covers:

- Sales Metrics: Detailed transaction data, including sales quantities, prices, and discounts.
- Customer Demographics: Information on customer segmentation by region, age group, and purchasing behavior.
- Product Information: Attributes related to product categories, stock-keeping units (SKUs), and performance by product line.
- Temporal Data: Time-stamped sales data to analyze seasonal and monthly trends.
  
This structured dataset enables a robust analysis of sales patterns, customer behavior, and product performance, providing valuable insights for decision-making.

### Tools Used
- Microsoft Excel: Utilized for initial data cleaning, analysis, and visualizations to gain preliminary insights. [Download Here](https://www.microsoft.com)  
- SQL (Structured Query Language): Used to clean data, filter, or aggregate it for analysis before importing into Power BI. [Download Server Here](https://www.microsoft.com/en-us/sql-server/sql-server-downloads) and [SMSS](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16&redirectedfrom=MSDN)
- Power BI: Employed to build an interactive dashboard, enabling dynamic data exploration and visual storytelling of insights through visuals like pie charts, bar charts, line graphs, etc.
- GitHub: Used for version control, documentation, and portfolio building, providing a platform to showcase the project.

### Data Characteristics
----
The dataset includes the following variables:
- Order: A unique identifier for each order transaction that helps differentiate between individual orders.
- Customer Id: A unique identifier for each customer which links orders or subscriptions back to specific customers, useful for customer analysis.
- Product: Represents the specific product ordered
- Region: Geographic region where the customer or order originates (North, South, East & West)
- Order Date: The date when the order was placed
- Quantity: The number of units ordered
- UnitPrice: The price per unit of the product
- Total Revenue: The total revenue from each order, likely calculated as ```Quantity * UnitPrice```.
- Customer Name: The full name of the customer
- Subscription Type: The type or level of subscription (e.g., Basic, Premium, Standard)
- Subscription Start: The starting date of the customer’s subscription
- Subscription End: The end date of the customer’s subscription
- Canceled: Indicates whether the subscription has been canceled
- SUBSCRIPTION DURATION: The length of the subscription in days, months, or years
- AVERAGE SUBSCRIPTION: Likely represents the average subscription length or revenue per customer.

### Methodology
----
### Data Loading and Initial Inspection
Loaded the dataset in Excel & Power BI and did a preliminary inspection to understand its structure, types of data in each column, and overall cleanliness.
### Remove Duplicates
Checked for and removed any duplicate rows, especially in critical columns like Order, Customer ID, and Product. This is essential for accurate calculations, like total revenue or unique customer counts.
### Handle Missing Values
Identified missing values in crucial columns such as Customer ID, Order Date, Quantity, UnitPrice, Subscription Type, etc.
### Standardize Data Formats
Standardized the format of each column to ensure consistency, especially for dates, numbers, and currency.
Convert date fields (Order Date, Subscription Start, Subscription End) to a consistent date format (e.g., YYYY-MM-DD).
Ensure numeric fields like UnitPrice and Total Revenue are formatted to 2 decimal places.
### Correct Data Types
Checked and set data types for each column (e.g., dates, numbers, text).
### Create New Variables 
Generated additional columns to add value to the analysis, such as:
Total Revenue: Calculate if missing by using Quantity * UnitPrice.
Subscription Duration: Calculated the length of each subscription as Subscription End - Subscription Start.
### Standardize Categorical Data
Ensured uniformity in categorical columns (Region, Product, Subscription Type):
Remove extra spaces, standardize casing (e.g., title case), and correct spelling inconsistencies.
### Data Validation and Logical Consistency Checks
Performed logical checks, such as:
Ensuring Subscription End dates are after Subscription Start.
Verifying that Quantity and Unit Price are positive values.
Checking that calculated revenue values match expected results.
### Final Checks and Documentation
Performed a final review of the cleaned data, confirming that all transformations are applied correctly.
Document each cleaning step in GitHub, detailing the rationale and impact of the changes made.

### Exploratory Data Analysis
---
EDA involved the exploring of the Data to answer some questions about the Data;
### Analysis Questions
- What is the total sales for each product category?
- How many sales transactions occurred in each region?
- What is the top-selling product by total sales value?
- How much revenue has each product generated?
- What is the monthly breakdown of sales for the current year?
- What are the top 5 customers with the highest total purchase amount?
- What is the percentage contribution of total sales by each region?
- Which products had no sales in the last quarter?
- What is the total number of customers from each region?
- What is the most popular subscription type based on the number of customers?
- Which customers canceled their subscription within the last 6 months?
- What is the average subscription duration for all customers?
- What is the total revenue generated by each subscription type?
- Which are the top 3 regions with the highest subscription cancellations?
- What is the total number of active and canceled subscriptions?

### Approach
---
### Data Visualization
Each question was addressed using descriptive statistics, visualizations, and statistical tests to determine significance and identify key trends.

![LITA SALES 1](https://github.com/user-attachments/assets/781174d9-d9a9-4e35-b69a-82c1a43ce292)

![LITA SALES 2](https://github.com/user-attachments/assets/aea8fcf8-04aa-48b3-b150-278a61f5b7b2)

![Customer Segmentation 1](https://github.com/user-attachments/assets/100d56b4-b1e0-4a38-ac01-50ce09cb30e0)

![Customer Segmentation 2](https://github.com/user-attachments/assets/03cae4b6-d315-4b1f-81e3-12cd4a6b6330)


### Data Analysis
----
This is where we include some basic lines of code or queries during the analysis in SQL
``` ---------Retrieve the Total Sales from each product category-------

SELECT sum (Quantity) As Total_Sales, PRODUCT from [dbo].[UD Sales Data]
group by PRODUCT
order by 1 desc
```

``` -------Number of Sales transactions in each region------

SELECT Region, COUNT(Quantity) AS NumberOfTransactions
FROM [dbo].[UD Sales Data]
GROUP BY Region;
```

``` ------Monthly Sales Totals for the Current Year------

SELECT Month(Orderdate) AS Month,SUM(Quantity * Unitprice) AS Monthly_Sales
FROM [dbo].[UD Sales Data]
WHERE Year(Orderdate) = Year(Getdate())
GROUP by Month(Orderdate);
```

``` ----The most popular subsription type by the numbers of customers----
Select Top 1 [SubscriptionType],COUNT(Distinct [CustomerID]) AS Total_Customers
From [dbo].[LITA Capstone Dataset - Customer Segment UDUAK]
Group by SubscriptionType
Order by Total_Customers desc;
```

``` ----The Total number of active and canceled Subscriptions----
SELECT 
    COUNT(CASE WHEN Canceled = 1 THEN 1 END) AS Active_subscriptions,
    COUNT(CASE WHEN Canceled = 0 THEN 1 END) AS Canceled_subscriptions
FROM [dbo].[LITA Capstone Dataset - Customer Segment UDUAK];
```










