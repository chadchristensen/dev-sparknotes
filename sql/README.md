# SQL

## Table of Contents
1. [Basic Queries](#basic-queries)
* SELECT Statements: How to retrieve data from a database.
* FROM Clause: Understanding tables and how to select them.
* WHERE Clause: Filtering data based on conditions.

2. [Joins](#joins)
* INNER JOIN: Combining rows from two or more tables based on a related column.
* LEFT JOIN: Returning all rows from the left table, and the matched rows from the right table.
* RIGHT JOIN: Returning all rows from the right table, and the matched rows from the left table.
* FULL OUTER JOIN: Returning all rows when there is a match in either left or right table.

3. [Aggregation Functions](#aggregation-functions)
* COUNT(): Counting the number of rows.
* SUM(): Summing the values of a column.
* AVG(): Calculating the average value of a column.
* MAX() and MIN(): Finding the maximum and minimum values.

4. [Grouping Data](#grouping-data)
* GROUP BY: Aggregating data across multiple records.
* HAVING: Filtering groups based on conditions.

5. [Data Manipulation](#data-manipulation)
* INSERT: Adding new rows to a table.
* UPDATE: Modifying existing rows in a table.
* DELETE: Removing rows from a table.

5. [Subqueries](#subqueries)
* Subqueries in SELECT: Using queries within other queries.
* Subqueries in WHERE: Filtering data based on subquery results.

6. [Data Types](#data-types)
* Understanding common data types such as INTEGER, VARCHAR, DATE, etc.

7. [Indexes](#indexes)
* Basics of Indexing: Understanding how indexes work and their importance.
* Creating Indexes: How to create indexes to improve query performance.
* Composite Indexes: Using multiple columns in an index.
* Index Maintenance: Keeping indexes healthy and up-to-date.

8. [Query Optimization](#query-optimization)
* EXPLAIN/EXPLAIN PLAN: Analyzing query execution plans to identify bottlenecks.
* Query Hints: Providing hints to the database engine for better query performance.
* Query Rewrite: Techniques to rewrite queries for better performance.
* Using LIMIT/OFFSET: Efficiently paging through large result sets.

9. [Normalization](#normalization)
* Basic concepts of database normalization and why it is important.
* Denormalization: When and how to denormalize for performance reasons.

10. [Basic Transactions](#basic-transactions)
* BEGIN, COMMIT, ROLLBACK: Understanding transactions and how to ensure data integrity.

11. [Performance Tuning Specifics](#performance-tuning-specifics)
* Avoiding SELECT: Selecting only the necessary columns to reduce data load.
* Reducing Joins: Minimizing the number of joins in queries for better performance.
* Use of Stored Procedures: Using stored procedures to encapsulate complex logic.
* Proper Use of WHERE Clauses: Ensuring conditions are indexed properly.
* Index Scans vs. Table Scans: Understanding the difference and how to avoid full table scans.
* Caching Strategies: Using caching mechanisms to reduce database load.
* Partitioning: Implementing table partitioning to manage large datasets efficiently.

## 1. Basic Queries
Understanding basic queries is foundational to working with SQL databases. Here are the critical components:

1. SELECT Statements

* Syntax: The basic syntax for a SELECT statement is:
	
  ```SQL
  SELECT column1, column2, ...
  FROM table_name;
  ```
* Selecting Specific Columns: It’s essential to know how to select specific columns instead of using SELECT *. For example:
  ```SQL
  SELECT first_name, last_name
  FROM employees;
  ```

2. FROM Clause
   
* Syntax: Specifies the table from which to retrieve the data.
	```SQL
    SELECT column1, column2
    FROM table_name;
	```
* Example:
	```SQL
	SELECT product_name, price
	FROM products;
	```

3. WHERE Clause
   
* Syntax: Used to filter records that meet certain conditions.
	```SQL
	SELECT column1, column2
	FROM table_name
	WHERE condition;
	```
* Operators: Common operators include =, !=, >, <, >=, <=, BETWEEN, LIKE, and IN.
  * Equality:
	```SQL
	SELECT * FROM employees WHERE department = 'Sales';
	```
  * Range:
	```SQL
	SELECT * FROM products WHERE price BETWEEN 10 AND 20;
	```
  * Pattern Matching:
	```SQL
	SELECT * FROM customers WHERE name LIKE 'A%';
	```
  * Set Membership:
	```SQL
	SELECT * FROM orders WHERE status IN ('Shipped', 'Pending');
	```

4. ORDER BY Clause
* Syntax: Used to sort the result set by one or more columns.
	```SQL
  SELECT column1, column2
  FROM table_name
  WHERE condition
  ORDER BY column1 [ASC|DESC];
	```
* Example:
  ```SQL
  SELECT * FROM employees
  WHERE department = 'Sales'
  ORDER BY last_name ASC;
  ```

5. LIMIT Clause
* Syntax: Used to specify the number of records to return.
  ```SQL
  SELECT column1, column2
  FROM table_name
  WHERE condition
  LIMIT number;
  ```
* Example:
  ```SQL
  SELECT * FROM customers
  ORDER BY sign_up_date DESC
  LIMIT 10;
  ```

6. DISTINCT Keyword
* Syntax: Used to return only distinct (different) values.
  
  ```SQL
  SELECT DISTINCT column1, column2
  FROM table_name;
  ```
* Example:
  ```SQL
  SELECT DISTINCT country
  FROM customers;
  ```

7. Aliasing
* Syntax: Used to give a table or a column a temporary name.
  ```SQL
  SELECT column_name AS alias_name
  FROM table_name;
  ```
* Example:
  ```SQL
  SELECT first_name AS 'First Name', last_name AS 'Last Name'
  FROM employees;
  ```

**Summary**

Mastering these basic query elements will provide a solid foundation for more complex SQL operations. These fundamentals are essential for effectively retrieving and manipulating data in a relational database.

## 2. Joins
Joins are used in SQL to combine rows from two or more tables based on a related column between them. Here are the critical types of joins you need to know:

1. INNER JOIN
* **Syntax:** Returns records that have matching values in both tables.
  ```SQL
  SELECT columns
  FROM table1
  INNER JOIN table2
  ON table1.common_column = table2.common_column;
  ```
* **Example:**
  ```SQL
  SELECT employees.first_name, employees.last_name, departments.department_name
  FROM employees
  INNER JOIN departments
  ON employees.department_id = departments.department_id;
  ```

* **Explanation:** This query selects all employees and their respective department names where there is a match between employees.department_id and departments.department_id.

2. LEFT JOIN (or LEFT OUTER JOIN)

* **Syntax**: Returns all records from the left table, and the matched records from the right table. The result is NULL from the right side if there is no match.

  ```SQL
  SELECT columns
  FROM table1
  LEFT JOIN table2
  ON table1.common_column = table2.common_column;
  ```

* **Example:**
  ```SQL
  SELECT employees.first_name, employees.last_name, departments.department_name
  FROM employees
  LEFT JOIN departments
  ON employees.department_id = departments.department_id;
  ```

* **Explanation:** This query returns all employees and their department names. If an employee is not assigned to any department, the department_name will be NULL.

3. RIGHT JOIN (or RIGHT OUTER JOIN)

* **Syntax**: Returns all records from the right table, and the matched records from the left table. The result is NULL from the left side if there is no match.

  ```SQL
  SELECT columns
  FROM table1
  RIGHT JOIN table2
  ON table1.common_column = table2.common_column;
  ```

* **Example:**

  ```SQL
  SELECT employees.first_name, employees.last_name, departments.department_name
  FROM employees
  RIGHT JOIN departments
  ON employees.department_id = departments.department_id;
  ```

* **Explanation:** This query returns all departments and the employees in each department. If a department has no employees, the `first_name` and last_name will be NULL.

4. FULL OUTER JOIN
* **Syntax:** Returns all records when there is a match in either left or right table. Records with no match in left or right tables will be included as well.

  ```SQL
  SELECT columns
  FROM table1
  FULL OUTER JOIN table2
  ON table1.common_column = table2.common_column;
  ```

* **Example:**
  ```SQL
  SELECT employees.first_name, employees.last_name, departments.department_name
  FROM employees
  FULL OUTER JOIN departments
  ON employees.department_id = departments.department_id;
  ```

* **Explanation:** This query returns all employees and all departments, with NULL values in places where there is no match.

5. Self Join
* **Syntax:** A self join is a regular join but the table is joined with itself.

  ```SQL
  SELECT a.column_name, b.column_name
  FROM table1 a, table1 b
  WHERE condition;
  ```

* **Example:**
  ```SQL
  SELECT e1.first_name AS 'Employee', e2.first_name AS 'Manager'
  FROM employees e1
  INNER JOIN employees e2
  ON e1.manager_id = e2.employee_id;
  ```

* **Explanation:** This query lists employees and their managers by joining the employees table with itself.

6. Cross Join

* Syntax: Returns the Cartesian product of the two tables (i.e., every row in the first table is combined with every row in the second table).

  ```SQL
  SELECT columns
  FROM table1
  CROSS JOIN table2;
  ```

* **Example:**

  ```SQL
  SELECT products.product_name, categories.category_name
  FROM products
  CROSS JOIN categories;
  ```

* **Explanation:** This query returns a combination of every product with every category.

**Summary**

Mastering joins is crucial for working with related data stored across multiple tables. Understanding these types of joins and when to use them will significantly enhance your ability to retrieve and analyze data effectively.
## Aggregation Functions

## Grouping Data

## Data Manipulation

## Subqueries

## Data Types

## Indexes

## Query Optimization

## Normalization

## Basic Transactions

## Performance Tuning Specifics



## Notes:
* In Postgres, SERIAL is now 