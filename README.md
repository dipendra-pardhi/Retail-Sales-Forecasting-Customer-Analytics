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

