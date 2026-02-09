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

<img width="450" height="225" alt="image" src="https://github.com/user-attachments/assets/2a8f4543-6e0a-4a5b-8d70-e0a72e8f1ff4" />



-------------------------------------------------
2️⃣ Orders Cleansing & Delivery Logic

Created a clean orders table with business-ready delivery status logic.

<img width="1063" height="425" alt="image" src="https://github.com/user-attachments/assets/7773ea5b-ce7d-44dd-bfda-3c46aca92fbb" />


------------------------------------------------------------------------------------
3️⃣ Order Items Cleansing

<img width="523" height="187" alt="image" src="https://github.com/user-attachments/assets/b120ca45-86b9-4650-b50d-c89dc4d319e8" />
-----------------------

4️⃣ Date Dimension (DIM_DATE)

A custom Date Dimension built using recursive SQL.

<img width="681" height="611" alt="Screenshot 2026-02-09 120504" src="https://github.com/user-attachments/assets/a6af3375-299c-48fe-8d64-da6abe0ed4f1" />

-------------------------------------------------------------------------
🧠 Data Model

->Fact Tables: Orders, Order Items

->Dimension Tables: Date, Products, Sellers, Categories, Customers

->Optimized star schema for Power BI performance and slicer interaction

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

<img width="1336" height="751" alt="Screenshot 2026-02-09 072339" src="https://github.com/user-attachments/assets/b0c84a18-e70b-4fb0-821b-4db204a81d67" />

->Visuals Included:

->Monthly Profit Trend

->Revenue vs Profit by Category

->Top Sellers by Revenue

->Seller Performance Table (Revenue, Profit, Orders)

->Freight Cost & Profit Margin KPIs

--------------------------------------------------------------------

Page 3 — Category Drill-Through Analysis

Purpose: Deep-dive analysis per category

<img width="1337" height="753" alt="Screenshot 2026-02-09 072402" src="https://github.com/user-attachments/assets/d8397a8e-c9cf-4520-9475-4e1af33a250d" />

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
