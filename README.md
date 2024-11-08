# Lita Capstone Project

## Customer Data

[Project Overview](#project-overview)

[Data Source](#data-source)

[Metrics of Focus](#metrics-of-focus)

[Tool Used](#tool-used)

[Data Cleaning and Preparation](#data-cleaning-and-preparation)

[Exploratory Data Analysis](#exploratory-data-analysis)

[Data Analysis](#data-analysis)
  - [Formulars](#formulars)
  - [Queries](#queries)

[Visual Analysis Inference](#visual-analysis-inference)
  - [Data Summary](#data-summary)
  - [Data Visualization](#data-visualization)

[Results and Findings](#results-and-findings)

[Recommendation](#recommendation)

[Limitation](#limitation)



### Project Overview
--------------------------------------------------------------------------------------------------------------------------------------------------------

This data analysis project aims analyze customer data for a subscription service to identify segments and trends. By analysising various aspect of the data, I seek to identify customer behaviour, track subscription type and identify key trend in cancellation and renewal, make data driven reccommendation and gain deeper understanding of the Service Company.


### Data Source
---------------------------------------------------------------------------------------------------------------------------------------------------

The primary dataset used for this analysis is the "Customer data.csv" file containing detailed information about each sales made by the Service Company. This was provided by the Incubator Hub.

This dataset include the following columns:

Customer ID - Unique ID to identify each customer

Customer Name - Name of Customer

Region - Region where the customer belong

Subscription Type - Type of subscription plan each customer subscribed to

Subscription Start - Start date of each customer subscription

Subscription End - End date of each customer subcription

Canceled - Status of each customer

Revenue - Price of each subscription type


### Metrics of Focus
--------------------------------------------------------------------------------------------------------------------------------------------------------------

Subscription Type

Canceled

Count of customerID

Region


### Tool Used
-----------------------------------------------------------------------------------------------------------------------------------------------------------

- Excel: 
  - Data Cleaning and Preparation
  - Data Analysis
- SQL: Structured Query Language for Querying of Data
- Power BI:
  - Data Visualization
  - Creating Report


### Data Cleaning and Preparation
-----------------------------------------------------------------------------------------------------------------------------------------------------

In the initial stage, I performed the following task:
1. Data Loading and Inspection
2. Data Cleaning and Formating


### Exploratory Data Analysis
--------------------------------------------------------------------------------------------------------------------------------------------------------------------

EDA involves exploring the sales data to answer key questions, such as;
  1. What is total number of cancelled and Active Subscription
  2. Which subscription type is top seller
  3. What is the regional performance?
  4. What is the monthly sales trends?
  5. How much revenue was lost to Cancelled Subscription


### Data Analysis

#### Formulars
---------------------------------------------------------------------------------------------------------------------------------------------------------------

Formular used to calculate most popular type

Basic - Most POPULAR
```
=COUNTIF(D2:D33788,D2)
```

PREMIUN
```
=COUNTIF(D2:D33788,D3)
```

Standard
```
=COUNTIF(D2:D33788,D5)
```


Formular used to calculate average subscription duration
```
=AVERAGE(Table2[Sub-Month Duration])
```

Formular used to sort canceled

FALSE
```
=COUNTIF(Table2[Canceled],G2)
```

TRUE
```
=COUNTIF(Table2[Canceled],G3)
```


![C Formular Result](https://github.com/user-attachments/assets/476a8476-50c0-4ce8-8465-282618050374)


#### Queries
---------------------------------------------------------------------------

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

#### Data Summary
----------------------------------------------------------------------------------------------------------------

SUBSCRIPTION TYPE

![customer data](https://github.com/user-attachments/assets/9f4342bc-f30f-4384-bdc2-05461fe8e4af)

SUBSCRIPTION TYPE

![customer 1](https://github.com/user-attachments/assets/e5135788-e96e-4530-9dee-fa7cd5fb9e51)

CANCELLATION

![customer 2](https://github.com/user-attachments/assets/c16d578d-8628-4a71-826d-b3796a9a5b5c)

REGION

![customer 3](https://github.com/user-attachments/assets/bc9b358a-ceb6-4e33-b7be-94697f5d8829)

MONTH and YEAR
![customer 4](https://github.com/user-attachments/assets/2c48ba59-687a-4011-b037-c16e2113d63d)


#### Data Visualization
-----------------------------------------------------------------------------------------------

![customer visual](https://github.com/user-attachments/assets/53e9a8bb-8a9a-4b98-96f1-5ddf4c483a62)

![customer visual 1](https://github.com/user-attachments/assets/3e0bf330-238e-499b-819d-111f7bc4f680)

![customer visual 2](https://github.com/user-attachments/assets/07044a1f-6b73-4d5e-8fae-c22a6c8eb3f2)

![customer visual 3](https://github.com/user-attachments/assets/cd2e0aa2-247c-4f9e-ab08-cf650c46dc9c)


### Results and Findings
----------------------------------------------------------------------------------------

1. Active Subscriptions: 15,175
2. Canceled Subscriptions: 18,612
3. Total Customers: 33,787
4. Cancellation Rate: 55%
5. Total Revenue: $67,540,175
6. Average Subscription Duration:    12 months

*Customer Segment Analysis:*

1. Top-performing subscription type by Revenue and Count:
 Basic
2. Cancellation Distribution:
    - Basic: 11,854 (canceled), 5,067 (active)
    - Premium: 3,382 (canceled), 5,064 (active)
    - Standard: 3,376 (canceled), 5,044 (active)

*Regional Analysis:*

1. East: 100% cancellation rate
2. North: Best-performing region with highest active users and lowest cancellations

*Subscription Trends:*

1. Peak Subscription Month: November 2023
2. YoY Comparison:
    - 2023: 17m (active), 24m (canceled)
    - 2024: 14m (active), 13m (canceled)

Only one type of subscription type is available in all region


### Recommendation
------------------------------------------------------------------------------------------------------------------------------

1. Investigate cancellation reasons to reduce revenue loss.
2. Market and promote Premium and Standard subscriptions type.
3. Target top-performing regions with tailored marketing strategies.
4. Offer all subscription types to all regions.
5. Review Basic Subscription type package


### Limitation
---------------------------------------------------------------------------------------------------------------------------

I created a calculated column named Sub Duration using the subscription start and end column. This is an important column to analysis the average of subscription duration in the service company.
