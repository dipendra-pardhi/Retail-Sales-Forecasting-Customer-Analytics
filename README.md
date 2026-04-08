# 📊 Data Analytics Projects Portfolio

This repository contains end-to-end Data Analytics projects using SQL, Power BI, and Python to generate business insights and predictive analysis.

---

# 🔹 Project 1: Retail Sales Forecasting & Customer Analytics

## 📌 Introduction

This project focuses on analyzing retail sales data to understand product performance, customer behavior, and sales trends. It also includes time-series forecasting to predict future sales and support business decision-making.

---

## 📂 Data Sources

The dataset includes:

* Transaction data (sales, quantity, date)
* Customer data (customer details)
* Product data (category, product info)
* Store data (city, region)

---

## 📊 Project Overview

* Cleaned and prepared raw data using Excel
* Created structured dataset using SQL joins
* Built KPI dashboards in Power BI
* Performed time-series analysis and forecasting using Python

---

## 🛠 Tools & Technologies

* Excel, PostgreSQL, Power BI, Python (Pandas, Matplotlib, ARIMA)

---

## 📌 SQL: Master Table Creation

```sql
SELECT 
    t.transaction_id,
    t.transaction_date,
    t.quantity,
    t.sales,
    t.profit,
    c.customer_name,
    p.product_name,
    p.category,
    s.store_city,
    s.region
FROM transactions t
JOIN customers c ON t.customer_id = c.customer_id
JOIN products p ON t.product_id = p.product_id
JOIN stores s ON t.store_id = s.store_id;
```

---

## 📌 SQL: Sales Analysis

```sql
SELECT 
    category,
    SUM(sales) AS total_sales
FROM master_sales
GROUP BY category
ORDER BY total_sales DESC;
```

---

## 📌 Python: Monthly Sales Trend

```python
import pandas as pd

df['transaction_date'] = pd.to_datetime(df['transaction_date'])

monthly_sales = df.groupby(
    pd.Grouper(key='transaction_date', freq='ME')
)['sales'].sum()
```

---

## 📌 Python: Visualization

```python
import matplotlib.pyplot as plt

monthly_sales.plot()
plt.title("Monthly Sales Trend")
plt.xlabel("Date")
plt.ylabel("Sales")
plt.show()
```

---

## 📌 Python: Forecasting (ARIMA)

```python
from statsmodels.tsa.arima.model import ARIMA

model = ARIMA(monthly_sales, order=(1,1,1))
model_fit = model.fit()

forecast = model_fit.forecast(steps=6)
```

---

## 📊 Key Insights

* Identified top-performing product categories contributing major revenue
* Analyzed customer purchasing behavior and transaction patterns
* Observed seasonal trends and monthly fluctuations
* Predicted future sales trends using ARIMA model

---

## 🚀 Conclusion

This project demonstrates a complete analytics workflow from data cleaning to predictive modeling.

---

# 🔹 Project 2: E-Commerce Sales & Customer Behavior Analysis

## 📌 Introduction

This project analyzes e-commerce data to understand sales performance, customer behavior, payment trends, and delivery efficiency to improve business decision-making.

---

## 📂 Data Sources

The dataset includes:

* Orders data
* Customer details
* Product information
* Payment methods
* Delivery and review data

---

## 📊 Project Overview

* Imported and structured raw data using SQL
* Created master dataset using joins
* Performed analysis on sales, payments, and delivery
* Built interactive dashboards in Power BI

---

## 🛠 Tools & Technologies

* Excel, PostgreSQL, Power BI

---

## 📌 SQL: Master Table Creation

```sql
SELECT 
    o.order_id,
    o.customer_id,
    c.customer_city,
    o.order_purchase_timestamp,
    o.order_delivered_customer_date,
    o.order_estimated_delivery_date,
    oi.product_id,
    oi.price,
    oi.freight_value,
    p.product_category_name,
    py.payment_type,
    py.payment_value,
    r.review_score
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
JOIN order_items oi ON o.order_id = oi.order_id
JOIN products p ON oi.product_id = p.product_id
JOIN order_payments py ON o.order_id = py.order_id
LEFT JOIN order_reviews r ON o.order_id = r.order_id;
```

---

## 📌 SQL: Payment Analysis

```sql
SELECT payment_type, COUNT(*) 
FROM master_table
GROUP BY payment_type
ORDER BY COUNT(*) DESC;
```

---

## 📌 SQL: Delivery Performance

```sql
SELECT 
COUNT(*) FILTER (WHERE order_delivered_customer_date > order_estimated_delivery_date) AS late_orders,
COUNT(*) AS total_orders
FROM master_table;
```

---

## 📌 SQL: Category Analysis

```sql
SELECT product_category_name, SUM(price) AS revenue
FROM master_table
GROUP BY product_category_name
ORDER BY revenue DESC;
```

---

## 📊 Key Insights

* Credit card contributed majority (~75%) of transactions
* Identified ~40%+ late deliveries affecting customer experience
* Top product categories generated highest revenue
* Customer ratings provided insights into satisfaction

---

## 🚀 Conclusion

This project highlights the use of SQL and Power BI to generate actionable insights from e-commerce data.

---

# 📂 Project Structure

```
📁 Data-Analytics-Projects
 ├── Retail-Project/
 ├── E-Commerce-Project/
 └── README.md
```

---

# 🔥 Future Improvements

* Add machine learning models (churn prediction, forecasting)
* Improve dashboard interactivity
* Expand customer segmentation

---
