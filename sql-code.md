# SQL Analysis

This section contains all SQL queries used for data cleaning, KPI calculation, and business analysis of the BlinkIT Grocery dataset.

---

## 1. View Complete Dataset

```sql
SELECT *
FROM blinkit_data;
```

**Purpose:** Verify that the dataset has been imported successfully and inspect the available columns.

---

## 2. Data Cleaning

### Standardize Item Fat Content Values

The `Item_Fat_Content` column contained inconsistent values such as:

* LF
* low fat
* Low Fat
* reg
* Regular

The following query standardizes these values to improve reporting consistency.

```sql
UPDATE blinkit_data
SET Item_Fat_Content =
    CASE
        WHEN Item_Fat_Content IN ('LF', 'low fat')
            THEN 'Low Fat'
        WHEN Item_Fat_Content = 'reg'
            THEN 'Regular'
        ELSE Item_Fat_Content
    END;
```

### Validate Data Cleaning

```sql
SELECT DISTINCT Item_Fat_Content
FROM blinkit_data;
```

---

# KPI Analysis

## 1. Total Sales

**Objective:** Calculate total revenue generated from all items sold.

```sql
SELECT CONCAT(
        CAST(SUM(Sales)/1000000 AS DECIMAL(10,2)),
        'M'
       ) AS Total_Sales_Millions
FROM blinkit_grocery_data;
```
<p align="center">
  <img src="screenshot/1.png" width="100">
</p>

---

## 2. Average Sales

**Objective:** Calculate average revenue per transaction.

```sql
SELECT CONCAT(
        CAST(AVG(Sales) AS DECIMAL(10,0)),
        'M'
       ) AS Avg_Sales
FROM blinkit_grocery_data;
```
<p align="center">
  <img src="screenshot/2.png" width="100">
</p>

---

## 3. Number of Items

**Objective:** Count total items sold.

```sql
SELECT COUNT(*) AS Total_No_Items
FROM blinkit_grocery_data;
```
<p align="center">
  <img src="screenshot/3.png" width="100">
</p>

---

## 4. Average Rating

**Objective:** Measure average customer satisfaction rating.

```sql
SELECT CAST(
        AVG(Rating) AS DECIMAL(10,2)
       ) AS Avg_Rating
FROM blinkit_grocery_data;
```
<p align="center">
  <img src="screenshot/4.png" width="100">
</p>

---

# Granular Business Analysis

## 1. Total Sales by Fat Content

### Objective

Analyze how fat content impacts sales performance and compare additional KPIs across fat content categories.

### Metrics

* Total Sales
* Average Sales
* Number of Items
* Average Rating

```sql
SELECT
    `Item Fat Content`,
    CONCAT(CAST(SUM(Sales)/1000 AS DECIMAL(10,2)), 'k') AS Total_Sales,
    CONCAT(CAST(AVG(Sales) AS DECIMAL(10,0)), 'M') AS Avg_Sales,
    COUNT(*) AS Total_No_Items,
    CAST(AVG(Rating) AS DECIMAL(10,2)) AS Avg_Rating
FROM blinkit_grocery_data
GROUP BY `Item Fat Content`
ORDER BY Total_Sales DESC;
```

---

## 2. Total Sales by Item Type

### Objective

Identify top-performing product categories based on sales.

```sql
SELECT
    `Item Type`,
    CONCAT(CAST(SUM(Sales)/1000 AS DECIMAL(10,2)), 'k') AS Total_Sales,
    CONCAT(CAST(AVG(Sales) AS DECIMAL(10,0)), 'M') AS Avg_Sales,
    COUNT(*) AS Total_No_Items,
    CAST(AVG(Rating) AS DECIMAL(10,2)) AS Avg_Rating
FROM blinkit_grocery_data
GROUP BY `Item Type`
ORDER BY Total_Sales DESC;
```

---

## 3. Fat Content by Outlet Location

### Objective

Compare sales performance of Low Fat and Regular products across outlet locations.

```sql
SELECT
    `Item Fat Content`,
    `Outlet Location Type`,
    CONCAT(CAST(SUM(Sales)/1000 AS DECIMAL(10,2)), 'k') AS Total_Sales,
    CONCAT(CAST(AVG(Sales) AS DECIMAL(10,0)), 'M') AS Avg_Sales,
    COUNT(*) AS Total_No_Items,
    CAST(AVG(Rating) AS DECIMAL(10,2)) AS Avg_Rating
FROM blinkit_grocery_data
GROUP BY
    `Item Fat Content`,
    `Outlet Location Type`
ORDER BY Total_Sales DESC;
```

---

## 4. Total Sales by Outlet Establishment Year

### Objective

Evaluate how outlet age influences revenue generation.

```sql
SELECT
    `Outlet Establishment Year`,
    CONCAT(CAST(SUM(Sales)/1000 AS DECIMAL(10,2)), 'k') AS Total_Sales,
    CONCAT(CAST(AVG(Sales) AS DECIMAL(10,0)), 'M') AS Avg_Sales,
    COUNT(*) AS No_Of_Items
FROM blinkit_grocery_data
GROUP BY `Outlet Establishment Year`
ORDER BY `Outlet Establishment Year`;
```

---

## 5. Percentage of Sales by Outlet Size

### Objective

Determine the contribution of each outlet size toward overall sales.

```sql
SELECT
    `Outlet Size`,
    CAST(SUM(Sales) AS DECIMAL(10,2)) AS Total_Sales,
    CAST(
        (SUM(Sales) * 100.0 /
        SUM(SUM(Sales)) OVER())
        AS DECIMAL(10,2)
    ) AS Sales_Percentage
FROM blinkit_grocery_data
GROUP BY `Outlet Size`;
```

**Note:** `OVER()` is used as a window function to calculate overall sales while preserving grouped results.

---

## 6. Sales by Outlet Location

### Objective

Analyze geographical distribution of sales.

```sql
SELECT
    `Outlet Location Type`,
    CAST(SUM(Sales) AS DECIMAL(10,2)) AS Total_Sales,
    CAST(
        (SUM(Sales) * 100.0 /
        SUM(SUM(Sales)) OVER())
        AS DECIMAL(10,2)
    ) AS Sales_Percentage
FROM blinkit_grocery_data
GROUP BY `Outlet Location Type`;
```

---

## 7. All KPIs by Outlet Type

### Objective

Compare outlet types across all major business metrics.

### Metrics Included

* Total Sales
* Average Sales
* Number of Items
* Average Rating

```sql
SELECT
    `Outlet Type`,
    CONCAT(CAST(SUM(Sales)/1000 AS DECIMAL(10,2)), 'k') AS Total_Sales,
    CONCAT(CAST(AVG(Sales) AS DECIMAL(10,0)), 'M') AS Avg_Sales,
    COUNT(*) AS No_Of_Items,
    CAST(AVG(Rating) AS DECIMAL(10,2)) AS Avg_Rating
FROM blinkit_grocery_data
GROUP BY `Outlet Type`
ORDER BY Total_Sales DESC;
```

---

## SQL Skills Demonstrated

* Data Cleaning
* Data Validation
* Aggregate Functions
* GROUP BY Operations
* CASE Statements
* Window Functions
* Business KPI Analysis
* Retail Sales Analytics
* Customer Satisfaction Analysis
* Inventory Performance Analysis
