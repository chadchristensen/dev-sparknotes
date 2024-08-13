# SQL

## Table of Contents
1. [Basic Queries](#1-basic-queries)
* SELECT Statements: How to retrieve data from a database.
* FROM Clause: Understanding tables and how to select them.
* WHERE Clause: Filtering data based on conditions.

2. [Joins](#2-joins)
* INNER JOIN: Combining rows from two or more tables based on a related column.
* LEFT JOIN: Returning all rows from the left table, and the matched rows from the right table.
* RIGHT JOIN: Returning all rows from the right table, and the matched rows from the left table.
* FULL OUTER JOIN: Returning all rows when there is a match in either left or right table.

3. [Aggregation Functions](#3-aggregation-functions)
* COUNT(): Counting the number of rows.
* SUM(): Summing the values of a column.
* AVG(): Calculating the average value of a column.
* MAX() and MIN(): Finding the maximum and minimum values.

4. [Grouping Data](#4-grouping-data)
* GROUP BY: Aggregating data across multiple records.
* HAVING: Filtering groups based on conditions.

5. [Data Manipulation](#5-data-manipulation)
* INSERT: Adding new rows to a table.
* UPDATE: Modifying existing rows in a table.
* DELETE: Removing rows from a table.

6. [Subqueries](#6-subqueries)
* Subqueries in SELECT: Using queries within other queries.
* Subqueries in WHERE: Filtering data based on subquery results.

7. [Data Types](#7-data-types)
* Understanding common data types such as INTEGER, VARCHAR, DATE, etc.

8. [Indexes](#8-indexes)
* Basics of Indexing: Understanding how indexes work and their importance.
* Creating Indexes: How to create indexes to improve query performance.
* Composite Indexes: Using multiple columns in an index.
* Index Maintenance: Keeping indexes healthy and up-to-date.

9. [Query Optimization](#9-query-optimization)
* EXPLAIN/EXPLAIN PLAN: Analyzing query execution plans to identify bottlenecks.
* Query Hints: Providing hints to the database engine for better query performance.
* Query Rewrite: Techniques to rewrite queries for better performance.
* Using LIMIT/OFFSET: Efficiently paging through large result sets.

10. [Normalization](#10-normalization)
* Basic concepts of database normalization and why it is important.
* Denormalization: When and how to denormalize for performance reasons.

11. [Basic Transactions](#11-basic-transactions)
* BEGIN, COMMIT, ROLLBACK: Understanding transactions and how to ensure data integrity.

12. [Performance Tuning Specifics](#12-performance-tuning-specifics)
* Avoiding SELECT *: Selecting only the necessary columns to reduce data load.
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

## 3. Aggregation Functions

Aggregation functions in SQL are used to perform calculations on multiple rows of a table’s column and return a single value. They are often used with the GROUP BY clause to group the results based on one or more columns. Here are the essential aggregation functions you need to know:

1. **COUNT()**
* Purpose: Returns the number of rows that match a specified condition.
* Syntax:
	```SQL
  SELECT COUNT(column_name)
  FROM table_name
  WHERE condition;
  ```

* Example:
  ```SQL
  SELECT COUNT(employee_id)
  FROM employees
  WHERE department_id = 1;
  ```

* Explanation: This query counts the number of employees in department 1.

2. SUM()
* Purpose: Returns the total sum of a numeric column.
* Syntax:
    ```SQL
    SELECT SUM(column_name)
    FROM table_name
    WHERE condition;
    ```

  * Example:
  ```SQL
  SELECT SUM(salary)
  FROM employees
  WHERE department_id = 2;
  ```

* Explanation: This query calculates the total salary for all employees in department 2.

3. AVG()
* **Purpose:** Returns the average value of a numeric column.
* **Syntax:**
	```SQL
	SELECT AVG(column_name)
	FROM table_name
	WHERE condition;
	```

* **Example:**
  	```SQL
   SELECT AVG(salary)
  FROM employees
  WHERE department_id = 3;
  ```

* Explanation: This query calculates the average salary for all employees in department 3.

4. MAX()
* Purpose: Returns the maximum value of a column.
* Syntax:
	```SQL
	SELECT MAX(column_name)
	FROM table_name
	WHERE condition;
	```
* Example: 
	```SQL
	SELECT MAX(salary)
	FROM employees
	WHERE department_id = 4;
	```

* Explanation: This query finds the highest salary in department 4.

5. MIN()	
* Purpose: Returns the minimum value of a column.
* Syntax: 
	```SQL
	SELECT MIN(column_name)
	FROM table_name
	WHERE condition;
	```
* Example:
	```SQL
	SELECT MIN(salary)
	FROM employees
	WHERE department_id = 5;
	```

* Explanation: This query finds the lowest salary in department 5.
  
## 4. Grouping Data

Aggregation functions are often used in conjunction with the `GROUP BY` clause to group the results based on one or more columns.

1. GROUP BY Clause
   * Purpose: Groups rows that have the same values into summary rows, like “find the number of employees in each department”.
   * Syntax:
      ```SQL
      SELECT column1, aggregation_function(column2)
      FROM table_name
      WHERE condition
      GROUP BY column1;
      ```
   * Example:
      ```SQL
      SELECT department_id, COUNT(employee_id)
      FROM employees
      GROUP BY department_id;
      ```

   * Explanation: This query counts the number of employees in each department.

2. Using Aggregate Functions with GROUP BY
   * COUNT(): Counts the number of rows.
     ```SQL
     SELECT department_id, COUNT(employee_id) AS employee_count
     FROM employees
     GROUP BY department_id;
     ```
   * SUM(): Sums the values in a column.
     ```SQL
     SELECT department_id, SUM(salary) AS total_salary
     FROM employees
     GROUP BY department_id;
     ```
   * AVG(): Calculates the average value of a column.
     ```SQL
     SELECT department_id, AVG(salary) AS average_salary
     FROM employees
     GROUP BY department_id;
     ```
   * MAX(): Finds the maximum value in a column.
     ```SQL
     SELECT department_id, MAX(salary) AS highest_salary
     FROM employees
     GROUP BY department_id;
     ```
   * MIN(): Finds the minimum value in a column.
     ```SQL
     SELECT department_id, MIN(salary) AS lowest_salary
     FROM employees
     GROUP BY department_id;
     ```

3. `HAVING` Clause
   * Purpose: Filters records that work on summarized `GROUP BY` results. It’s similar to the `WHERE` clause but used for aggregate functions.
   * Syntax:
     ```SQL
     SELECT column1, aggregate_function(column2)
     FROM table_name
     WHERE condition
     GROUP BY column1
     HAVING aggregate_function(column2) condition;
     ```
   * Example:
     ```SQL
     SELECT department_id, COUNT(employee_id) AS employee_count
     FROM employees
     GROUP BY department_id
     HAVING COUNT(employee_id) > 10;
     ```
  *	Explanation: This query groups employees by department and then filters to show only those departments with more than 10 employees.

1. Combining `GROUP BY` with `ORDER BY`
   * Purpose: You can order the results of your grouped data.
   * Syntax:
     ```SQL
     SELECT column1, aggregate_function(column2)
     FROM table_name
     WHERE condition
     GROUP BY column1
     ORDER BY column1 [ASC|DESC];
     ```
   * Example:
     ```SQL
     SELECT department_id, COUNT(employee_id) AS employee_count
     FROM employees
     GROUP BY department_id
     ORDER BY employee_count DESC;
     ```
   * Explanation: This query groups employees by department, counts them, and then orders the results by the number of employees in descending order.

### Summary

Mastering the `GROUP BY` and `HAVING` clauses in conjunction with aggregate functions is essential for effective data summarization and analysis in SQL. These tools allow you to perform complex queries that can provide valuable insights from your data.


## 5. Data Manipulation

### Data Manipulation

Data manipulation in SQL involves performing operations to modify the data stored in a database. The three primary operations for data manipulation are INSERT, UPDATE, and DELETE.

1. INSERT Statement
  * Purpose: Adds new rows of data to a table.
  * Syntax:
      ```SQL
      INSERT INTO table_name (column1, column2, column3, ...)
      VALUES (value1, value2, value3, ...);
      ```
  * Example:
    ```SQL
    INSERT INTO employees (first_name, last_name, department_id, salary)
    VALUES ('John', 'Doe', 1, 60000);
    ```
  * Explanation: This query inserts a new row into the employees table with the specified values for `first_name`, `last_name`, `department_id`, and `salary`.
  * Inserting Multiple Rows:
    ```SQL
    INSERT INTO employees (first_name, last_name, department_id, salary)
    VALUES 
    ('Jane', 'Smith', 2, 75000),
    ('Bill', 'Jones', 1, 65000),
    ('Mary', 'Brown', 3, 80000);
    ```
  * Explanation: This query inserts multiple rows into the employees table in a single `INSERT` statement.

2. UPDATE Statement
   * Purpose: Modifies existing rows in a table.
   * Syntax: 
      ```SQL
      UPDATE table_name
      SET column1 = value1, column2 = value2, ...
      WHERE condition;
      ```
   * Example: 
      ```SQL
      UPDATE employees
      SET salary = 70000
      WHERE employee_id = 1;
      ```
  * Explanation: This query updates the salary of the employee with employee_id 1 to 70000.
  * Updating Multiple Columns:
      ```SQL
      UPDATE employees
      SET salary = 75000, department_id = 2
      WHERE employee_id = 2;
      ```
  * Explanation: This query updates both the `salary` and `department_id` of the `employee` with `employee_id` 2.
  * Updating Multiple Rows:
    ```SQL
    UPDATE employees
    SET salary = salary * 1.1
    WHERE department_id = 3;
    ```
  * Explanation: This query gives a 10% salary increase to all employees in department 3.

3. DELETE Statement
  * Purpose: Removes rows from a table.
  * Syntax:
    ```SQL
    DELETE FROM table_name
    WHERE condition;
    ```
  * Example:
    ```SQL
    DELETE FROM employees
    WHERE employee_id = 3;
    ```
  * Explanation: This query deletes all employees who are in department 4.
  * Deleting All Rows (Use with caution):
    ```SQL
    DELETE FROM employees;
    ```
  * Explanation: This query deletes all rows from the employees table. It does not delete the table itself, only the data within it.

### Using Transactions
Transactions in SQL ensure that a series of operations are completed successfully before making any changes permanent. They are essential for maintaining data integrity.

* Syntax:
  ```SQL
  BEGIN TRANSACTION;

  -- Insert a new employee
  INSERT INTO employees (first_name, last_name, department_id, salary)
  VALUES ('Alice', 'Williams', 5, 90000);

  -- Update another employee's salary
  UPDATE employees
  SET salary = 95000
  WHERE employee_id = 4;

  -- Delete an employee
  DELETE FROM employees
  WHERE employee_id = 6;

  COMMIT;
  ```

* Explanation:
	•	`BEGIN TRANSACTION` starts a transaction block.
	•	Multiple `SQL` operations are performed within the transaction.
	•	`COMMIT` makes all changes permanent. If any of the operations fail, you can use `ROLLBACK` to undo all changes within the transaction block.

### Summary

Mastering data manipulation commands in SQL is crucial for effectively managing and modifying data within a database. Understanding how to use INSERT, UPDATE, and DELETE statements allows you to add, change, and remove data as needed, ensuring that your database remains accurate and up-to-date. Using transactions helps maintain data integrity by ensuring that a series of related operations are all completed successfully.

## 6. Subqueries
### Subqueries
A subquery, also known as an inner query or nested query, is a query within another SQL query and embedded within the WHERE clause, the FROM clause, or the SELECT clause. Subqueries can be used to return data that will be used in the main query as a condition to further restrict the data to be retrieved.

1. Subqueries in the SELECT Clause
* Purpose: To include a value in the SELECT list that is computed from another query.
* Syntax:
  ```SQL
  SELECT column1, (SELECT column2 FROM table2 WHERE condition) AS alias_name
  FROM table1;
  ```

* Example:
  ```SQL
  SELECT employee_id, first_name,
       (SELECT department_name FROM departments WHERE departments.department_id = employees.department_id) AS department_name
  FROM employees;
  ```

* Explanation: This query selects the `employee_id` and `first_name` from the employees table and also retrieves the `department_name` from the departments table based on the matching `department_id`.

2. Subqueries in the WHERE Clause
* Purpose: o use the result of another query to filter the results of the main query.
* Syntax:
  ```SQL
  SELECT column1, column2
  FROM table1
  WHERE column3 = (SELECT column4 FROM table2 WHERE condition);
  ```

* Example:
  ```SQL
  SELECT first_name, last_name
  FROM employees
  WHERE department_id = (SELECT department_id FROM departments WHERE department_name = 'Sales');
  ```

* Explanation: This query selects the `first_name` and `last_name` of employees who are in the department named ‘Sales’.

* Using Subqueries with IN:
  ```SQL
  SELECT first_name, last_name
  FROM employees
  WHERE department_id IN (SELECT department_id FROM departments WHERE location = 'New York');
  ```

* Explanation: This query selects the `first_name` and `last_name` of employees who work in departments located in ‘New York’.

3. Subqueries in the FROM Clause
* Purpose: To use the result of another query as a table in the main query.
* Syntax:
    ```SQL
    SELECT column1, column2
    FROM (SELECT column3, column4 FROM table2 WHERE condition) AS alias_name
    WHERE condition;
    ```
* Example:
  ```SQL
  SELECT sub.department_name, COUNT(sub.employee_id) AS employee_count
  FROM (SELECT department_id, department_name FROM departments) AS sub
  INNER JOIN employees ON sub.department_id = employees.department_id
  GROUP BY sub.department_name;
  ```

* Explanation: This query creates a subquery that selects the `department_id` and `department_name` from the departments table. The main query then counts the number of employees in each department.

### Types of Subqueries
#### Single-Row Subqueries
* Purpose: Returns only one row:
* Example:
  ```SQL
  SELECT first_name, last_name
  FROM employees
  WHERE salary > (SELECT AVG(salary) FROM employees);
  ```

* Explanation: This query selects the first_name and last_name of employees whose salary is greater than the average salary of all employees.

#### Multiple-Row Subqueries
* Purpose: Returns more than one row.
* Example:
  ```SQL
  SELECT first_name, last_name
  FROM employees
  WHERE department_id IN (SELECT department_id FROM departments WHERE location = 'Chicago');
  ```
* Explanation: This query selects the first_name and last_name of employees who work in departments located in ‘Chicago’.

#### Correlated Subqueries
* Purpose: References columns from the outer query. It is evaluated once for each row processed by the outer query.
* Syntax: 
    ```SQL
    SELECT column1, column2
    FROM table1 outer
    WHERE column3 operator (SELECT column4 FROM table2 WHERE table2.column5 = outer.column6);
    ```
* Example:
  ```SQL
  SELECT e1.first_name, e1.last_name, e1.salary
  FROM employees e1
  WHERE e1.salary > (SELECT AVG(e2.salary) FROM employees e2 WHERE e2.department_id = e1.department_id);
  ```

### Summary

Subqueries are a powerful feature in SQL that allow you to perform complex queries by embedding one query within another. Understanding how to use subqueries in the SELECT, WHERE, and FROM clauses, as well as the differences between single-row, multiple-row, and correlated subqueries, will significantly enhance your ability to retrieve and analyze data effectively.

## 7. Data Types

### Data Types 

Data types define the type of data that a column can hold in a SQL database. Choosing the correct data type for each column is crucial for data integrity, performance, and storage efficiency. Here’s a comprehensive look at common data types:

1. Numeric Data Types
* INT (INTEGER): Stores whole numbers.
   * Syntax:
      ```SQL
      column_name INT;
      ```
   * Example:
      ```SQL
      age INT;
      ```
* FLOAT: Stores floating-point numbers, which are numbers with a decimal point.
  * Syntax:
    ```sql
    column_name FLOAT;
    ```
  * Example:
    ```sql
    price FLOAT;
    ```
* DOUBLE: Stores double-precision floating-point numbers, offering more precision than FLOAT.
  * Syntax:
    ```SQL
    column_name DOUBLE;
    ```
  * Example:
    ```sql
    distance DOUBLE;
    ```
* DECIMAL (NUMERIC): Stores exact numeric data with a fixed precision and scale. Ideal for monetary values.
  * Syntax:
    ```sql
    column_name DECIMAL(precision, scale);
    ```
  * Example:
    ```sql
    salary DECIMAL(10, 2);
    ```
  * Explanation: DECIMAL(10, 2) means the number can have up to 10 digits, with 2 digits after the decimal point.
2. String Data Types
* CHAR: Stores fixed-length strings.
  * Syntax:
    ```sql
    column_name CHAR(length);
    ```
  * Example:
    ```sql
    gender CHAR(1);
    ```
  * Explanation: CHAR(1) can store a single character.
* VARCHAR: Stores variable-length strings.
  * Syntax:
    ```sql
    column_name VARCHAR(length);
    ```
  * Example:
    ```sql
    name VARCHAR(100);
    ```
  * Explanation: VARCHAR(100) can store a string with up to 100 characters.
* TEXT: Stores large amounts of text.
  * Syntax:
    ```sql
      column_name TEXT;
    ```
  * Example:
    ```sql
    description TEXT;
    ```
* Explanation: TEXT can store a string of any length (subject to the database system's limit).

3. Date and Time Data Types
* DATE: Stores dates in the format YYYY-MM-DD.
  * Syntax:
    ```sql
    column_name DATE;
    ```
  * Example:
    ```sql
    birth_date DATE;
    ```
* TIME: Stores time in the format HH:MM:SS.
  * Syntax:
    ```sql
    column_name TIME;
    ```
  * Example:
    ```sql
    start_time TIME;
    ```
* DATETIME: Stores both date and time in the format YYYY-MM-DD HH:MM:SS.
  * Syntax:
    ```sql
    column_name DATETIME;
    ```
  * Example:
    ```sql
    created_at DATETIME;
    ```
* TIMESTAMP: Stores both date and time, typically used for tracking changes in records.
  * Syntax:
    ```sql
    column_name TIMESTAMP;
    ```
  * Example:
    ```sql
    last_updated TIMESTAMP;
    ```
4. Binary Data Types
* BLOB: Stores binary large objects, such as images or other multimedia files.
  * Syntax:
    ```sql
    column_name BLOB;
    ```
  * Example:
    ```sql
    profile_picture BLOB;
    ```
5. Boolean Data Types
* BOOLEAN: Stores true or false values.
  * Syntax:
    ```sql
    column_name BOOLEAN;
    ```
  * Example:
    ```sql
    is_active BOOLEAN;
    ```
6. Enumerated Data Types
* ENUM: Stores one value from a defined list of values.
  * Syntax:
    ```sql
    column_name ENUM('value1', 'value2', ...);
    ```
  * Example:
    ```sql
    status ENUM('active', 'inactive', 'pending');
    ```
### Practical Examples
* Creating a Table with Various Data Types:
  ```sql
  CREATE TABLE employees (
      employee_id INT PRIMARY KEY,
      first_name VARCHAR(50),
      last_name VARCHAR(50),
      birth_date DATE,
      salary DECIMAL(10, 2),
      is_active BOOLEAN,
      profile_picture BLOB,
      status ENUM('active', 'inactive', 'pending')
  );
  ```

* Inserting Data with Various Data Types:
  ```sql
  INSERT INTO employees (employee_id, first_name, last_name, birth_date, salary, is_active, profile_picture, status)
  VALUES (1, 'John', 'Doe', '1980-05-15', 75000.00, TRUE, LOAD_FILE('/path/to/picture.jpg'), 'active');
  ```

* Selecting Data with Various Data Types:
  ```sql
  SELECT employee_id, first_name, last_name, birth_date, salary, is_active, status
  FROM employees;
  ```

* Updating Data with Various Data Types:
  ```sql
  UPDATE employees
  SET salary = 80000.00, is_active = FALSE
  WHERE employee_id = 1;
  ```

* Deleting Data with Various Data Types:
  ```sql
  DELETE FROM employees
  WHERE is_active = FALSE;
  ```

### Summary

Understanding and correctly using data types in SQL is fundamental for effective database design and operation. Different data types serve different purposes, and selecting the appropriate type for each column ensures that the database performs efficiently and maintains data integrity. Knowing how to define and manipulate various data types will significantly enhance your SQL skills and database management capabilities.

## 8. Indexes

### Indexes
Indexes in SQL are special lookup tables that the database search engine can use to speed up data retrieval. An index on a column or set of columns can drastically improve the performance of query operations. However, indexes also introduce overhead for data modification operations such as INSERT, UPDATE, and DELETE. Here’s an in-depth look at indexes:

1. Basics of Indexing:
* Purpose: To speed up the retrieval of rows by using a pointer.
  * Syntax:
    ```sql
    CREATE INDEX index_name
    ON table_name (column1, column2, ...);
    ```
  * Example:
    ```sql
    CREATE INDEX idx_last_name
    ON employees (last_name);
    ```
  * Explanation: This query creates an index named `idx_last_name` on the `last_name` column of the employees table. This index will speed up searches based on `last_name`.
2. Creating Indexes
   * Single-Column Index:
     ```sql
     CREATE INDEX idx_employee_id
     ON employees (employee_id);
     ```
   * Composite Index (Multi-Column Index):
      ```sql
      CREATE INDEX idx_name_department
      ON employees (last_name, department_id);
      ```
* Explanation: This index speeds up queries that filter on both last_name and department_id.

3. Unique Indexes
   * Purpose: Ensures that all values in the index key are unique.
   * Syntax:
      ```sql
      CREATE UNIQUE INDEX index_name
      ON table_name (column1, column2, ...);
      ```
   * Example:
      ```sql
      CREATE UNIQUE INDEX idx_unique_email
      ON employees (email);
      ```
   * Explanation: This query creates a unique index on the email column to ensure that no two employees can have the same email address.

4. Primary Key Indexes
   * Purpose: Automatically created when a primary key constraint is defined.
   * Syntax:
      ```sql
      CREATE TABLE employees (
          employee_id INT PRIMARY KEY,
          first_name VARCHAR(50),
          last_name VARCHAR(50)
      );
      ```
   * Explanation: The PRIMARY KEY constraint automatically creates a unique index on the employee_id column.

5. Foreign Key Indexes
   * Purpose: Often created on foreign key columns to speed up joins.
   * Example:
      ```sql
      CREATE TABLE departments (
          department_id INT PRIMARY KEY,
          department_name VARCHAR(50)
      );
      

      CREATE TABLE employees (
          employee_id INT PRIMARY KEY,
          first_name VARCHAR(50),
          last_name VARCHAR(50),
          department_id INT,
          FOREIGN KEY (department_id) REFERENCES departments(department_id)
      );

      CREATE INDEX idx_department_id
      ON employees (department_id);
      ```
   * Explanation: The index on `department_id` improves join performance between employees and departments tables.
6. Full-Text Indexes
   * Purpose: Used for full-text searches.
   * Syntax:
      ```sql
      CREATE FULLTEXT INDEX index_name
      ON table_name (column1, column2, ...);
      ```
   * Example:
      ```sql
      CREATE FULLTEXT INDEX idx_fulltext_description
      ON products (description);
      ```
   * Explanation: This index allows for efficient full-text search queries on the description column.
7. Dropping Indexes
   * Purpose: To remove an index that is no longer needed.
   * Syntax:
      ```sql
      DROP INDEX index_name ON table_name;
      ```
   * Example:
      ```sql
      DROP INDEX idx_last_name ON employees;
      ```
   * Explanation: This query drops the idx_last_name index from the employees table.

### Index Maintenance
#### Rebuilding Indexes
   * Purpose: To optimize performance by reorganizing index data.
   * Syntax:
      ```sql
      ALTER INDEX index_name REBUILD;
      ```
   * Example:
      ```sql
      ALTER INDEX idx_last_name REBUILD;
      ```
   * Explanation: This query rebuilds the idx_last_name index, which can improve performance if the index has become fragmented.
#### Monitoring Index Usage
   * Purpose: To analyze index usage and determine if indexes are effective.
   * Example Tools:
      * SQL Server: `sys.dm_db_index_usage_stats` view.
      * MySQL: `SHOW INDEX FROM table_name;` command.
      * PostgreSQL: `pg_stat_user_indexes` view.
### Practical Examples
1. Creating an Index:
    ```sql
    CREATE INDEX idx_last_name
    ON employees (last_name);
    ```

2. Creating a Composite Index:
    ```sql
    CREATE INDEX idx_name_department
    ON employees (last_name, department_id);
    ```

3. Creating a Unique Index:
    ```sql
    CREATE UNIQUE INDEX idx_unique_email
    ON employees (email);
    ```

4. Creating a Full-Text Index:
    ```sql
    CREATE FULLTEXT INDEX idx_fulltext_description
    ON products (description);
    ```

5. Dropping an Index:
    ```sql
    DROP INDEX idx_last_name ON employees;
    ```

6. Rebuilding an Index:
    ```sql
    ALTER INDEX idx_last_name REBUILD;
    ```

### Summary

Indexes are critical for enhancing the performance of SQL queries by allowing the database to find rows more quickly. Understanding when and how to use different types of indexes—single-column, composite, unique, primary key, foreign key, and full-text indexes—can significantly optimize your database operations. However, it's important to balance the benefits of faster query performance with the overhead that indexes introduce for data modification operations. Regular maintenance and monitoring of indexes ensure they continue to provide performance benefits.

## 9. Query Optimization
### Query Optimization
Optimizing SQL queries is crucial for ensuring that your database performs efficiently, especially as the volume of data and the complexity of queries increase. Here are several key techniques and best practices for query optimization:

1. EXPLAIN/EXPLAIN PLAN
   * Purpose: Analyze how a SQL query will be executed by the database. It provides insights into the query execution plan, such as which indexes are used and the join order of tables.
   * Syntax:
      ```sql
      EXPLAIN SELECT column1, column2 FROM table_name WHERE condition;
      ```
   * Example:
      ```sql
      EXPLAIN SELECT first_name, last_name FROM employees WHERE department_id = 1;
      ```
* Explanation: This command returns the execution plan for the query, showing details like the type of join, possible keys, key used, and rows examined.

2. Query Hints
   * Purpose: Provide the database engine with instructions on how to execute a query. These are specific to the database management system (DBMS).
   * Syntax (MySQL Example):
      ```sql
      SELECT /*+ MAX_EXECUTION_TIME(1000) */ column1, column2 FROM table_name WHERE condition;
      ```
   * Example (Oracle Example):
      ```sql
      SELECT /*+ INDEX(employees idx_department_id) */ first_name, last_name FROM employees WHERE department_id = 1;
      ```
   * Explanation: The hint tells the Oracle DBMS to use the idx_department_id index for the query.
3. Query Rewrite
   * Purpose: Modify queries to improve performance, often by simplifying complex queries or breaking them into smaller, more efficient parts.
   * Example:
     * Original Query:
        ```sql
        SELECT * FROM orders WHERE YEAR(order_date) = 2023;
        ```
     * Rewritten Query:
        ```sql
        SELECT * FROM orders WHERE order_date BETWEEN '2023-01-01' AND '2023-12-31';
        ```
     * Explanation: The rewritten query uses a range condition instead of a function on the column, making it easier for the database to use indexes.
4. Using LIMIT/OFFSET
   * Purpose: Efficiently handle large result sets by fetching only the necessary rows.
   * Syntax:
      ```sql
      SELECT column1, column2 FROM table_name ORDER BY column1 LIMIT 10 OFFSET 20;
      ```
   * Example:
      ```sql
      SELECT first_name, last_name FROM employees ORDER BY hire_date DESC LIMIT 10 OFFSET 20;
      ```
   * Explanation: This query fetches 10 rows starting from the 21st row, which is useful for paginating results in applications.
5. Avoiding SELECT *
   * Purpose: Reduce the amount of data retrieved by specifying only the necessary columns.
   * Example:
     * Inefficient Query:
        ```sql
        SELECT * FROM employees WHERE department_id = 1;
        ```
     * Efficient Query:
        ```sql
        SELECT first_name, last_name, hire_date FROM employees WHERE department_id = 1;
        ```
   * Explanation: By selecting only the required columns, you reduce the amount of data transferred and processed.
6. Reducing Joins
   * Purpose: Minimize the number of joins to reduce complexity and improve performance.
   * Example:
      * Complex Query:
        ```sql
        SELECT e.first_name, e.last_name, d.department_name, p.project_name
        FROM employees e
        JOIN departments d ON e.department_id = d.department_id
        JOIN projects p ON e.project_id = p.project_id;
        ```
     * Simplified Query:
        ```sql
        SELECT e.first_name, e.last_name, d.department_name
        FROM employees e
        JOIN departments d ON e.department_id = d.department_id;
        ```
     * Explanation: The simplified query joins only two tables instead of three, reducing the complexity and improving performance.
7. Proper Use of WHERE Clauses
   * Purpose: Ensure conditions are properly indexed and avoid using functions on indexed columns.
   * Example:
     * Inefficient Query:
        ```sql
        SELECT * FROM employees WHERE UPPER(last_name) = 'SMITH';
        ```
     * Efficient Query:
        ```sql
        SELECT * FROM employees WHERE last_name = 'Smith';
        ```
    * Explanation: The efficient query allows the use of an index on the last_name column, whereas the inefficient query does not.
8. Index Scans vs. Table Scans
   * Purpose: Prefer index scans over table scans for faster data retrieval.
   * Example:
     * Table Scan:
        ```sql
        SELECT * FROM employees WHERE department_id = 1;
        ```
     * Index Scan (Assuming index on department_id):
        ```sql
        CREATE INDEX idx_department_id ON employees (department_id);
        SELECT * FROM employees WHERE department_id = 1;
        ```

   * Explanation: Creating an index on department_id allows the database to perform an index scan, which is faster than a table scan.
9. Caching Strategies
   * Purpose: Use caching to reduce database load by storing frequently accessed data in memory.
   * Example:
     * Use a caching layer like Redis or Memcached to store frequently accessed query results.
        ```sql
        -- Assuming you have a caching mechanism in place
        -- Pseudo-code example
        IF cache_exists('employees_department_1') THEN
            RETURN cache('employees_department_1');
        ELSE
            result = SELECT * FROM employees WHERE department_id = 1;
            cache('employees_department_1', result);
            RETURN result;
        END IF;
        ```
   * Explanation: This pseudo-code checks if the result is already in the cache and returns it if available. If not, it queries the database, caches the result, and then returns it.
10. Partitioning
    * Purpose: Break down a large table into smaller, more manageable pieces to improve query performance.
    * Syntax (MySQL Example):
      ```sql
      CREATE TABLE orders (
          order_id INT,
          order_date DATE,
          ...
      )
      PARTITION BY RANGE (YEAR(order_date)) (
          PARTITION p0 VALUES LESS THAN (2021),
          PARTITION p1 VALUES LESS THAN (2022),
          PARTITION p2 VALUES LESS THAN (2023),
          PARTITION p3 VALUES LESS THAN (2024)
      );
      ```
    * Explanation: This query partitions the orders table by year, allowing the database to access only the relevant partition when querying by order_date.

### Practical Examples
1. Using EXPLAIN to Analyze a Query:
    ```sql
    EXPLAIN SELECT first_name, last_name FROM employees WHERE department_id = 1;
    ```

2. Using Query Hints (MySQL Example):
    ```sql
    SELECT /*+ MAX_EXECUTION_TIME(1000) */ first_name, last_name FROM employees WHERE department_id = 1;
    ```

3. Rewriting Queries for Optimization:
    ```sql
    -- Original Query
    SELECT * FROM orders WHERE YEAR(order_date) = 2023;

    -- Rewritten Query
    SELECT * FROM orders WHERE order_date BETWEEN '2023-01-01' AND '2023-12-31';
    ```

4. Using LIMIT and OFFSET for Pagination:
    ```sql
    SELECT first_name, last_name FROM employees ORDER BY hire_date DESC LIMIT 10 OFFSET 20;
    ```

5. Selecting Specific Columns Instead of *:
    ```sql
    SELECT first_name, last_name, hire_date FROM employees WHERE department_id = 1;
    ```

6. Reducing Joins in Queries:
    ```sql
    -- Complex Query with Multiple Joins
    SELECT e.first_name, e.last_name, d.department_name, p.project_name
    FROM employees e
    JOIN departments d ON e.department_id = d.department_id
    JOIN projects p ON e.project_id = p.project_id;

    -- Simplified Query with Fewer Joins
    SELECT e.first_name, e.last_name, d.department_name
    FROM employees e
    JOIN departments d ON e.department_id = d.department_id;
    ```

7. Optimizing WHERE Clauses:
    ```sql
    -- Inefficient Query
    SELECT * FROM employees WHERE UPPER(last_name) = 'SMITH';

    -- Efficient Query
    SELECT * FROM employees WHERE last_name = 'Smith';
    ```

8. Creating and Using Indexes:
    ```sql
    CREATE INDEX idx_department_id ON employees (department_id);
    SELECT * FROM employees WHERE department_id = 1;
    ```

9. Implementing Caching Strategies:
    ```sql
    -- Pseudo-code for caching query results
    IF cache_exists('employees_department_1') THEN
        RETURN cache('employees_department_1');
    ELSE
        result = SELECT * FROM employees WHERE department_id = 1;
        cache('employees_department_1', result);
        RETURN result;
    END IF;
    ```

10. Partitioning Tables:
    ```sql
    CREATE TABLE orders (
        order_id INT,
        order_date DATE,
        ...
    )
    PARTITION BY RANGE (YEAR(order_date)) (
        PARTITION p0 VALUES LESS THAN (2021),
        PARTITION p1 VALUES LESS THAN (2022),
        PARTITION p2 VALUES LESS THAN (2023),
        PARTITION p3 VALUES LESS THAN (2024)
    );
    ```

### Summary
Optimizing SQL queries involves various techniques aimed at improving performance and efficiency. Understanding and utilizing tools like EXPLAIN, rewriting queries, using appropriate indexes, leveraging caching strategies, and partitioning tables can significantly enhance query performance. By applying these optimization strategies, you can ensure your database operations are fast, efficient, and scalable, especially as your data grows and query complexity increases.

## 10. Normalization

## 11. Basic Transactions

## 12 .Performance Tuning Specifics



## Notes:
* In Postgres, SERIAL is now 