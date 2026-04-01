CREATE DATABASE retail_project;

	CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    gender VARCHAR(10),
    birth_date DATE,
    city VARCHAR(50),
    join_date DATE
);

CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    category VARCHAR(50),
    sub_category VARCHAR(50),
    unit_price NUMERIC(10,2),
    cost_price NUMERIC(10,2)
);

CREATE TABLE stores (
    store_id INT PRIMARY KEY,
    store_name VARCHAR(100),
    city VARCHAR(50),
    region VARCHAR(50)
);


CREATE TABLE transactions (
    transaction_id INT PRIMARY KEY,
    transaction_date DATE,
    customer_id INT,
    product_id INT,
    store_id INT,
    quantity INT,
    discount NUMERIC(5,2),
    payment_method VARCHAR(50),

    FOREIGN KEY (customer_id) REFERENCES customers(customer_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id),
    FOREIGN KEY (store_id) REFERENCES stores(store_id)
);

COPY customers(customer_id, first_name, last_name, gender, birth_date, city, join_date)
FROM 'C:\Users\Dipendra\Desktop\Customers.csv'
DELIMITER ','
CSV HEADER;


DROP TABLE customers;

CREATE TABLE customers (
    customer_id VARCHAR(10) PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    gender VARCHAR(10),
    birth_date DATE,
    city VARCHAR(50),
    join_date DATE
);


DROP TABLE transactions CASCADE;
DROP TABLE customers CASCADE;
DROP TABLE products CASCADE;
DROP TABLE stores CASCADE;

CREATE TABLE customers (
    customer_id VARCHAR(10) PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    gender VARCHAR(10),
    birth_date DATE,
    city VARCHAR(50),
    join_date DATE
);

CREATE TABLE products (
    product_id VARCHAR(10) PRIMARY KEY,
    product_name VARCHAR(100),
    category VARCHAR(50),
    sub_category VARCHAR(50),
    unit_price NUMERIC(10,2),
    cost_price NUMERIC(10,2)
);

CREATE TABLE stores (
    store_id VARCHAR(10) PRIMARY KEY,
    store_name VARCHAR(100),
    city VARCHAR(50),
    region VARCHAR(50)
);


DROP TABLE transactions;

CREATE TABLE transactions (
    transaction_id VARCHAR(10) PRIMARY KEY,
    transaction_date DATE,
    customer_id VARCHAR(10),
    product_id VARCHAR(10),
    store_id VARCHAR(10),
    quantity NUMERIC(10,2),  -- 🔥 CHANGE HERE
    discount NUMERIC(5,2),
    payment_method VARCHAR(50),

    FOREIGN KEY (customer_id) REFERENCES customers(customer_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id),
    FOREIGN KEY (store_id) REFERENCES stores(store_id)
);




COPY customers
FROM 'C:\Users\Dipendra\Desktop\Customers.csv'
DELIMITER ','
CSV HEADER;


COPY products
FROM 'C:\Users\Dipendra\Desktop\products.csv'
DELIMITER ','
CSV HEADER;

COPY stores
FROM 'C:\Users\Dipendra\Desktop\stores.csv'
DELIMITER ','
CSV HEADER;

COPY transactions
FROM 'C:\Users\Dipendra\Desktop\transactions.csv'
DELIMITER ','
CSV HEADER;



CREATE TABLE master_sales AS
SELECT 
    t.transaction_id,
    t.transaction_date,
    t.quantity,
    t.discount,
    t.payment_method,

    c.customer_id,
    c.first_name || ' ' || c.last_name AS customer_name,
    c.gender,
    c.city AS customer_city,
    c.join_date,

    p.product_id,
    p.product_name,
    p.category,
    p.sub_category,
    p.unit_price,
    p.cost_price,

    s.store_id,
    s.store_name,
    s.city AS store_city,
    s.region,

    -- 🔥 BUSINESS CALCULATIONS
    (p.unit_price * t.quantity * (1 - t.discount)) AS sales,
    ((p.unit_price - p.cost_price) * t.quantity) AS profit

FROM transactions t
JOIN customers c ON t.customer_id = c.customer_id
JOIN products p ON t.product_id = p.product_id
JOIN stores s ON t.store_id = s.store_id;


SELECT * FROM master_sales LIMIT 10;

SELECT COUNT(*) FROM master_sales;

SELECT ROUND(SUM(sales),2) FROM master_sales;

SELECT ROUND(SUM(profit),2) FROM master_sales;

SELECT COUNT(DISTINCT transaction_id) FROM master_sales;


SELECT 
    product_name,
    SUM(sales) AS total_revenue
FROM master_sales
GROUP BY product_name
ORDER BY total_revenue DESC
LIMIT 10;


SELECT 
    category,
    SUM(sales) AS total_sales
FROM master_sales
GROUP BY category
ORDER BY total_sales DESC;


SELECT 
    DATE_TRUNC('month', transaction_date) AS month,
    SUM(sales) AS monthly_sales
FROM master_sales
GROUP BY month
ORDER BY month;


SELECT 
    customer_name,
    SUM(sales) AS total_spent
FROM master_sales
GROUP BY customer_name
ORDER BY total_spent DESC
LIMIT 10;


SELECT 
    store_name,
    SUM(sales) AS total_sales
FROM master_sales
GROUP BY store_name
ORDER BY total_sales DESC;


SELECT 
    payment_method,
    COUNT(*) AS total_transactions
FROM master_sales
GROUP BY payment_method
ORDER BY total_transactions DESC;



SELECT 
    category,
    SUM(profit) AS total_profit
FROM master_sales
GROUP BY category
ORDER BY total_profit DESC;

SELECT DISTINCT category FROM master_sales;

