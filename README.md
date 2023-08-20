
# SQL (Structured Query Language)

Welcome to the SQL Details repository! This repository is your comprehensive guide to all things related to Structured Query Language (SQL). Whether you're a complete beginner or an experienced developer looking to deepen your SQL knowledge, you'll find valuable information, examples, and resources here.

## Table of Contents

- [Introduction to SQL](#introduction-to-sql)
- [Data Types](#data-types)
- [SQL Basics](#sql-basics)
- [Advanced SQL](#advanced-sql)


## Introduction to SQL

Structured Query Language (SQL) is a domain-specific language used for managing and manipulating relational databases. It provides a standardized way to interact with databases, enabling tasks such as querying data, inserting records, updating information, and more.


## Data Types

Understanding data types is crucial for accurate data representation. In this section explains various data types and their usage in SQL, including:

### Text types

| Data Type   | Description                                                  |
|-------------|--------------------------------------------------------------|
| CHAR(size)  | Holds a fixed length string. Max size: 255 characters.       |
| VARCHAR(size) | Holds a variable length string. Max size: 255 characters.    |
| TINYTEXT    | Holds a string with max length of 255 characters.            |
| TEXT        | Holds a string with max length of 65,535 characters.         |
| ...         | ...                                                          |

### Number types

| Data Type   | Description                                                  |
|-------------|--------------------------------------------------------------|
| TINYINT(size)  | Range: -128 to 127 normal, 0 to 255 UNSIGNED.                |
| SMALLINT(size) | Range: -32768 to 32767 normal, 0 to 65535 UNSIGNED.          |
| MEDIUMINT(size) | Range: -8388608 to 8388607 normal, 0 to 16777215 UNSIGNED.  |
| ...         | ...                                                          |

### Date types

| Data Type   | Description                                                  |
|-------------|--------------------------------------------------------------|
| DATE()      | A date in format YYYY-MM-DD. Range: '1000-01-01' to '9999-12-31'. |
| DATETIME()  | A date and time in format YYYY-MM-DD HH:MI:SS. Range: '1000-01-01 00:00:00' to '9999-12-31 23:59:59'. |
| TIMESTAMP() | A timestamp in seconds since Unix epoch. Range: '1970-01-01 00:00:01' to '2038-01-09 03:14:07'. |
| ...         | ...                                                          |




## SQL Basics


- **SELECT Statements**: Retrieving data from a database.

  Example:
  ```sql
  SELECT first_name, last_name
  FROM employees;
  ```

- **Filtering**: Retrieve customers from the "Customers" table who are located in "Dhaka"

  Example:
  ```sql
  SELECT * FROM customers 
  WHERE City = 'Dhaka';
  ```

- **Filtering with LIKE**: Retrieve addreess from the "customers" table with address containing the word "Dhaka"

  Example:
  ```sql
  SELECT * FROM customers 
  WHERE address like '%Dhaka%';
  ```

- **Sorting Results**: Retrieve the names of customers from the "Customers" table, sorted alphabetically by their last names.

  Example:
  ```sql
  SELECT CustomerName 
  FROM Customers 
  ORDER BY LastName;
  ```

- **Aggregate Function - Count**: Count the number of orders placed by each customer.

  Example:
  ```sql
  SELECT customer_id, COUNT(order_id) AS OrderCount 
  FROM orders 
  GROUP BY customer_id;
  ```

- **Joining Tables**: Retrieve customer names and their corresponding order details.
  Example:
  ```sql
  SELECT c.CustomerName, o.OrderDate, o.TotalAmount
  FROM Customers c
  JOIN Orders o ON c.CustomerID = o.CustomerID;
  ```


## Advanced SQL

- **Window Functions**: Analytic functions for advanced data analysis.

  Example:
  ```sql
  SELECT product_name, price, 
         ROW_NUMBER() OVER(PARTITION BY category ORDER BY price DESC) AS row_num
  FROM products;
  ```

- **Common Table Expression (CTE)**: Create a CTE to calculate the total sales for each product category.
  
  Example:
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

- **Subquery - IN**: Retrieve customers who have placed orders with a total amount greater than the average order amount.

  Example:
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

- **Subquery - EXISTS**: Retrieve customers who have placed at least one order.

  Example:
  ```sql
  SELECT CustomerName 
  FROM Customers 
  WHERE EXISTS (
      SELECT * 
      FROM Orders 
      WHERE Customers.CustomerID = Orders.CustomerID
  );
  ```
