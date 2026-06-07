# 🛒 BlinkIT Sales Analysis | SQL + Power BI Project

# <h2>📷 Dashboard Preview</h2>

<p align="center">
  <img src="dashboard.png" width="1000">
</p>

---

## 📌 Project Overview

This project analyzes BlinkIT's sales performance, customer satisfaction, and inventory distribution using SQL and Power BI.

The objective is to uncover business insights related to product performance, outlet performance, customer ratings, and sales distribution to support data-driven decision-making and operational optimization.

The project combines:

* SQL for data cleaning and business analysis
* Power Query for data transformation
* DAX for KPI calculations
* Power BI for interactive dashboard development

---

# 🎯 Business Objectives

The project aims to answer the following business questions:

### KPI Requirements

* What is the Total Sales generated?
* What is the Average Sales per item?
* How many Items have been sold?
* What is the Average Customer Rating?

### Analytical Requirements

* Impact of Fat Content on Sales
* Sales Performance by Item Type
* Fat Content Analysis by Outlet
* Outlet Establishment Impact on Sales
* Sales Contribution by Outlet Size
* Geographic Sales Distribution
* Complete KPI Analysis by Outlet Type

---

# 🛠 Tools & Technologies

| Tool        | Purpose                  |
| ----------- | ------------------------ |
| SQL Server  | Data Cleaning & Analysis |
| Power Query | Data Transformation      |
| Power BI    | Dashboard Development    |
| DAX         | KPI Calculations         |
| Excel/CSV   | Source Dataset           |

---

# 📂 Dataset Information

The dataset contains grocery sales records including:

* Item Type
* Item Fat Content
* Total Sales
* Item Visibility
* Outlet Type
* Outlet Size
* Outlet Location Type
* Outlet Establishment Year
* Rating

---

# 🧹 Data Cleaning Using SQL

One of the major data quality issues was inconsistent naming within the Item_Fat_Content column.

### Before Cleaning

| Original Values |
| --------------- |
| LF              |
| low fat         |
| Low Fat         |
| reg             |
| Regular         |

### SQL Cleaning Query

```sql
UPDATE blinkit_data
SET Item_Fat_Content =
CASE
    WHEN Item_Fat_Content IN ('LF','low fat')
        THEN 'Low Fat'
    WHEN Item_Fat_Content='reg'
        THEN 'Regular'
    ELSE Item_Fat_Content
END;
```

### Validation Query

```sql
SELECT DISTINCT Item_Fat_Content
FROM blinkit_data;
```

This standardization improved reporting accuracy and aggregation consistency.

---

# 🔄 Power Query Transformations

Additional data preparation was performed using Power Query.

### Transformations Performed

✔ Data type corrections

✔ Column formatting

✔ Null value checks

✔ Data validation

✔ Data loading optimization

✔ Business-ready dataset creation

---

# 📊 DAX Measures

### Total Sales

```DAX
Total Sales =
SUM('BlinkIT Grocery Data'[Sales])
```

### Average Sales

```DAX
Avg Sales =
AVERAGE('BlinkIT Grocery Data'[Sales])
```

### Number of Items

```DAX
No. of Items =
COUNTROWS('BlinkIT Grocery Data')
```

### Average Rating

```DAX
Avg Rating =
AVERAGE('BlinkIT Grocery Data'[Rating])
```

---

# 📈 Dashboard Features

## KPI Cards

The dashboard displays:

* Total Sales
* Average Sales
* Number of Items
* Average Rating

---

## Visual Analysis

### 1. Total Sales by Fat Content

Objective:

Analyze how fat content influences sales performance.

Metrics:

* Total Sales
* Average Sales
* Number of Items
* Average Rating

---

### 2. Total Sales by Item Type

Objective:

Identify top-performing product categories.

Metrics:

* Total Sales
* Average Sales
* Number of Items
* Average Rating

---

### 3. Fat Content by Outlet

Objective:

Compare sales generated from Low Fat and Regular products across outlet locations.

Metrics:

* Total Sales
* Average Sales
* Number of Items
* Average Rating

---

### 4. Total Sales by Outlet Establishment Year

Objective:

Evaluate how outlet age impacts sales performance.

---

### 5. Percentage of Sales by Outlet Size

Objective:

Understand contribution of outlet size toward overall sales.

Outlet Categories:

* Small
* Medium
* High

---

### 6. Sales by Outlet Location

Objective:

Analyze geographic sales distribution.

Locations:

* Tier 1
* Tier 2
* Tier 3

---

### 7. All Metrics by Outlet Type

Objective:

Provide a complete performance comparison between outlet formats.

Metrics:

* Total Sales
* Average Sales
* Number of Items
* Average Rating
* Item Visibility

---

# 💾 SQL Analysis

The project includes SQL queries covering:

### KPI Calculations

* Total Sales
* Average Sales
* Number of Items
* Average Rating

### Sales Analysis

* Sales by Fat Content
* Sales by Item Type
* Sales by Outlet Location
* Sales by Outlet Size
* Sales by Outlet Establishment Year

### Advanced SQL

* CASE Statements
* Aggregations
* Window Functions
* PIVOT Tables
* Data Cleaning Queries
* Data Validation Queries

---

# 🔍 Key Business Insights

### Product Performance

* Certain item categories contribute disproportionately to total revenue.
* Product mix significantly impacts sales performance.

### Fat Content Analysis

* Consumer preference patterns can be observed between Low Fat and Regular products.
* Fat content influences overall revenue contribution.

### Outlet Analysis

* Larger outlets contribute a greater share of sales.
* Outlet establishment year impacts sales performance.
* Sales distribution differs across outlet locations.

### Customer Satisfaction

* Customer ratings remain relatively consistent across categories.
* Highly rated products often correlate with stronger sales performance.

---

# 💡 Business Recommendations

### Inventory Optimization

Maintain higher stock levels for top-performing product categories.

### Product Strategy

Increase visibility and promotions for high-margin products.

### Outlet Expansion

Prioritize expansion strategies in high-performing outlet locations.

### Customer Experience

Focus on improving product quality and customer satisfaction ratings.

### Performance Monitoring

Track outlet-level KPIs regularly to identify underperforming locations.

---

# 🚀 Skills Demonstrated

## SQL

* Data Cleaning
* Data Validation
* Aggregate Functions
* CASE Statements
* Window Functions
* PIVOT Operations
* Business Querying

## Power BI

* Dashboard Development
* Interactive Visualizations
* KPI Design
* Data Storytelling

## Power Query

* Data Cleaning
* Data Transformation
* ETL Processes

## DAX

* Measures
* KPI Calculations
* Business Metrics

## Business Analytics

* Sales Analysis
* Customer Satisfaction Analysis
* Inventory Analysis
* Retail Analytics
* Performance Monitoring

---

# 👨‍💻 Author

**Shubham Singh**

Aspiring Data Analyst | SQL | Power BI | Excel | Statistics | Python

This project demonstrates end-to-end retail analytics, combining SQL-based data analysis with Power BI dashboard development to generate actionable business insights for sales optimization and decision-making.
