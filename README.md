

# SQL (Structured Query Language)


Welcome to the SQL Learning Repository! This repository is a comprehensive guide to Structured Query Language (SQL). Whether you're a beginner or an experienced developer, you'll find valuable information, practical examples, and curated resources to master SQL for real-world applications.

## Why Learn SQL?

SQL is the standard language for interacting with relational databases. It is essential for:
- Data analysis and reporting
- Backend and full-stack development
- Business intelligence
- Data engineering and data science

Learning SQL empowers you to extract insights from data, automate workflows, and build robust applications.


## Table of Contents

- [Introduction to SQL](#introduction-to-sql)
- [Database Design Fundamentals](#database-design-fundamentals)
- [Data Types](#data-types)
- [SQL Basics](#sql-basics)
- [Intermediate SQL](#intermediate-sql)
- [Advanced SQL](#advanced-sql)
- [Complex Query Patterns](#complex-query-patterns)
- [Performance Optimization](#performance-optimization)
- [Database Security](#database-security)
- [Real-World Scenarios](#real-world-scenarios)
- [Best Practices](#best-practices)
- [Learning Resources](#learning-resources)



## Introduction to SQL

Structured Query Language (SQL) is a domain-specific language for managing and manipulating relational databases. SQL allows you to:
- Query data (retrieve, filter, sort, aggregate)
- Insert, update, and delete records
- Define and modify database schemas
- Control access and permissions

SQL is supported by popular database systems like MySQL, PostgreSQL, SQLite, SQL Server, and Oracle.

### SQL Standards and Dialects

SQL follows ANSI/ISO standards, but each database system has its own dialect:
- **MySQL**: Known for web applications, supports JSON data type
- **PostgreSQL**: Advanced open-source database with array and JSON support
- **SQL Server**: Microsoft's enterprise database with T-SQL extensions
- **Oracle**: Enterprise database with PL/SQL procedural language
- **SQLite**: Lightweight, file-based database perfect for embedded applications

## Database Design Fundamentals

### Database Normalization

Normalization reduces data redundancy and improves data integrity:

**1st Normal Form (1NF):**
- Each column contains atomic (indivisible) values
- No repeating groups

**2nd Normal Form (2NF):**
- Must be in 1NF
- All non-key attributes depend on the entire primary key

**3rd Normal Form (3NF):**
- Must be in 2NF
- No transitive dependencies (non-key attributes don't depend on other non-key attributes)

**Boyce-Codd Normal Form (BCNF):**
- Stricter version of 3NF
- Every determinant must be a candidate key

### Entity-Relationship Diagrams (ERD)

ERDs visualize database structure:
- **Entities**: Objects or concepts (tables)
- **Attributes**: Properties of entities (columns)
- **Relationships**: Connections between entities
  - One-to-One (1:1)
  - One-to-Many (1:M)
  - Many-to-Many (M:M)

### ACID Properties

Essential properties of database transactions:
- **Atomicity**: All or nothing execution
- **Consistency**: Database remains in valid state
- **Isolation**: Transactions don't interfere with each other
- **Durability**: Committed changes persist even after system failure

## Data Types

Understanding data types is crucial for accurate data representation and efficient storage. Here are common SQL data types:


### Text Types

| Data Type     | Description                                                  |
|--------------|--------------------------------------------------------------|
| CHAR(size)   | Fixed-length string. Max size: 255 characters.               |
| VARCHAR(size)| Variable-length string. Max size: 65,535 characters.         |
| TINYTEXT     | String, max 255 characters.                                 |
| TEXT         | String, max 65,535 characters.                              |
| MEDIUMTEXT   | String, max 16,777,215 characters.                          |
| LONGTEXT     | String, max 4,294,967,295 characters.                       |


### Number Types

| Data Type      | Description                                                  |
|---------------|--------------------------------------------------------------|
| TINYINT(size)  | -128 to 127 (signed), 0 to 255 (unsigned).                  |
| SMALLINT(size) | -32,768 to 32,767 (signed), 0 to 65,535 (unsigned).         |
| MEDIUMINT(size)| -8,388,608 to 8,388,607 (signed), 0 to 16,777,215 (unsigned)|
| INT(size)      | -2,147,483,648 to 2,147,483,647 (signed).                   |
| BIGINT(size)   | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807.    |
| DECIMAL(p,s)   | Fixed-point number.                                         |
| FLOAT, DOUBLE  | Floating-point numbers.                                     |


### Date and Time Types

| Data Type   | Description                                                  |
|-------------|--------------------------------------------------------------|
| DATE        | Date (YYYY-MM-DD).                                           |
| TIME        | Time (HH:MM:SS).                                             |
| DATETIME    | Date and time (YYYY-MM-DD HH:MM:SS).                         |
| TIMESTAMP   | Unix timestamp.                                              |
| YEAR        | Year (YYYY or YY).                                           |

### Other Types

| Data Type | Description                       |
|-----------|-----------------------------------|
| BOOLEAN   | True/False (0 or 1).              |
| BLOB      | Binary Large Object (files, etc). |
| ENUM      | Enumeration, one value from list. |




## SQL Basics

### Creating a Table
```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    hire_date DATE
);
```

### Inserting Data
```sql
INSERT INTO employees (employee_id, first_name, last_name, hire_date)
VALUES (1, 'John', 'Doe', '2022-01-15');
```

### SELECT Statements: Retrieving Data
```sql
SELECT first_name, last_name
FROM employees;
```

### Filtering Rows
Retrieve customers from the "Customers" table who are located in "Dhaka":
```sql
SELECT * FROM customers 
WHERE City = 'Dhaka';
```

### Filtering with LIKE
Retrieve addresses from the "customers" table with address containing the word "Dhaka":
```sql
SELECT * FROM customers 
WHERE address LIKE '%Dhaka%';
```

### Sorting Results
Retrieve the names of customers from the "Customers" table, sorted alphabetically by their last names:
```sql
SELECT CustomerName 
FROM Customers 
ORDER BY LastName;
```

### Aggregate Functions
Count the number of orders placed by each customer:
```sql
SELECT customer_id, COUNT(order_id) AS OrderCount 
FROM orders 
GROUP BY customer_id;
```

### Updating Data
```sql
UPDATE employees
SET last_name = 'Smith'
WHERE employee_id = 1;
```

### Deleting Data
```sql
DELETE FROM employees
WHERE employee_id = 1;
```

### Joining Tables
Retrieve customer names and their corresponding order details:

```sql
SELECT c.CustomerName, o.OrderDate, o.TotalAmount
FROM Customers c
JOIN Orders o ON c.CustomerID = o.CustomerID;
```



## Intermediate SQL

### Constraints
- **PRIMARY KEY**: Uniquely identifies each row.
- **FOREIGN KEY**: Enforces referential integrity.
- **UNIQUE**: Ensures all values in a column are unique.
- **NOT NULL**: Ensures a column cannot have NULL values.
- **CHECK**: Ensures values meet a specific condition.

Example:
```sql
CREATE TABLE orders (
  order_id INT PRIMARY KEY,
  customer_id INT,
  order_date DATE,
  CONSTRAINT fk_customer FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);
```

### Indexes
Indexes speed up data retrieval:
```sql
CREATE INDEX idx_lastname ON employees(last_name);
```

### Transactions
Ensure a group of SQL statements execute as a single unit:
```sql
START TRANSACTION;
UPDATE accounts SET balance = balance - 100 WHERE account_id = 1;
UPDATE accounts SET balance = balance + 100 WHERE account_id = 2;
COMMIT;
```

### Views
Virtual tables based on SQL queries:
```sql
CREATE VIEW active_customers AS
SELECT * FROM customers WHERE status = 'active';
```

### Stored Procedures
Reusable SQL code blocks with parameters and control structures:
```sql
DELIMITER //
CREATE PROCEDURE GetCustomerOrderSummary(IN cust_id INT, OUT total_orders INT, OUT total_amount DECIMAL(10,2))
BEGIN
    DECLARE done INT DEFAULT FALSE;
    DECLARE order_amount DECIMAL(10,2);
    DECLARE order_cursor CURSOR FOR 
        SELECT total_amount FROM orders WHERE customer_id = cust_id;
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = TRUE;
    
    SET total_orders = 0;
    SET total_amount = 0.00;
    
    OPEN order_cursor;
    order_loop: LOOP
        FETCH order_cursor INTO order_amount;
        IF done THEN
            LEAVE order_loop;
        END IF;
        SET total_orders = total_orders + 1;
        SET total_amount = total_amount + order_amount;
    END LOOP;
    CLOSE order_cursor;
END//
DELIMITER ;
```

### Triggers
Automatic execution of code in response to database events:
```sql
CREATE TRIGGER update_product_stock
AFTER INSERT ON order_items
FOR EACH ROW
BEGIN
    UPDATE products 
    SET stock_quantity = stock_quantity - NEW.quantity
    WHERE product_id = NEW.product_id;
END;
```

### User-Defined Functions
Custom functions for complex calculations:
```sql
CREATE FUNCTION calculate_discount(price DECIMAL(10,2), customer_type VARCHAR(20))
RETURNS DECIMAL(10,2)
READS SQL DATA
DETERMINISTIC
BEGIN
    DECLARE discount_rate DECIMAL(5,2);
    
    CASE customer_type
        WHEN 'VIP' THEN SET discount_rate = 0.15;
        WHEN 'PREMIUM' THEN SET discount_rate = 0.10;
        WHEN 'REGULAR' THEN SET discount_rate = 0.05;
        ELSE SET discount_rate = 0.00;
    END CASE;
    
    RETURN price * (1 - discount_rate);
END;
```

## Advanced SQL### Window Functions
Powerful analytic functions for advanced data analysis:

**ROW_NUMBER(), RANK(), DENSE_RANK():**
```sql
SELECT 
    product_name, 
    category,
    price,
    ROW_NUMBER() OVER(PARTITION BY category ORDER BY price DESC) AS row_num,
    RANK() OVER(PARTITION BY category ORDER BY price DESC) AS rank_num,
    DENSE_RANK() OVER(PARTITION BY category ORDER BY price DESC) AS dense_rank_num
FROM products;
```

**LAG() and LEAD() for comparing with previous/next rows:**
```sql
SELECT 
    order_date,
    total_amount,
    LAG(total_amount, 1) OVER(ORDER BY order_date) AS prev_amount,
    LEAD(total_amount, 1) OVER(ORDER BY order_date) AS next_amount,
    total_amount - LAG(total_amount, 1) OVER(ORDER BY order_date) AS amount_change
FROM orders;
```

**Running totals and moving averages:**
```sql
SELECT 
    order_date,
    daily_sales,
    SUM(daily_sales) OVER(ORDER BY order_date ROWS UNBOUNDED PRECEDING) AS running_total,
    AVG(daily_sales) OVER(ORDER BY order_date ROWS 6 PRECEDING) AS moving_avg_7days
FROM daily_sales_summary;
```### Common Table Expressions (CTE)
Create a CTE to calculate the total sales for each product category:
```sql
WITH CategorySales AS (
  SELECT Category, SUM(Price * Quantity) AS TotalSales
  FROM Products
  JOIN OrderDetails ON Products.ProductID = OrderDetails.ProductID
  GROUP BY Category
)
SELECT Category, TotalSales
FROM CategorySales
ORDER BY TotalSales DESC;
```

### Subqueries
- **IN**: Retrieve customers who have placed orders with a total amount greater than the average order amount.
```sql
SELECT CustomerName
FROM Customers
WHERE CustomerID IN (
  SELECT CustomerID
  FROM Orders
  WHERE TotalAmount > (
    SELECT AVG(TotalAmount) FROM Orders
  )
);
```

- **EXISTS**: Retrieve customers who have placed at least one order.
```sql
SELECT CustomerName 
FROM Customers 
WHERE EXISTS (
    SELECT * 
    FROM Orders 
    WHERE Customers.CustomerID = Orders.CustomerID
);
```

### Recursive Queries
Using CTEs for hierarchical data:
```sql
WITH RECURSIVE employee_hierarchy AS (
    -- Base case: top-level managers
    SELECT employee_id, name, manager_id, 1 as level
    FROM employees
    WHERE manager_id IS NULL
    
    UNION ALL
    
    -- Recursive case: employees with managers
    SELECT e.employee_id, e.name, e.manager_id, eh.level + 1
    FROM employees e
    INNER JOIN employee_hierarchy eh ON e.manager_id = eh.employee_id
)
SELECT * FROM employee_hierarchy ORDER BY level, name;
```

### Pivot and Unpivot Operations
Transforming row data to columns and vice versa:
```sql
-- Pivot example (MySQL 8.0+)
SELECT *
FROM (
    SELECT customer_id, month, sales_amount
    FROM monthly_sales
) AS source_table
PIVOT (
    SUM(sales_amount)
    FOR month IN ('Jan', 'Feb', 'Mar', 'Apr')
) AS pivot_table;
```

## Complex Query Patterns

### Data Warehousing Queries

**Star Schema Queries:**
```sql
SELECT 
    d.year,
    d.quarter,
    p.category,
    c.region,
    SUM(f.sales_amount) AS total_sales,
    COUNT(f.transaction_id) AS transaction_count,
    AVG(f.sales_amount) AS avg_transaction
FROM fact_sales f
JOIN dim_date d ON f.date_key = d.date_key
JOIN dim_product p ON f.product_key = p.product_key
JOIN dim_customer c ON f.customer_key = c.customer_key
WHERE d.year = 2024
GROUP BY d.year, d.quarter, p.category, c.region
HAVING SUM(f.sales_amount) > 100000
ORDER BY total_sales DESC;
```

### Advanced Aggregations

**ROLLUP and CUBE for multi-level aggregations:**
```sql
-- ROLLUP provides hierarchical totals
SELECT 
    COALESCE(region, 'All Regions') AS region,
    COALESCE(product_category, 'All Categories') AS category,
    SUM(sales_amount) AS total_sales
FROM sales_data
GROUP BY ROLLUP(region, product_category);

-- CUBE provides all possible combinations
SELECT 
    COALESCE(region, 'All Regions') AS region,
    COALESCE(product_category, 'All Categories') AS category,
    COALESCE(sales_person, 'All Salespeople') AS salesperson,
    SUM(sales_amount) AS total_sales
FROM sales_data
GROUP BY CUBE(region, product_category, sales_person);
```

### Complex Join Patterns

**Self-joins for hierarchical relationships:**
```sql
SELECT 
    emp.name AS employee,
    mgr.name AS manager,
    emp.salary,
    mgr.salary AS manager_salary
FROM employees emp
LEFT JOIN employees mgr ON emp.manager_id = mgr.employee_id;
```

**Multiple table joins with conditions:**
```sql
SELECT 
    c.customer_name,
    o.order_date,
    p.product_name,
    oi.quantity,
    oi.unit_price,
    (oi.quantity * oi.unit_price) AS line_total
FROM customers c
INNER JOIN orders o ON c.customer_id = o.customer_id
INNER JOIN order_items oi ON o.order_id = oi.order_id
INNER JOIN products p ON oi.product_id = p.product_id
WHERE o.order_date >= DATE_SUB(CURRENT_DATE, INTERVAL 30 DAY)
  AND c.status = 'active'
ORDER BY c.customer_name, o.order_date;
```

## Performance Optimization

### Query Optimization Techniques

1. **Use EXPLAIN to analyze query execution:**
```sql
EXPLAIN SELECT * FROM large_table WHERE indexed_column = 'value';
```

2. **Proper indexing strategies:**
```sql
-- Composite index for multiple column searches
CREATE INDEX idx_customer_date ON orders(customer_id, order_date);

-- Partial index for filtered queries
CREATE INDEX idx_active_customers ON customers(customer_id) WHERE status = 'active';

-- Covering index to avoid table lookups
CREATE INDEX idx_order_summary ON orders(customer_id, order_date) INCLUDE (total_amount);
```

3. **Query rewriting for better performance:**
```sql
-- Instead of IN with subquery
SELECT * FROM customers 
WHERE customer_id IN (SELECT customer_id FROM orders WHERE order_date > '2024-01-01');

-- Use EXISTS for better performance
SELECT * FROM customers c
WHERE EXISTS (SELECT 1 FROM orders o WHERE o.customer_id = c.customer_id AND o.order_date > '2024-01-01');
```

### Database Partitioning

**Range partitioning by date:**
```sql
CREATE TABLE sales_data (
    id INT,
    sale_date DATE,
    amount DECIMAL(10,2)
)
PARTITION BY RANGE (YEAR(sale_date)) (
    PARTITION p2022 VALUES LESS THAN (2023),
    PARTITION p2023 VALUES LESS THAN (2024),
    PARTITION p2024 VALUES LESS THAN (2025),
    PARTITION p_future VALUES LESS THAN MAXVALUE
);
```

## Database Security

### User Management and Privileges

```sql
-- Create users with specific privileges
CREATE USER 'app_user'@'localhost' IDENTIFIED BY 'secure_password';
GRANT SELECT, INSERT, UPDATE ON company_db.* TO 'app_user'@'localhost';

-- Create read-only user for reporting
CREATE USER 'report_user'@'%' IDENTIFIED BY 'report_password';
GRANT SELECT ON company_db.* TO 'report_user'@'%';

-- Revoke privileges
REVOKE DELETE ON company_db.* FROM 'app_user'@'localhost';
```

### Data Encryption and Security

```sql
-- Encrypt sensitive data
CREATE TABLE customer_sensitive (
    customer_id INT PRIMARY KEY,
    encrypted_ssn VARBINARY(255),
    encrypted_credit_card VARBINARY(255)
);

-- Insert encrypted data
INSERT INTO customer_sensitive VALUES (
    1, 
    AES_ENCRYPT('123-45-6789', 'encryption_key'),
    AES_ENCRYPT('4111-1111-1111-1111', 'encryption_key')
);

-- Decrypt data (be careful with this in production)
SELECT 
    customer_id,
    AES_DECRYPT(encrypted_ssn, 'encryption_key') AS ssn,
    CONCAT('****-****-****-', RIGHT(AES_DECRYPT(encrypted_credit_card, 'encryption_key'), 4)) AS masked_card
FROM customer_sensitive;
```

## Real-World Scenarios

### E-commerce Analytics

**Customer Lifetime Value calculation:**
```sql
WITH customer_metrics AS (
    SELECT 
        c.customer_id,
        c.registration_date,
        COUNT(DISTINCT o.order_id) AS total_orders,
        SUM(o.total_amount) AS total_spent,
        MAX(o.order_date) AS last_order_date,
        DATEDIFF(CURRENT_DATE, c.registration_date) AS days_as_customer
    FROM customers c
    LEFT JOIN orders o ON c.customer_id = o.customer_id
    GROUP BY c.customer_id, c.registration_date
),
clv_calculation AS (
    SELECT 
        *,
        total_spent / NULLIF(days_as_customer, 0) * 365 AS estimated_annual_value,
        CASE 
            WHEN total_orders >= 10 AND total_spent >= 1000 THEN 'VIP'
            WHEN total_orders >= 5 AND total_spent >= 500 THEN 'Premium'
            WHEN total_orders >= 1 THEN 'Regular'
            ELSE 'Inactive'
        END AS customer_segment
    FROM customer_metrics
)
SELECT 
    customer_segment,
    COUNT(*) AS customer_count,
    AVG(total_spent) AS avg_spent,
    AVG(estimated_annual_value) AS avg_annual_value
FROM clv_calculation
GROUP BY customer_segment
ORDER BY avg_annual_value DESC;
```

### Financial Reporting

**Monthly revenue analysis with growth rates:**
```sql
WITH monthly_revenue AS (
    SELECT 
        DATE_FORMAT(order_date, '%Y-%m') AS month_year,
        SUM(total_amount) AS monthly_revenue
    FROM orders
    WHERE order_date >= DATE_SUB(CURRENT_DATE, INTERVAL 24 MONTH)
    GROUP BY DATE_FORMAT(order_date, '%Y-%m')
),
revenue_with_growth AS (
    SELECT 
        month_year,
        monthly_revenue,
        LAG(monthly_revenue) OVER (ORDER BY month_year) AS prev_month_revenue,
        ((monthly_revenue - LAG(monthly_revenue) OVER (ORDER BY month_year)) / 
         LAG(monthly_revenue) OVER (ORDER BY month_year)) * 100 AS month_over_month_growth
    FROM monthly_revenue
)
SELECT 
    month_year,
    FORMAT(monthly_revenue, 2) AS formatted_revenue,
    ROUND(month_over_month_growth, 2) AS growth_percentage,
    CASE 
        WHEN month_over_month_growth > 10 THEN 'High Growth'
        WHEN month_over_month_growth > 0 THEN 'Positive Growth'
        WHEN month_over_month_growth = 0 THEN 'Flat'
        ELSE 'Decline'
    END AS growth_category
FROM revenue_with_growth
ORDER BY month_year;
```

## Modern SQL Features and Extensions

### JSON Support in SQL

Modern databases support JSON data types for flexible schema design:

**MySQL JSON Functions:**
```sql
-- Create table with JSON column
CREATE TABLE products (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    attributes JSON
);

-- Insert JSON data
INSERT INTO products (id, name, attributes) VALUES
(1, 'Laptop', '{"brand": "Dell", "ram": "16GB", "storage": "512GB SSD"}'),
(2, 'Phone', '{"brand": "Apple", "model": "iPhone 13", "color": "Blue"}');

-- Query JSON data
SELECT name, 
       JSON_EXTRACT(attributes, '$.brand') AS brand,
       JSON_EXTRACT(attributes, '$.ram') AS ram
FROM products
WHERE JSON_EXTRACT(attributes, '$.brand') = 'Dell';

-- Update JSON data
UPDATE products 
SET attributes = JSON_SET(attributes, '$.price', 999.99)
WHERE id = 1;
```

**PostgreSQL JSONB Operations:**
```sql
-- JSONB provides better performance than JSON
CREATE TABLE events (
    id SERIAL PRIMARY KEY,
    event_data JSONB
);

-- Insert JSONB data
INSERT INTO events (event_data) VALUES
('{"user_id": 123, "action": "login", "timestamp": "2024-01-15T10:30:00Z", "metadata": {"ip": "192.168.1.1"}}');

-- Query with JSONB operators
SELECT * FROM events 
WHERE event_data @> '{"action": "login"}';

-- Create indexes on JSONB fields
CREATE INDEX idx_user_actions ON events USING GIN ((event_data->'action'));
```

### Array Data Types

PostgreSQL supports array data types for storing multiple values:

```sql
-- Create table with array columns
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    tags TEXT[],
    prices NUMERIC(10,2)[]
);

-- Insert array data
INSERT INTO products (name, tags, prices) VALUES
('Laptop', ARRAY['electronics', 'computers', 'portable'], ARRAY[999.99, 1199.99, 1499.99]);

-- Query array data
SELECT * FROM products 
WHERE 'electronics' = ANY(tags);

-- Array functions
SELECT name, 
       array_length(tags, 1) AS tag_count,
       unnest(prices) AS individual_prices
FROM products;
```

### Temporal Tables and Time Travel

SQL Server and other databases support temporal tables for historical data tracking:

```sql
-- Create temporal table (SQL Server)
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    department VARCHAR(50),
    salary DECIMAL(10,2),
    -- System-versioned columns
    valid_from DATETIME2 GENERATED ALWAYS AS ROW START,
    valid_to DATETIME2 GENERATED ALWAYS AS ROW END,
    PERIOD FOR SYSTEM_TIME (valid_from, valid_to)
)
WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.employees_history));

-- Query historical data
SELECT * FROM employees 
FOR SYSTEM_TIME AS OF '2024-01-01';

-- Query data changes over time
SELECT * FROM employees 
FOR SYSTEM_TIME BETWEEN '2024-01-01' AND '2024-12-31';
```

### Advanced Analytics with SQL

**Percentile and Statistical Functions:**
```sql
-- Calculate percentiles and statistical measures
SELECT 
    department,
    AVG(salary) AS avg_salary,
    PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY salary) AS median_salary,
    PERCENTILE_CONT(0.25) WITHIN GROUP (ORDER BY salary) AS q1_salary,
    PERCENTILE_CONT(0.75) WITHIN GROUP (ORDER BY salary) AS q3_salary,
    STDDEV(salary) AS salary_stddev,
    VAR(salary) AS salary_variance
FROM employees
GROUP BY department;
```

**Time Series Analysis:**
```sql
-- Moving averages and trend analysis
WITH daily_sales AS (
    SELECT 
        DATE(order_date) AS sale_date,
        SUM(total_amount) AS daily_revenue
    FROM orders
    GROUP BY DATE(order_date)
),
sales_with_trends AS (
    SELECT 
        sale_date,
        daily_revenue,
        AVG(daily_revenue) OVER (
            ORDER BY sale_date 
            ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
        ) AS seven_day_avg,
        LAG(daily_revenue, 7) OVER (ORDER BY sale_date) AS revenue_week_ago,
        (daily_revenue - LAG(daily_revenue, 7) OVER (ORDER BY sale_date)) / 
         LAG(daily_revenue, 7) OVER (ORDER BY sale_date) * 100 AS week_over_week_growth
    FROM daily_sales
)
SELECT * FROM sales_with_trends
WHERE sale_date >= CURRENT_DATE - INTERVAL '30' DAY
ORDER BY sale_date;
```

### Graph Queries and Hierarchical Data

**Recursive CTEs for Organization Charts:**
```sql
-- Complex hierarchical query with level and path tracking
WITH RECURSIVE org_chart AS (
    -- Base case: CEO and top executives
    SELECT 
        employee_id,
        name,
        manager_id,
        title,
        1 AS level,
        CAST(name AS VARCHAR(1000)) AS path,
        ARRAY[employee_id] AS id_path
    FROM employees
    WHERE manager_id IS NULL
    
    UNION ALL
    
    -- Recursive case: all other employees
    SELECT 
        e.employee_id,
        e.name,
        e.manager_id,
        e.title,
        oc.level + 1,
        oc.path || ' -> ' || e.name,
        oc.id_path || e.employee_id
    FROM employees e
    INNER JOIN org_chart oc ON e.manager_id = oc.employee_id
    WHERE e.employee_id != ALL(oc.id_path) -- Prevent cycles
)
SELECT 
    REPEAT('  ', level - 1) || name AS indented_name,
    title,
    level,
    path,
    array_length(id_path, 1) AS path_length
FROM org_chart
ORDER BY level, name;
```

### Database Sharding and Federation

**Horizontal Partitioning Strategies:**
```sql
-- Range-based sharding example
-- Shard 1: customers with ID 1-1000000
CREATE TABLE customers_shard_1 (
    customer_id INT CHECK (customer_id BETWEEN 1 AND 1000000),
    -- other columns
) INHERITS (customers_master);

-- Shard 2: customers with ID 1000001-2000000
CREATE TABLE customers_shard_2 (
    customer_id INT CHECK (customer_id BETWEEN 1000001 AND 2000000),
    -- other columns
) INHERITS (customers_master);

-- Function to determine shard
CREATE OR REPLACE FUNCTION get_customer_shard(cid INT) 
RETURNS TEXT AS $$
BEGIN
    IF cid BETWEEN 1 AND 1000000 THEN
        RETURN 'customers_shard_1';
    ELSIF cid BETWEEN 1000001 AND 2000000 THEN
        RETURN 'customers_shard_2';
    ELSE
        RETURN 'customers_shard_default';
    END IF;
END;
$$ LANGUAGE plpgsql;
```

### Machine Learning Integration

**PostgreSQL with ML Extensions:**
```sql
-- Using MADlib for machine learning
-- Linear regression example
SELECT madlib.linregr_train(
    'sales_data',           -- source table
    'sales_model',          -- output model table
    'revenue',              -- dependent variable
    'ARRAY[1, advertising_spend, season_factor]'  -- independent variables
);

-- Predict using the model
SELECT 
    customer_id,
    madlib.linregr_predict(
        coefficients,
        ARRAY[1, 500, 1.2]  -- new data point
    ) AS predicted_revenue
FROM sales_model, customer_data;
```

**SQL Server Machine Learning Services:**
```sql
-- R integration example
EXEC sp_execute_external_script
    @language = N'R',
    @script = N'
        # Perform clustering
        library(cluster)
        customer_clusters <- kmeans(InputDataSet[,2:4], centers = 3)
        OutputDataSet <- data.frame(
            customer_id = InputDataSet$customer_id,
            cluster = customer_clusters$cluster
        )',
    @input_data_1 = N'SELECT customer_id, total_spent, order_frequency, avg_order_value FROM customer_metrics',
    @output_data_1_name = N'OutputDataSet';
```

## Database Administration and Monitoring

### Database Backup and Recovery

**MySQL Backup Strategies:**
```sql
-- Create full backup
mysqldump --single-transaction --routines --triggers company_db > backup.sql

-- Point-in-time recovery setup
SET GLOBAL binlog_format = 'ROW';
SHOW BINARY LOGS;

-- Restore from backup
mysql company_db < backup.sql
```

**PostgreSQL Backup with pg_dump:**
```bash
# Full database backup
pg_dump -h localhost -U postgres -d company_db -f backup.sql

# Backup with custom format for faster restore
pg_dump -h localhost -U postgres -d company_db -Fc -f backup.dump

# Restore
pg_restore -h localhost -U postgres -d company_db_restored backup.dump
```

### Performance Monitoring Queries

**MySQL Performance Analysis:**
```sql
-- Query performance analysis
SELECT 
    query_id,
    exec_count,
    avg_timer_wait/1000000000 AS avg_exec_time_sec,
    sum_timer_wait/1000000000 AS total_exec_time_sec,
    SUBSTRING(digest_text, 1, 100) AS query_sample
FROM performance_schema.events_statements_summary_by_digest
ORDER BY sum_timer_wait DESC
LIMIT 10;

-- Index usage analysis
SELECT 
    t.table_schema,
    t.table_name,
    s.index_name,
    s.cardinality,
    s.seq_in_index
FROM information_schema.tables t
LEFT JOIN information_schema.statistics s ON t.table_name = s.table_name
WHERE t.table_schema = 'company_db'
ORDER BY t.table_name, s.seq_in_index;

-- Connection and thread monitoring
SELECT 
    id,
    user,
    host,
    db,
    command,
    time,
    state,
    SUBSTRING(info, 1, 100) AS query_sample
FROM information_schema.processlist
WHERE command != 'Sleep'
ORDER BY time DESC;
```

**PostgreSQL System Monitoring:**
```sql
-- Query performance statistics
SELECT 
    query,
    calls,
    total_time,
    mean_time,
    rows
FROM pg_stat_statements
ORDER BY total_time DESC
LIMIT 10;

-- Table and index usage
SELECT 
    schemaname,
    tablename,
    seq_scan,
    seq_tup_read,
    idx_scan,
    idx_tup_fetch,
    n_tup_ins,
    n_tup_upd,
    n_tup_del
FROM pg_stat_user_tables
ORDER BY seq_scan DESC;

-- Database size and growth
SELECT 
    datname,
    pg_size_pretty(pg_database_size(datname)) AS size,
    pg_database_size(datname) AS size_bytes
FROM pg_database
WHERE datistemplate = false
ORDER BY pg_database_size(datname) DESC;
```

### Automated Database Maintenance

**MySQL Maintenance Scripts:**
```sql
-- Optimize tables
OPTIMIZE TABLE customers, orders, order_items;

-- Analyze table statistics
ANALYZE TABLE customers, orders, order_items;

-- Check table integrity
CHECK TABLE customers, orders, order_items;

-- Update table statistics
UPDATE mysql.innodb_table_stats SET n_rows = (
    SELECT COUNT(*) FROM customers
) WHERE table_name = 'customers';
```

**PostgreSQL Vacuum and Analyze:**
```sql
-- Manual vacuum and analyze
VACUUM ANALYZE customers;

-- Reindex for performance
REINDEX INDEX idx_customer_email;
REINDEX TABLE orders;

-- Update statistics
ANALYZE customers;

-- Check for bloated tables
SELECT 
    schemaname,
    tablename,
    pg_size_pretty(pg_total_relation_size(schemaname||'.'||tablename)) AS size,
    pg_size_pretty(pg_relation_size(schemaname||'.'||tablename)) AS table_size,
    pg_size_pretty(pg_total_relation_size(schemaname||'.'||tablename) - pg_relation_size(schemaname||'.'||tablename)) AS index_size
FROM pg_tables
WHERE schemaname NOT IN ('information_schema', 'pg_catalog')
ORDER BY pg_total_relation_size(schemaname||'.'||tablename) DESC;
```

### Database Security Hardening

**Access Control and Auditing:**
```sql
-- Create application-specific users
CREATE USER 'app_read_only'@'app-server.company.com' IDENTIFIED BY 'complex_password';
GRANT SELECT ON company_db.* TO 'app_read_only'@'app-server.company.com';

-- Audit trail table
CREATE TABLE audit_log (
    id INT AUTO_INCREMENT PRIMARY KEY,
    table_name VARCHAR(64),
    operation ENUM('INSERT', 'UPDATE', 'DELETE'),
    user_name VARCHAR(64),
    timestamp DATETIME DEFAULT CURRENT_TIMESTAMP,
    old_values JSON,
    new_values JSON
);

-- Audit trigger example
CREATE TRIGGER customer_audit
AFTER UPDATE ON customers
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (table_name, operation, user_name, old_values, new_values)
    VALUES ('customers', 'UPDATE', USER(), 
            JSON_OBJECT('name', OLD.name, 'email', OLD.email),
            JSON_OBJECT('name', NEW.name, 'email', NEW.email));
END;
```

**Data Masking for Development:**
```sql
-- Create masked copy of production data
CREATE TABLE customers_dev AS
SELECT 
    customer_id,
    CONCAT('Customer_', customer_id) AS name,
    CONCAT('user', customer_id, '@example.com') AS email,
    LEFT(phone, 3) + '-XXX-XXXX' AS phone,
    'XXX-XX-' + RIGHT(ssn, 4) AS ssn,
    registration_date,
    status
FROM customers_prod;
```

## Best Practices### Database Design
- Use meaningful and consistent naming conventions
- Normalize your database appropriately (usually 3NF)
- Choose appropriate data types to save space
- Use foreign keys to maintain referential integrity
- Document your database schema

### Query Writing
- Avoid using SELECT * in production queries
- Use specific column names for better performance
- Write readable queries with proper formatting and comments
- Use parameterized queries to prevent SQL injection
- Test queries with realistic data volumes

### Performance
- Create indexes on frequently queried columns
- Use EXPLAIN to analyze query execution plans
- Avoid unnecessary JOINs and subqueries
- Use LIMIT when appropriate to reduce result sets
- Consider query caching for frequently executed queries

### Security
- Never store passwords in plain text
- Use the principle of least privilege for database users
- Regularly update database software
- Encrypt sensitive data both in transit and at rest
- Audit database access and modifications

### Maintenance
- Regular database backups and recovery testing
- Monitor database performance metrics
- Archive old data to maintain performance
- Plan for database growth and scaling
- Document database procedures and policies

## Learning Resources

### Books
**Beginner Level:**
- *SQL For Dummies* by Allen G. Taylor
- *Learning SQL* by Alan Beaulieu
- *SQL in 10 Minutes, Sams Teach Yourself* by Ben Forta

**Intermediate Level:**
- *SQL Cookbook* by Anthony Molinaro
- *Effective SQL* by John Viescas
- *SQL Performance Explained* by Markus Winand

**Advanced Level:**
- *The Art of SQL* by Stéphane Faroult
- *High Performance MySQL* by Baron Schwartz
- *PostgreSQL: Up and Running* by Regina Obe

### Online Courses
**Free Courses:**
- [Khan Academy: Intro to SQL](https://www.khanacademy.org/computing/computer-programming/sql)
- [freeCodeCamp: Relational Database Course](https://www.freecodecamp.org/learn/relational-database/)
- [W3Schools SQL Tutorial](https://www.w3schools.com/sql/)

**Paid Courses:**
- [Codecademy: Learn SQL](https://www.codecademy.com/learn/learn-sql)
- [Coursera: Databases and SQL for Data Science](https://www.coursera.org/learn/sql-data-science)
- [Udemy: The Complete SQL Bootcamp](https://www.udemy.com/course/the-complete-sql-bootcamp/)
- [DataCamp: Introduction to SQL](https://www.datacamp.com/courses/introduction-to-sql)

### Practice Platforms
**Coding Challenges:**
- [LeetCode SQL Problems](https://leetcode.com/problemset/database/)
- [HackerRank SQL Practice](https://www.hackerrank.com/domains/sql)
- [Codewars SQL Kata](https://www.codewars.com/collections/sql)
- [SQLBolt Interactive Lessons](https://sqlbolt.com/)

**Interactive Learning:**
- [SQLZoo](https://sqlzoo.net/)
- [W3Resource SQL Exercises](https://www.w3resource.com/sql-exercises/)
- [Mode Analytics SQL Tutorial](https://mode.com/sql-tutorial/)
- [Select Star SQL](https://selectstarsql.com/)

### Tools and Software
**Database Management Systems:**
- [MySQL Community Server](https://dev.mysql.com/downloads/mysql/)
- [PostgreSQL](https://www.postgresql.org/download/)
- [SQLite](https://www.sqlite.org/download.html)
- [Microsoft SQL Server Express](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)

**Database Administration Tools:**
- [phpMyAdmin](https://www.phpmyadmin.net/) (MySQL)
- [pgAdmin](https://www.pgadmin.org/) (PostgreSQL)
- [DBeaver](https://dbeaver.io/) (Universal)
- [MySQL Workbench](https://www.mysql.com/products/workbench/)
- [DataGrip](https://www.jetbrains.com/datagrip/) (JetBrains)

### Documentation
- [MySQL Documentation](https://dev.mysql.com/doc/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [SQLite Documentation](https://www.sqlite.org/docs.html)

---

Happy learning and querying!
