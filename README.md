# 🛍 Retail Query Insights  
**SQL Project | Beginner Level | Database: p1_retail_db**

## 📌 Project Overview

This project demonstrates foundational SQL techniques typically used by data analysts to explore, clean, and analyze retail sales data. It involves setting up a retail sales database, performing exploratory data analysis (EDA), and answering business-specific questions through SQL queries.

> Ideal for beginners starting their journey in data analysis and looking to build a strong base in SQL.

---

## 🎯 Objectives

- *Set Up a Retail Sales Database*: Create and populate a structured retail sales database.
- *Data Cleaning*: Identify and remove records with missing or null values.
- *Exploratory Data Analysis (EDA)*: Understand the dataset using SQL.
- *Business Insights*: Answer business-driven questions and generate meaningful insights.

---

## 🗂 Project Breakdown

### 1️⃣ Database Setup

sql
CREATE DATABASE p1_retail_db;

CREATE TABLE retail_sales (
    transactions_id INT PRIMARY KEY,
    sale_date DATE,	
    sale_time TIME,
    customer_id INT,	
    gender VARCHAR(10),
    age INT,
    category VARCHAR(35),
    quantity INT,
    price_per_unit FLOAT,	
    cogs FLOAT,
    total_sale FLOAT
);


## Data Exploration & Cleaning

-- Total number of records
SELECT COUNT(*) FROM retail_sales;

-- Count of unique customers
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;

-- Unique product categories
SELECT DISTINCT category FROM retail_sales;

-- Check for null/missing values
SELECT * FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;

-- Delete records with missing values
DELETE FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;

## Business Analysis – SQL Queries

-- 1. All sales made on '2022-11-05'
SELECT * FROM retail_sales
WHERE sale_date = '2022-11-05';

-- 2. Clothing sales with quantity > 4 in Nov-2022
SELECT * FROM retail_sales
WHERE category = 'Clothing'
AND TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
AND quantity > 4;

-- 3. Total sales and order count per category
SELECT category, SUM(total_sale) AS net_sale, COUNT(*) AS total_orders
FROM retail_sales
GROUP BY category;

-- 4. Average age of customers in 'Beauty' category
SELECT ROUND(AVG(age), 2) AS avg_age
FROM retail_sales
WHERE category = 'Beauty';

-- 5. Transactions with total_sale > 1000
SELECT * FROM retail_sales
WHERE total_sale > 1000;

-- 6. Number of transactions by gender in each category
SELECT category, gender, COUNT(*) AS total_trans
FROM retail_sales
GROUP BY category, gender
ORDER BY category;

-- 7. Best-selling month per year based on average sales
SELECT year, month, avg_sale FROM (
    SELECT 
        EXTRACT(YEAR FROM sale_date) AS year,
        EXTRACT(MONTH FROM sale_date) AS month,
        AVG(total_sale) AS avg_sale,
        RANK() OVER(PARTITION BY EXTRACT(YEAR FROM sale_date) ORDER BY AVG(total_sale) DESC) AS rank
    FROM retail_sales
    GROUP BY year, month
) AS t1
WHERE rank = 1;

-- 8. Top 5 customers by total sales
SELECT customer_id, SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 5;

-- 9. Unique customers per category
SELECT category, COUNT(DISTINCT customer_id) AS cnt_unique_cs
FROM retail_sales
GROUP BY category;

-- 10. Orders grouped by time-of-day shifts
WITH hourly_sale AS (
    SELECT *, 
        CASE
            WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
            WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
            ELSE 'Evening'
        END AS shift
    FROM retail_sales
)
SELECT shift, COUNT(*) AS total_orders
FROM hourly_sale
GROUP BY shift;


## 📈 Key Findings

- **Customer Demographics**: Sales are spread across a range of age groups and genders.
- **High-Value Purchases**: Transactions over ₹1000 indicate premium customer segments.
- **Category Performance**: Categories like Clothing and Beauty show frequent and high-volume transactions.
- **Top Customers**: Some customers significantly outspend others, enabling targeted marketing.
- **Sales Trends**: Certain months and times of day show higher sales, useful for planning promotions.

---

## 📝 Reports Generated

- **Sales Summary**: Overall sales, orders, and category-wise breakdown.
- **Trend Analysis**: Monthly and shift-based trends for decision-making.
- **Customer Insights**: Unique and high-value customer data for segmentation.

---

## 🧰 How to Use This Project

### 📥 Clone the Repository

bash
git clone https://github.com/SPARSH402/retail-query-insights