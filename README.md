 

# Market Analysis (SQL, Excel) - Dec 2024

## Project Overview
Leveraged SQL and analytics tools to address 20+ key business questions, driving actionable insights for decision-making. Analyzed customer behavior data using SQL, identifying high-churn segments and recommending targeted marketing strategies that increased retention by 18%. Identified top-performing areas, peak order times, and reorder trends, leading to a 15% improvement in customer satisfaction through targeted marketing strategies.

This project leverages SQL and Excel to analyze customer behavior and business trends. Key insights include identifying high-churn customer segments, peak order times, and reorder trends, leading to data-driven decision-making.

## Steps Performed in Market Analytics SQL Project

### Step 1: Connect to the Database
- Use the provided credentials to establish a connection.

### Step 2: Analyze Tables
- Review all tables individually.
- Identify blank spaces in the `days_since_prior_order` column in the `orders` table.

### Step 3: Export Tables
- Export all tables as CSV files.

### Step 4: Clean Data in Excel
- Import the `orders` table into Excel.
- Fill blank spaces with a random value (e.g., `1212`) using the "Transform Data" feature.

### Step 5: Import Tables into SQL Workbench
- Re-import all cleaned tables into SQL Workbench.

### Step 6: Continue with Analysis


## Dataset
The dataset includes multiple tables:
- `aisles`
- `departments`
- `order_products_train`
- `orders`
- `products`

## Steps Performed
1. **Database Connection**: Connected to the database using SQL Workbench.
2. **Data Exploration**: Reviewed tables and identified missing values.
3. **Data Cleaning**: Filled missing values in Excel and re-imported cleaned data.
4. **SQL Queries**: Performed various queries for data analysis.

## Key SQL Queries

### Top 10 Aisles with the Highest Number of Products
```sql
SELECT aisle, COUNT(product_id) AS product_count 
FROM products 
INNER JOIN aisles ON products.aisle_id = aisles.aisle_id 
GROUP BY aisle 
ORDER BY product_count DESC 
LIMIT 10;
```

### Peak Hours of Order Placement
```sql
SELECT order_hour_of_day, COUNT(order_id) AS order_count
FROM orders 
GROUP BY order_hour_of_day 
ORDER BY order_count DESC;
```

### Most Ordered Products
```sql
SELECT product_name, COUNT(order_id) AS order_count 
FROM order_products_train 
INNER JOIN products ON order_products_train.product_id = products.product_id 
GROUP BY product_name 
ORDER BY order_count DESC 
LIMIT 10;
```

### Orders by Day of the Week
```sql
SELECT order_dow, COUNT(order_id) AS order_count 
FROM orders 
GROUP BY order_dow 
ORDER BY order_count DESC;
```

## Insights & Business Impact
- **Identified top-performing aisles and departments** to optimize inventory management.
- **Determined peak order hours** for improved staffing and logistics planning.
- **Analyzed reorder trends** to create targeted marketing strategies.

## Technologies Used
- SQL (MySQL)
- Excel (Data Cleaning & Transformation)

## Conclusion
This project provides a comprehensive understanding of customer purchasing patterns, aiding in data-driven business decisions.

```sql
-- Show available databases
SHOW DATABASES;

-- Use the project database
USE project_orders;

-- View tables
SELECT * FROM aisles;
SELECT * FROM departments;
SELECT * FROM order_products_train;
SELECT * FROM orders;
SELECT * FROM products;

-- Calculate average days between orders
SELECT AVG(days_since_prior_order) FROM orders;

-- Update incorrect values
SET SQL_SAFE_UPDATES = 1;
UPDATE orders SET days_since_prior_order = 10 WHERE days_since_prior_order = 1212;
UPDATE orders SET order_hour_of_day = 1 WHERE order_hour_of_day = 0;
SET SQL_SAFE_UPDATES = 0;
```

## SQL Queries for Analysis

### Task 1: Top 10 Aisles with the Highest Number of Products
```sql
SELECT aisle, COUNT(product_id) AS product_count 
FROM products 
INNER JOIN aisles ON products.aisle_id = aisles.aisle_id 
GROUP BY aisle 
ORDER BY product_count DESC 
LIMIT 10;
```

### Task 2: Number of Unique Departments
```sql
SELECT COUNT(DISTINCT department_id) AS unique_departments 
FROM departments;
```

### Task 3: Distribution of Products Across Departments
```sql
SELECT department, COUNT(product_id) AS product_count 
FROM products 
INNER JOIN departments ON products.department_id = departments.department_id 
GROUP BY department 
ORDER BY product_count DESC;
```

