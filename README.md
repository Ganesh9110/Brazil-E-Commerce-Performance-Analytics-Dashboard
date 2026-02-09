Brazil E-Commerce Performance Analytics Dashboard
📌 Project Summary

This project delivers an end-to-end analytics solution for a Brazilian e-commerce business using Snowflake for data engineering and Power BI for interactive business intelligence.
The dashboard provides actionable insights into revenue, profit, delivery performance, seller efficiency, and category trends through a clean, professional, multi-page design.
---------------------------------
🧱 Tech Stack

->Data Warehouse: Snowflake
->Query Language: SQL
->Visualization Tool: Power BI
->Data Modeling: Star Schema
->Domain: E-Commerce Analytics
---------------------------------
🗂 Dataset Overview

Brazilian E-Commerce public dataset containing transactional and dimensional data.

Source Tables

Orders

Order Items

Products

Product Categories

Sellers

Customers

Order Reviews
----------------------------------------------------
⚙️ Data Engineering (Snowflake)
1️⃣ Warehouse & Database Setup

USE WAREHOUSE Brazil_WH;
CREATE OR REPLACE DATABASE LIST_DB;
USE DATABASE LIST_DB;
CREATE OR REPLACE SCHEMA LIST_SCHEMA;
USE SCHEMA LIST_SCHEMA;
-------------------------------------------------
2️⃣ Orders Cleansing & Delivery Logic

Created a clean orders table with business-ready delivery status logic.

CREATE OR REPLACE TABLE CLEAN_ORDERS AS 
SELECT
    ORDER_ID,
    CUSTOMER_ID,
    ORDER_STATUS,
    ORDER_PURCHASE_TIMESTAMP,
    ORDER_APPROVED_AT,
    ORDER_DELIVERED_CARRIER_DATE,
    ORDER_DELIVERED_CUSTOMER_DATE,
    ORDER_ESTIMATED_DELIVERY_DATE,
    CASE
        WHEN ORDER_DELIVERED_CUSTOMER_DATE IS NULL THEN 'Not Delivered'
        WHEN ORDER_DELIVERED_CUSTOMER_DATE > ORDER_ESTIMATED_DELIVERY_DATE THEN 'Delivered Late'
        ELSE 'Delivered On Time'
    END AS DELIVERY_STATUS
FROM ORDERS;
------------------------------------------------------------------------------------
3️⃣ Order Items Cleansing
CREATE OR REPLACE TABLE CLEAN_ORDER_ITEMS AS
SELECT
    ORDER_ID,
    PRODUCT_ID,
    SELLER_ID,
    CAST(PRICE AS FLOAT) AS PRICE,
    CAST(FREIGHT_VALUE AS FLOAT) AS FREIGHT_VALUE
FROM ORDER_ITEMS;
---------------------------------------------------------
4️⃣ Reviews Cleansing
CREATE OR REPLACE TABLE CLEAN_ORDER_REVIEWS AS
SELECT
    REVIEW_ID,
    ORDER_ID,
    REVIEW_SCORE,
    COALESCE(REVIEW_COMMENT_MESSAGE, 'No Comment') AS REVIEW_COMMENT_MESSAGE,
    REVIEW_CREATION_DATE,
    REVIEW_ANSWER_TIMESTAMP
FROM ORDER_REVIEWS;
--------------------------------------------------------
5️⃣ Product Data Quality Filtering

Only valid product dimensions were retained.

CREATE OR REPLACE TABLE CLEAN_PRODUCTS AS
SELECT *
FROM PRODUCTS
WHERE PRODUCT_WEIGHT_G IS NOT NULL
  AND PRODUCT_LENGTH_CM IS NOT NULL
  AND PRODUCT_HEIGHT_CM IS NOT NULL
  AND PRODUCT_WIDTH_CM IS NOT NULL;
-----------------------------------------------------------
6️⃣ Category Mapping (Portuguese → English)
CREATE OR REPLACE TABLE PRODUCT_CATEGORY_CLEAN AS 
SELECT
    P.PRODUCT_ID,
    C.PRODUCT_CATEGORY_NAME_ENGLISH AS CATEGORY_NAME
