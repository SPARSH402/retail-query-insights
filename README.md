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

---

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
