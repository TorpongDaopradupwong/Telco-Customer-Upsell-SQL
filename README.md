# Telco-Customer-Upsell-SQL
# 📡 Telco Customer Upsell Strategy using SQL

## 📌 Project Overview
This project simulates a real-world task at a Telecommunication company. The goal is to identify high-potential customers for an **"Upsell Campaign"** by analyzing their data usage patterns and current subscription plans using **SQL**.

## ❓ Business Problem
The Marketing team wants to launch a new high-speed internet package ("MaxSpeed"). To maximize conversion rates, they need a targeted list of customers who:
1.  Consume a high amount of data (**> 50 GB/month**).
2.  Are currently on a low-tier price plan (**< 500 THB**).
Targeting these specific customers prevents churn and increases Average Revenue Per User (ARPU).

## 🛠️ Tech Stack
* **Language:** SQL (SQLite), Python
* **Tools:** Jupyter Notebook, Pandas (for query execution)
* **Techniques:** Multi-table JOINs, Aggregations (SUM), Filtering (HAVING/WHERE), Sorting.

## 📊 Key Implementation
The core analysis involves joining 3 relational tables:
1.  `Subscribers` (Customer Info)
2.  `Packages` (Price Plans)
3.  `Data_Usage` (Transaction Logs)

**SQL Logic Used:**
```sql
SELECT 
    subscribers.name, 
    packages.package_name, 
    SUM(data_usage.data_gb) as Total_Data
FROM subscribers
INNER JOIN packages ON subscribers.package_id = packages.package_id
INNER JOIN data_usage ON subscribers.sub_id = data_usage.sub_id
WHERE packages.price < 500
GROUP BY subscribers.name
HAVING Total_Data > 50;