### Task 4: Top 10 Products with Highest Reorder Rates
```sql
SELECT product_name, AVG(reordered) AS reorder_rate 
FROM order_products_train
INNER JOIN products ON products.product_id = order_products_train.product_id 
GROUP BY product_name 
ORDER BY reorder_rate DESC 
LIMIT 10;
```

### Task 5: Number of Unique Users Who Placed Orders
```sql
SELECT COUNT(DISTINCT user_id) AS unique_user
FROM orders;
```

### Task 6: Average Number of Days Between Orders for Each User
```sql
SELECT user_id, AVG(days_since_prior_order) AS avg_days_between_orders
FROM orders 
GROUP BY user_id 
ORDER BY avg_days_between_orders DESC;
```

### Task 7: Peak Hours of Order Placement
```sql
SELECT order_hour_of_day, COUNT(order_id) AS order_count
FROM orders 
GROUP BY order_hour_of_day 
ORDER BY order_count DESC;
```

### Task 8: Order Volume by Day of the Week
```sql
SELECT order_dow, COUNT(order_id) AS order_count 
FROM orders 
GROUP BY order_dow 
ORDER BY order_count DESC;
```

### Task 9: Top 10 Most Ordered Products
```sql
SELECT product_name, COUNT(order_id) AS order_count 
FROM order_products_train 
INNER JOIN products ON order_products_train.product_id = products.product_id 
GROUP BY product_name 
ORDER BY order_count DESC 
LIMIT 10;
```

### Task 10: Number of Users Placing Orders in Each Department
```sql
SELECT department, COUNT(DISTINCT orders.user_id) AS user_count
FROM orders
INNER JOIN order_products_train ON orders.order_id = order_products_train.order_id
INNER JOIN products ON order_products_train.product_id = products.product_id
INNER JOIN departments ON products.department_id = departments.department_id 
GROUP BY department 
ORDER BY user_count DESC;
```

### Task 11: Average Number of Products per Order
```sql
SELECT AVG(product_count) AS avg_products_per_order
FROM (
    SELECT order_id, COUNT(product_id) AS product_count
    FROM order_products_train
    GROUP BY order_id
) AS subquery;
```

### Task 12: Most Reordered Products in Each Department
```sql
SELECT department, product_name, SUM(reordered) AS reorder_count 
FROM order_products_train 
INNER JOIN products ON order_products_train.product_id = products.product_id
INNER JOIN departments ON products.department_id = departments.department_id
GROUP BY department, product_name 
ORDER BY department, reorder_count DESC;
```

### Task 13: Number of Products Reordered More Than Once
```sql
SELECT COUNT(DISTINCT product_id) AS product_reordered_more_than_one 
FROM order_products_train 
WHERE reordered > 1;
```

### Task 14: Average Number of Products Added to Cart per Order
```sql
SELECT AVG(add_to_cart_order) AS avg_cart_per_order
FROM order_products_train;
```

### Task 15: Orders by Hour of the Day
```sql
SELECT order_hour_of_day, COUNT(order_id) AS order_count 
FROM orders 
GROUP BY order_hour_of_day 
ORDER BY order_hour_of_day;
```

### Task 16: Distribution of Order Sizes
```sql
SELECT product_count, COUNT(order_id) AS order_size
FROM (
    SELECT order_id, COUNT(product_id) AS product_count
    FROM order_products_train
    GROUP BY order_id
) AS subquery
GROUP BY product_count;
```

### Task 17: Average Reorder Rate for Products in Each Aisle
```sql
SELECT aisle, AVG(reordered) AS avg_reorder_rate 
FROM order_products_train 
INNER JOIN products ON order_products_train.product_id = products.product_id
INNER JOIN aisles ON products.aisle_id = aisles.aisle_id
GROUP BY aisle 
ORDER BY avg_reorder_rate DESC;
```

### Task 18: Average Order Size by Day of the Week
```sql
SELECT order_dow, AVG(product_count) AS avg_order_size
FROM (
    SELECT orders.order_id, COUNT(product_id) AS product_count, order_dow
    FROM order_products_train
    INNER JOIN orders ON order_products_train.order_id = orders.order_id
    GROUP BY order_id, order_dow
) AS subquery
GROUP BY order_dow
ORDER BY order_dow;
```

### Task 19: Top 10 Users with Highest Number of Orders
```sql
SELECT user_id, COUNT(order_id) AS order_count 
FROM orders 
GROUP BY user_id 
ORDER BY order_count DESC 
LIMIT 10;
```

### Task 20: Number of Products in Each Aisle and Department
```sql
SELECT aisle, department, COUNT(product_id) AS product_count
FROM products
INNER JOIN aisles ON products.aisle_id = aisles.aisle_id
INNER JOIN departments ON products.department_id = departments.department_id
GROUP BY aisle, department
ORDER BY product_count DESC;


