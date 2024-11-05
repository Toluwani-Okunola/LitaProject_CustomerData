# LitaProject_CustomerData

## Customer Data

### Project Overview
This data analysis project aims to provide insights into the sales performance of a retail store over the past and current year. By analysising various aspect of the data, we seek to identify (top selling product, product performance, regional performance and monthly sales trend, make data driven reccommendation and gain deeper understanding of the store performance

### Data Source
The primary dataset used for this analysis is the "sales data.csv" file containing detailed information about each sales made by the store. This was provided by the Incubator Hub.

### Tool Used
- Excel: 
  - Data Cleaning and Preparation
  - Data Analysis
- SQL: Structured Query Language for Querying of Data
- Power BI:
  - Data Visualization
  - Creating Report

### Data Cleaning and Preparation
In the initial stage, I performed the following task:
1. Data Loading and Inspection
2. Data Cleaning and Formating

### Exploratory Data Analysis
EDA involves exploring the sales data to answer key questions, such as;
  1. What is the overall sales trends?
  2. Which products are top sellers?
  3. What is the regional performance?
  4. What is the monthly sales trends?

### Data Analysis
These are the codes i wrote to query the data:
```
SELECT * FROM [dbo].[Customer Data]
```
1. retrieve the total number of customers from each region.
```
SELECT Region, COUNT(CustomerID) AS TotalCustomer FROM [dbo].[Customer Data]
GROUP BY Region
```
2. find the most popular subscription type by the number of customers.
```
SELECT TOP 1 SubscriptionType, COUNT(CustomerID) AS MostPopular FROM [dbo].[Customer Data]
GROUP BY SubscriptionType
ORDER BY 2 desc
```
3. find customers who canceled their subscription within 6 months.
```
SELECT CustomerID, SubscriptionStart, SubscriptionEnd FROM [dbo].[Customer Data]
WHERE DATEDIFF(Month, SubscriptionStart, SubscriptionEnd) <= 6
and Canceled = 0
```
4. calculate the average subscription duration for all customers.
```
SELECT AVG(DATEDIFF(Month, SubscriptionStart, SubscriptionEnd)) AS AverageDuration FROM [dbo].[Customer Data]
```
5. find customers with subscriptions longer than 12 months.
```
SELECT CustomerID, SubscriptionStart, SubscriptionEnd FROM [dbo].[Customer Data]
WHERE DATEDIFF(Month, SubscriptionStart, SubscriptionEnd) > 12
```
6. find customers with subscriptions longer than 12 months.
```
SELECT CustomerID, SubscriptionStart, SubscriptionEnd FROM [dbo].[Customer Data]
WHERE DATEDIFF(Month, SubscriptionStart, SubscriptionEnd) > 12
```
7. find the top 3 regions by subscription cancellations.
```
SELECT TOP 3 Region, COUNT(Canceled) AS TotalCanceled FROM [dbo].[Customer Data]
WHERE Canceled = 0
GROUP BY Region
ORDER BY 2 desc
```
8. find the total number of active and canceled subscriptions.
```
SELECT 
CASE WHEN Canceled = 0 THEN 'CanceledSubscription'
ELSE 'ActiveSubscription'
END AS Subcription,
COUNT(Canceled) as TotalNumber FROM [dbo].[Customer Data]
GROUP BY Canceled
```

### Results/Findings

### Reccommendation

### Limitation
I created a calculated column named Sales by mltiplying unit pric and quantity. This is an important column to analysis the sales performance of the store