FROM PRODUCTS P
LEFT JOIN PRODUCT_CATEGORY C
    ON P.PRODUCT_CATEGORY_NAME = C.PRODUCT_CATEGORY_NAME;
-----------------------------------------------------------
7️⃣ Date Dimension (DIM_DATE)

A custom Date Dimension built using recursive SQL.

CREATE OR REPLACE TABLE DIM_DATE AS
WITH RECURSIVE calendar AS (
    SELECT DATE('2016-09-04') AS DATE_VALUE
    UNION ALL
    SELECT DATE_VALUE + INTERVAL '1 DAY'
    FROM calendar
    WHERE DATE_VALUE + INTERVAL '1 DAY' <= '2018-10-17'
)
SELECT 
    DATE_VALUE AS DATE,
    YEAR(DATE_VALUE) AS YEAR,
    MONTH(DATE_VALUE) AS MONTH_NUM,
    TO_CHAR(DATE_VALUE, 'Month') AS MONTH_NAME,
    QUARTER(DATE_VALUE) AS QUARTER,
    WEEK(DATE_VALUE) AS WEEK_NUM,
    DAY(DATE_VALUE) AS DAY_NUM,
    TO_CHAR(DATE_VALUE, 'DY') AS DAY_NAME,
    CASE 
        WHEN MONTH(DATE_VALUE) BETWEEN 1 AND 3 THEN 'Q1'
        WHEN MONTH(DATE_VALUE) BETWEEN 4 AND 6 THEN 'Q2'
        WHEN MONTH(DATE_VALUE) BETWEEN 7 AND 9 THEN 'Q3'
        ELSE 'Q4' 
    END AS QUARTER_NAME
FROM calendar
ORDER BY DATE_VALUE;
-------------------------------------------------------------------------
🧠 Data Model

->Fact Tables: Orders, Order Items
->Dimension Tables: Date, Products, Sellers, Categories, Customers
->Optimized star schema for Power BI performance and slicer interaction.

--------------------------------------------------------------------------

📊 Power BI Dashboard

Page 1 — Executive Overview
Purpose: High-level business monitoring

<img width="1351" height="741" alt="Screenshot 2026-02-09 072316" src="https://github.com/user-attachments/assets/fa06be08-f561-4fdb-a06f-5ff6b2ff48f3" />

->Visuals Included:
->KPI Cards: Revenue, Orders, Profit, AOV, Delivery %
->Monthly Revenue Trend
->Orders by Category
->Delivery Status Distribution
->Revenue Share by Category (Treemap)
->Orders by State

----------------------------------------------------------------------------
Page 2 — Product & Seller Performance

Purpose: Identify profitable categories and seller efficiency

->Visuals Included:
->Monthly Profit Trend
->Revenue vs Profit by Category
->Top Sellers by Revenue
->Seller Performance Table (Revenue, Profit, Orders)
->Freight Cost & Profit Margin KPIs

--------------------------------------------------------------------

Page 3 — Category Drill-Through Analysis

Purpose: Deep-dive analysis per category

Features:

->Drill-through enabled from category visuals
->Selected Category Card
->Monthly Revenue & Orders
->Seller Count
->Revenue by Seller
->Monthly Orders Trend
->Delivery Time Trend
->Top Cities by Orders

---------------------------------------------

📈 Key Business Insights

->Revenue growth is strongly correlated with on-time delivery.
->Over 94% orders delivered on time, positively impacting ratings.
->A small number of sellers generate a large share of revenue.
->Some high-revenue categories operate with lower profit margins.
->Freight cost optimization presents a major profit opportunity.
---------------------------------------------------------------------

💡 Business Recommendations

->Improve logistics for sellers with repeated late deliveries
->Focus promotions on high-margin categories
->Optimize freight costs to increase profitability
->Reduce dependency on top sellers by diversifying seller base
->Use drill-through views for targeted category decisions

------------------------------------------------------------------------

🧠 Skills Demonstrated

->Advanced SQL (Snowflake)
->Data Cleaning & Transformation
->Dimensional Modeling
->Time Intelligence & KPIs
->Power BI Dashboard Design
->Business Analytics & Storytelling

---------------------------------------------------------------------

✅ Final Notes

This project demonstrates end-to-end ownership of the analytics lifecycle — from raw data ingestion and modeling to executive-level business insights.
