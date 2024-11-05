# LitaProject_CustomerData

## Customer Data

### Project Overview
This data analysis project aims analyze customer data for a subscription service to identify 
segments and trends. By analysising various aspect of the data, we seek to identify customer behaviour, track subscription type and identify key trend in cancellation and renewal, make data driven reccommendation and gain deeper understanding of the Service Company.

### Data Source
The primary dataset used for this analysis is the "Customer data.csv" file containing detailed information about each sales made by the Service Company. This was provided by the Incubator Hub.

### Metrics of Focus
Subscription Type
Canceled
Count of customerID
Region

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
  1. What is total number of cancelled and Active Subscription
  2. Which subscription type is top seller
  3. What is the regional performance?
  4. What is the monthly sales trends?
  5. How much revenue was lost to Cancelled Subscription

### Data Analysis
These are the excel formular i used to calculate the most popular subscription, Aveage Subscription Duration and the Total Number of Canceled and Active Subscription
![C Formular Result](https://github.com/user-attachments/assets/476a8476-50c0-4ce8-8465-282618050374)

These are the codes i wrote to query the data:
```
SELECT * FROM [dbo].[Customer Data]
```
1. retrieve the total number of customers from each region.
```
SELECT Region, COUNT(CustomerID) AS TotalCustomer FROM [dbo].[Customer Data]
GROUP BY Region
```
![consumer data q1](https://github.com/user-attachments/assets/bb449d50-9b73-4e30-94a1-f47b64c0bd35)

2. find the most popular subscription type by the number of customers.
```
SELECT TOP 1 SubscriptionType, COUNT(CustomerID) AS MostPopular FROM [dbo].[Customer Data]
GROUP BY SubscriptionType
ORDER BY 2 desc
```
![consumer data q2](https://github.com/user-attachments/assets/7a318a05-adb1-4478-aa0c-27fe2b46bec9)
3. find customers who canceled their subscription within 6 months.
```
SELECT CustomerID, SubscriptionStart, SubscriptionEnd FROM [dbo].[Customer Data]
WHERE DATEDIFF(Month, SubscriptionStart, SubscriptionEnd) <= 6
and Canceled = 0
```
![consumer data q3](https://github.com/user-attachments/assets/07dce480-62bd-4589-b883-e33e14f90195)
4. calculate the average subscription duration for all customers.
```
SELECT AVG(DATEDIFF(Month, SubscriptionStart, SubscriptionEnd)) AS AverageDuration FROM [dbo].[Customer Data]
```
![consumer data q4](https://github.com/user-attachments/assets/1419a6ce-1b65-424e-b81f-f542dbf8c09a)
5. find customers with subscriptions longer than 12 months.
```
SELECT CustomerID, SubscriptionStart, SubscriptionEnd FROM [dbo].[Customer Data]
WHERE DATEDIFF(Month, SubscriptionStart, SubscriptionEnd) > 12
```
![consumer data q5](https://github.com/user-attachments/assets/a2f0bd23-57b9-42b7-90b6-9e42a34a1fa9)
6. find customers with subscriptions longer than 12 months.
```
SELECT CustomerID, SubscriptionStart, SubscriptionEnd FROM [dbo].[Customer Data]
WHERE DATEDIFF(Month, SubscriptionStart, SubscriptionEnd) > 12
```
![consumer data q6](https://github.com/user-attachments/assets/d06de85b-b921-46b7-b91a-f23f1641696f)
7. find the top 3 regions by subscription cancellations.
```
SELECT TOP 3 Region, COUNT(Canceled) AS TotalCanceled FROM [dbo].[Customer Data]
WHERE Canceled = 0
GROUP BY Region
ORDER BY 2 desc
```
![consumer data q7](https://github.com/user-attachments/assets/96a3cd43-b865-4fd9-90f8-a3a58df78184)
8. find the total number of active and canceled subscriptions.
```
SELECT 
CASE WHEN Canceled = 0 THEN 'CanceledSubscription'
ELSE 'ActiveSubscription'
END AS Subcription,
COUNT(Canceled) as TotalNumber FROM [dbo].[Customer Data]
GROUP BY Canceled
```
![consumer data q8](https://github.com/user-attachments/assets/c97e8903-00e2-4eff-b4bb-43cd86f93bc0)

### Visual Analysis Inference
Data Summary using Pivot Table
![customer data](https://github.com/user-attachments/assets/9f4342bc-f30f-4384-bdc2-05461fe8e4af)
![customer 1](https://github.com/user-attachments/assets/e5135788-e96e-4530-9dee-fa7cd5fb9e51)
![customer 2](https://github.com/user-attachments/assets/c16d578d-8628-4a71-826d-b3796a9a5b5c)
![customer 3](https://github.com/user-attachments/assets/bc9b358a-ceb6-4e33-b7be-94697f5d8829)
![customer 4](https://github.com/user-attachments/assets/2c48ba59-687a-4011-b037-c16e2113d63d)


Data Visualization using Power BI
![customer visual](https://github.com/user-attachments/assets/20893269-3e3f-4692-9a6f-4e5f6470425e)

![customer visual 1](https://github.com/user-attachments/assets/e449b418-0f78-4358-8460-c7963d9fd160)

![customer visual 2](https://github.com/user-attachments/assets/07044a1f-6b73-4d5e-8fae-c22a6c8eb3f2)

![customer visual 3](https://github.com/user-attachments/assets/cd2e0aa2-247c-4f9e-ab08-cf650c46dc9c)



### Results/Findings

### Reccommendation

### Limitation
I created a calculated column named Sub Duration using the subscription start and end column. This is an important column to analysis the average of subscription duration in the service company
