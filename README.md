# SQL-Project-Retail-Sales-Analysis

Project Overview
Project Title: Retail-Sales-Analysis
Level: Beginner
Database name: SQL - Retail Sales Analysis
Data Source: Github
Description: Retail sales analysis using Basic SQL to uncover trends, top category, and customer behavior

Developed an end-to-end SQL-based retail sales analysis project to extract actionable business insights from transactional data. Designed and structured a relational database, performed data cleaning and exploratory data analysis (EDA), and wrote optimized SQL queries to analyze sales performance, customer purchasing behavior, product trends, and revenue patterns. Applied SQL concepts including Joins, Aggregate Functions, GROUP BY, CASE Statements, Subqueries, CTEs, and Window Functions to answer business-driven analytical questions and provide a comprehensive 360-degree view of retail operations.

Expected Outcomes: 
1. Creating the dataset: Create the dataset of a retail store using sales data.
2. Data Cleaning & Transformation: Identify duplicates and remove. If required then change records with missing or null values.
3. Exploratory Data Analysis (EDA): Perform basic exploratory data analysis to understand the dataset and evaluate the correlations within the dataset.
4. Data Analysis: Leverage SQL analytics to extract actionable insights and answer critical business questions from sales performance data.

1.	Database Setup
   
•	Database Creation: Project initialization begins with the creation of the retail_sales_db database.

•   Table Creation: The retail_sales_data_analysis table stores transactional sales records. The schema consists of the following attributes: transaction_id, sale_date, sale_time, customer_id, gender, age, product_group, quantity (Qty of goods sold), price_per_unit, cogs (cost of good sold), and total_sale.

Query:

CREATE TABLE Retail_Sales 
(

transactions_id INT PRIMARY KEY,

sale_date DATE,

sale_time TIMESTAMP,

customer_id INT,

gender VARCHAR(15),

age INT,

product_group VARCHAR(20),

quantiy INT,

price_per_unit FLOAT,

cogs FLOAT,

total_sale FLOAT

);


3. Data Cleaning & Data Transformation
   
1 Total Records: Count all rows in the dataset.
Query:

SELECT COUNT(*)  AS total_transactions 

FROM retail_sales_data_analysis;

Output:

2000


2 Product Groups: List all distinct product groups.

Query:

SELECT DISTINCT product groups AS different_groups_of_product

FROM retail_sales_data_analysis;

Output:

1 Beauty

2 Clothing

3 Electronics


3 Unique Customers: Find the total number of customer.

Query:

SELECT COUNT(DISTINCT customer_id) AS total_number_of_customer

FROM retail_sales_data_analysis;

Output:

155

4 Checking Missing Data: Remove any rows containing null or empty values.

Query:

SELECT * FROM retail_sales_data_analysis

WHERE 
    
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR product_group IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;


DELETE FROM retail_sales_data_analysis

WHERE 
    
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR product_group IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;

OR
SELECT
    SUM(CASE WHEN transactions_id IS NULL THEN 1 ELSE 0 END) AS missing_transaction_id,
    SUM(CASE WHEN sale_date IS NULL THEN 1 ELSE 0 END) AS missing_sale_date,
    SUM(CASE WHEN sale_time IS NULL THEN 1 ELSE 0 END) AS missing_sale_time,
    SUM(CASE WHEN customer_id IS NULL THEN 1 ELSE 0 END) AS missing_customer_id,
    SUM(CASE WHEN gender IS NULL THEN 1 ELSE 0 END) AS missing_gender,
    SUM(CASE WHEN age IS NULL THEN 1 ELSE 0 END) AS missing_age,
    SUM(CASE WHEN category IS NULL THEN 1 ELSE 0 END) AS missing_category,
    SUM(CASE WHEN quantiy IS NULL THEN 1 ELSE 0 END) AS missing_quantity,
    SUM(CASE WHEN price_per_unit IS NULL THEN 1 ELSE 0 END) AS missing_price,
    SUM(CASE WHEN cogs IS NULL THEN 1 ELSE 0 END) AS missing_cogs,
    SUM(CASE WHEN total_sale IS NULL THEN 1 ELSE 0 END) AS missing_sales
FROM retail_sales;

5. Check duplicate transactions
SELECT
    transactions_id,
    COUNT(*) AS transaction_count
FROM retail_sales
GROUP BY transactions_id
HAVING COUNT(*) > 1;

6. Check invalid values
SELECT *
FROM retail_sales
WHERE quantiy <= 0
   OR price_per_unit <= 0
   OR cogs < 0
   OR total_sale <= 0;
If this returns no rows, there are no duplicate transaction IDs.

7. Validate sales calculation

This is a very good data-validation query for your project.

SELECT *
FROM retail_sales
WHERE quantiy IS NOT NULL
  AND price_per_unit IS NOT NULL
  AND total_sale IS NOT NULL
  AND total_sale <> quantiy * price_per_unit;

This checks whether:

Quantity × Price Per Unit = Total Sale

Note: Skipped null checks for transaction_id due to its Primary Key (non-nullable) constraint. 

Data cleaning is complete; dataset is ready for exploratory data analysis (EDA) and modeling.

3. Data Analysis & Findings
The following SQL queries were developed to answer specific business questions:

1: Retrieve all columns for sales made in the month of "June":

Query: 

SELECT *

FROM retail_sales_data_analysis

WHERE sale_date >= '2023-06-01'

AND sale_date < '2023-07-01';

2: Retrieve all columns for sales made in the month of "June":

CREATE TABLE retail_sales (
    transactions_id INT PRIMARY KEY,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(10),
    age INT,
    category VARCHAR(50),
    quantiy INT,
    price_per_unit DECIMAL(10,2),
    cogs DECIMAL(10,2),
    total_sale DECIMAL(10,2)
);
