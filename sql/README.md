# SQL

## Table of Contents
### 1. [Basic Queries](#1-basic-queries)
* [SELECT Statements:](#1-select-statements) How to retrieve data from a database.
* [FROM Clause](#2-from-clause): Understanding tables and how to select them.
* [WHERE Clause](#3-where-clause): Filtering data based on conditions.

### 2. [Joins](#2-joins)
* [INNER JOIN](#1-inner-join): Combining rows from two or more tables based on a related column.
* [LEFT JOIN](#2-left-join-or-left-outer-join): Returning all rows from the left table, and the matched rows from the right table.
* [RIGHT JOIN](#3-right-join-or-right-outer-join): Returning all rows from the right table, and the matched rows from the left table.
* [FULL OUTER JOIN](#4-full-outer-join): Returning all rows when there is a match in either left or right table.

### 3. [Aggregation Functions](#3-aggregation-functions)
* [COUNT()](#1-count): Counting the number of rows.
* [SUM()](#2-sum): Summing the values of a column.
* [AVG()](#3-avg): Calculating the average value of a column.
* [MAX() and MIN()](#5-min): Finding the maximum and minimum values.

### 4. [Grouping Data](#4-grouping-data)
* [GROUP BY](#1-group-by-clause): Aggregating data across multiple records.
* [HAVING](#3-having-clause): Filtering groups based on conditions.

### 5. [Data Manipulation](#5-data-manipulation)
* [INSERT](#1-insert-statement): Adding new rows to a table.
* [UPDATE](#2-update-statement): Modifying existing rows in a table.
* [DELETE](#3-delete-statement): Removing rows from a table.

### 6. [Subqueries](#6-subqueries)
* Subqueries in SELECT: Using queries within other queries.
* Subqueries in WHERE: Filtering data based on subquery results.

### 7. [Data Types](#7-data-types)
* [Numeric Data Types](#1-numeric-data-types)
* [String Data Types](#2-string-data-types)
* [Date and Time Data Types](#3-date-and-time-data-types)
* [Binary Data Types](#4-binary-data-types)
* [Boolean Data Types](#5-boolean-data-types)
* [Enumerated Data Types](#6-enumerated-data-types)

### 8. [Indexes](#8-indexes)
* Basics of Indexing: Understanding how indexes work and their importance.
* Creating Indexes: How to create indexes to improve query performance.
* Composite Indexes: Using multiple columns in an index.
* Index Maintenance: Keeping indexes healthy and up-to-date.

### 9. [Query Optimization](#9-query-optimization)
* EXPLAIN/EXPLAIN PLAN: Analyzing query execution plans to identify bottlenecks.
* Query Hints: Providing hints to the database engine for better query performance.
* Query Rewrite: Techniques to rewrite queries for better performance.
* Using LIMIT/OFFSET: Efficiently paging through large result sets.

### 10.  [Normalization](#10-normalization)
* Basic concepts of database normalization and why it is important.
* Denormalization: When and how to denormalize for performance reasons.

### 11.  [Basic Transactions](#11-basic-transactions)
* BEGIN, COMMIT, ROLLBACK: Understanding transactions and how to ensure data integrity.

### 12.  [Database Views](#12-database-views)
* Creating Views: Define virtual tables using SELECT queries to simplify data access and enhance security.
* Querying Views: Retrieve data from views, using them as virtual tables in your queries.
* Updating Views: Modifying underlying data through views and how to perform updates.
* Managing Views: Alter, replace, or drop views to maintain database structure and functionality.

### 13.  [More Performance Tuning](#13-more-performance-tuning)
* Avoiding SELECT *: Selecting only the necessary columns to reduce data load.
* Reducing Joins: Minimizing the number of joins in queries for better performance.
* Use of Stored Procedures: Using stored procedures to encapsulate complex logic.
* Proper Use of WHERE Clauses: Ensuring conditions are indexed properly.
* Index Scans vs. Table Scans: Understanding the difference and how to avoid full table scans.
* Caching Strategies: Using caching mechanisms to reduce database load.
* Partitioning: Implementing table partitioning to manage large datasets efficiently.

## 1. Basic Queries
Understanding basic queries is foundational to working with SQL databases. Here are the critical components:
### Basic Queries
#### 1. SELECT Statements

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

#### 2. FROM Clause
   
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

#### 3. WHERE Clause
   
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

#### 4. ORDER BY Clause
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

#### 5. LIMIT Clause
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

#### 6. DISTINCT Keyword
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

#### 7. Aliasing
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
### Joins
#### 1. INNER JOIN
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

#### 2. LEFT JOIN (or LEFT OUTER JOIN)

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

#### 3. RIGHT JOIN (or RIGHT OUTER JOIN)

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

#### 4. FULL OUTER JOIN
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

#### 5. Self Join
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

#### 6. Cross Join

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

### Aggregation Functions
#### 1. **COUNT()**
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

#### 2. SUM()
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

#### 3. AVG()
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

#### 4. MAX()
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

#### 5. MIN()	
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

### Grouping Data
#### 1. GROUP BY Clause
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

#### 2. Using Aggregate Functions with GROUP BY
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

#### 3. `HAVING` Clause
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

#### 1. INSERT Statement
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

#### 2. UPDATE Statement
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

#### 3. DELETE Statement
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

#### 1. Subqueries in the SELECT Clause
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

#### 2. Subqueries in the WHERE Clause
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

#### 3. Subqueries in the FROM Clause
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

#### 1. Numeric Data Types
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
  
#### 2. String Data Types
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

#### 3. Date and Time Data Types
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
#### 4. Binary Data Types
* BLOB: Stores binary large objects, such as images or other multimedia files.
  * Syntax:
    ```sql
    column_name BLOB;
    ```
  * Example:
    ```sql
    profile_picture BLOB;
    ```
#### 5. Boolean Data Types
* BOOLEAN: Stores true or false values.
  * Syntax:
    ```sql
    column_name BOOLEAN;
    ```
  * Example:
    ```sql
    is_active BOOLEAN;
    ```
#### 6. Enumerated Data Types
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
### Normalization
Normalization is a database design technique that organizes tables in a way that reduces redundancy and dependency. The goal is to decompose a table into smaller, more manageable pieces without losing data integrity. This is achieved through a series of normalization forms (NFs). Each form has specific rules and purposes.

1. First Normal Form (1NF)
   * Purpose: Ensures that the table is organized in such a way that each column contains atomic (indivisible) values, and each column contains only one type of data.
   * Rules:
      * Each table must have a primary key.
      * Each column should contain atomic values (no repeating groups or arrays).
      * Each column should contain values of a single type.
  * Example:
     * Non-1NF Table:
        ```plaintext
        Orders
        --------------------------------
        OrderID | CustomerName | Items
        1       | John Doe     | Pen, Pencil
        2       | Jane Smith   | Notebook
        ```
     * 1NF Table:
        ```plaintext
        Orders
        --------------------------------
        OrderID | CustomerName | Item
        1       | John Doe     | Pen
        1       | John Doe     | Pencil
        2       | Jane Smith   | Notebook
        ```
2. Second Normal Form (2NF)
   * Purpose: Ensures that the table is in 1NF and that all non-key attributes are fully functional dependent on the primary key.
   * Rules:
      * Must meet all the requirements of 1NF.
      * All non-key attributes must be fully functional dependent on the primary key.
      * Remove partial dependencies (a non-key attribute depends only on part of the composite primary key).
   * Example:
     * Non-2NF Table:
        ```plaintext
        Orders
        --------------------------------------
        OrderID | CustomerID | CustomerName  | ItemID | ItemName
        1       | 1          | John Doe      | 1      | Pen
        1       | 1          | John Doe      | 2      | Pencil
        2       | 2          | Jane Smith    | 3      | Notebook
        ```
     * 2NF Tables:
        ```plaintext
        Orders
        ----------------------------------
        OrderID | CustomerID | ItemID
        1       | 1          | 1
        1       | 1          | 2
        2       | 2          | 3

        Customers
        -----------------------------------
        CustomerID | CustomerName
        1          | John Doe
        2          | Jane Smith

        Items
        -----------------------------------
        ItemID | ItemName
        1      | Pen
        2      | Pencil
        3      | Notebook
        ```
3. Third Normal Form (3NF)
   * Purpose: Ensures that the table is in 2NF and that all the attributes are only dependent on the primary key.
   * Rules:
      * Must meet all the requirements of 2NF.
      * Remove transitive dependencies (non-key attributes should not depend on other non-key attributes).
   * Example:
     * Non-3NF Table:
        ```plaintext
        Orders
        ----------------------------------------------
        OrderID | CustomerID | CustomerName | CustomerAddress
        1       | 1          | John Doe     | 123 Main St
        2       | 2          | Jane Smith   | 456 Oak St
        ```

     * 3NF Tables:
        ```plaintext
        Orders
        ---------------------------
        OrderID | CustomerID
        1       | 1
        2       | 2

        Customers
        ----------------------------
        CustomerID | CustomerName | CustomerAddress
        1          | John Doe     | 123 Main St
        2          | Jane Smith   | 456 Oak St
        ```
4. Boyce-Codd Normal Form (BCNF)
   * Purpose: A stronger version of 3NF. Ensures that every determinant is a candidate key.
   * Rules:
     * Must meet all the requirements of 3NF.
     * For every functional dependency (X -> Y), X should be a super key.
   * Example:
     * Non-BCNF Table:
        ```plaintext
        Courses
        -----------------------------------
        CourseID | Instructor | Room
        1        | Smith      | 101
        2        | Jones      | 102
        3        | Smith      | 103
        ```

     * BCNF Tables:
        ```plaintext
        Courses
        -------------------------
        CourseID | InstructorID
        1        | 1
        2        | 2
        3        | 1

        Instructors
        --------------------------
        InstructorID | InstructorName
        1            | Smith
        2            | Jones

        InstructorRooms
        ------------------------
        InstructorID | Room
        1            | 101
        1            | 103
        2            | 102
        ```
### Higher Normal Forms
While the first three normal forms and BCNF are the most commonly used, there are higher normal forms such as Fourth Normal Form (4NF) and Fifth Normal Form (5NF), which deal with more complex scenarios involving multi-valued dependencies and join dependencies. These are less commonly needed in typical database design.

**Denormalization**
   * Purpose: Sometimes, to improve query performance, you may denormalize the data. This involves adding redundancy to the database to avoid complex joins and improve read performance.
   * Trade-offs: While denormalization can improve read performance, it may increase storage requirements and complicate data modification operations.

### Practical Examples
* 1NF Example:
    * Original Table (Not in 1NF):
      ```plaintext
      Orders
      ----------------------------------
      OrderID | Customer | Items
      1       | John Doe | Pen, Pencil
      ```

  * Normalized Table (1NF):
    ```plaintext
    Orders
    ---------------------------
    OrderID | Customer | Item
    1       | John Doe | Pen
    1       | John Doe | Pencil
    ```

* 2NF Example:
  * Original Table (Not in 2NF):
    ```plaintext
    Orders
    --------------------------------------
    OrderID | CustomerID | CustomerName  | ItemID | ItemName
    1       | 1          | John Doe      | 1      | Pen
    ```
  * Normalized Tables (2NF):
    ```plaintext
    Orders
    ---------------------------
    OrderID | CustomerID | ItemID
    1       | 1          | 1

    Customers
    ----------------------------
    CustomerID | CustomerName
    1          | John Doe

    Items
    ----------------------------
    ItemID | ItemName
    1      | Pen
    ```

* 3NF Example:
  * Original Table (Not in 3NF):
    ```plaintext
    Orders
    ----------------------------------------------
    OrderID | CustomerID | CustomerName | Address
    1       | 1          | John Doe     | 123 Main St
    ```
  * Normalized Tables (3NF):
    ```plaintext
    Orders
    ---------------------------
    OrderID | CustomerID
    1       | 1

    Customers
    ----------------------------
    CustomerID | CustomerName | Address
    1          | John Doe     | 123 Main St
    ```

### Summary
Normalization is essential for designing efficient and scalable databases. By following normalization principles, you can reduce redundancy, improve data integrity, and ensure that your database is easy to maintain. However, understanding when to denormalize for performance reasons is also crucial, as overly normalized databases can sometimes lead to complex and slow queries. Balancing normalization and denormalization based on your specific use case and performance requirements will help you design optimal database schemas.

## 11. Basic Transactions
### Basic Transactions
Transactions in SQL are a sequence of one or more SQL operations treated as a single unit of work. They ensure data integrity and consistency, especially in environments where multiple users may be accessing and modifying the database simultaneously. Transactions follow the ACID properties: Atomicity, Consistency, Isolation, and Durability.

#### 1. ACID Properties
   * Atomicity: Ensures that all operations within a transaction are completed successfully; otherwise, the transaction is aborted and no operations are applied.
   * Consistency: Ensures that the database transitions from one valid state to another valid state.
   * Isolation: Ensures that concurrent execution of transactions leaves the database in the same state as if the transactions were executed sequentially.
   * Durability: Ensures that once a transaction is committed, the changes are permanent, even in the event of a system failure.
#### 2. Basic Transaction Commands
   * BEGIN/START TRANSACTION: Starts a new transaction.
      ```sql
      BEGIN TRANSACTION;
      ```
   * COMMIT: Saves all changes made during the transaction.
      ```sql
      COMMIT;
      ```
   * ROLLBACK: Undoes all changes made during the transaction.
      ```sql
      ROLLBACK;
      ```
#### 3. Using Transactions
   
Transactions are used to ensure data integrity and consistency. They are especially useful for operations that involve multiple steps, such as transferring money between bank accounts, updating inventory, or placing an order.

**Example Scenario: Transferring Money Between Bank Accounts**
1. BEGIN TRANSACTION
   * Starts the transaction.
2. Update Account Balances
   * Deducts the amount from one account and adds it to another.
3. COMMIT
   * Saves the changes if both updates are successful.
4. ROLLBACK
   * Undoes the changes if any update fails.
  
  ```sql
  BEGIN TRANSACTION;

  UPDATE accounts
  SET balance = balance - 100
  WHERE account_id = 1;

  UPDATE accounts
  SET balance = balance + 100
  WHERE account_id = 2;

  COMMIT;
  ```

**Handling Errors with Transactions**
If an error occurs during a transaction, you can use ROLLBACK to revert all changes made up to that point, ensuring that the database remains in a consistent state.
  ```sql
  BEGIN TRANSACTION;

  BEGIN TRY
      UPDATE accounts
      SET balance = balance - 100
      WHERE account_id = 1;

      UPDATE accounts
      SET balance = balance + 100
      WHERE account_id = 2;

      COMMIT;
  END TRY
  BEGIN CATCH
      ROLLBACK;
  END CATCH;
  ```

#### 4. Savepoints
Savepoints allow you to create points within a transaction to which you can roll back without affecting the entire transaction. They are useful for complex transactions where you want to partially commit some changes while retaining the option to roll back others.

* SAVEPOINT: Creates a savepoint within the transaction.
    ```sql
    SAVEPOINT savepoint_name;
    ```

* ROLLBACK TO SAVEPOINT: Rolls back the transaction to the specified savepoint.
    ```sql
    ROLLBACK TO SAVEPOINT savepoint_name;
    ```

* RELEASE SAVEPOINT: Removes the specified savepoint.
    ```sql
    RELEASE SAVEPOINT savepoint_name;
    ```
Example:
```sql
BEGIN TRANSACTION;

UPDATE accounts
SET balance = balance - 100
WHERE account_id = 1;

SAVEPOINT sp1;

UPDATE accounts
SET balance = balance + 100
WHERE account_id = 2;

-- An error occurs, rollback to savepoint
ROLLBACK TO SAVEPOINT sp1;

-- Continue with other operations
UPDATE accounts
SET balance = balance + 50
WHERE account_id = 3;

COMMIT;
```

#### 5. Isolation Levels
Isolation levels control the visibility of changes made by one transaction to other concurrent transactions. SQL defines several isolation levels, each with different trade-offs between performance and consistency.

* READ UNCOMMITTED: Allows a transaction to read data that has not yet been committed by other transactions. This isolation level can lead to dirty reads.
sql

  ```sql
  SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;
  ```

* READ COMMITTED: Ensures that a transaction cannot read data that has not been committed by other transactions. This isolation level prevents dirty reads.
sql

  ```sql
  SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
  ```

* REPEATABLE READ: Ensures that if a transaction reads the same row twice, the values are the same each time. This isolation level prevents non-repeatable reads but not phantom reads.
  ```sql
  SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
  ```

* SERIALIZABLE: Ensures complete isolation from other transactions. This isolation level prevents dirty reads, non-repeatable reads, and phantom reads.
  ```sql
  SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
  ```

Example:

```sql
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;

BEGIN TRANSACTION;

SELECT balance
FROM accounts
WHERE account_id = 1;

-- Perform other operations...

COMMIT;
```

### Practical Examples
1. Basic Transaction:

    ```sql
    BEGIN TRANSACTION;

    INSERT INTO orders (customer_id, order_date, total)
    VALUES (1, '2024-07-20', 150.00);

    UPDATE inventory
    SET quantity = quantity - 1
    WHERE product_id = 101;

    COMMIT;
    ```

2. Transaction with Error Handling:
    ```sql
    BEGIN TRANSACTION;

    BEGIN TRY
        INSERT INTO orders (customer_id, order_date, total)
        VALUES (2, '2024-07-20', 200.00);

        UPDATE inventory
        SET quantity = quantity - 1
        WHERE product_id = 102;

        COMMIT;
    END TRY
    BEGIN CATCH
        ROLLBACK;
    END CATCH;
    ```

3. Using Savepoints:

    ```sql
    BEGIN TRANSACTION;

    UPDATE accounts
    SET balance = balance - 50
    WHERE account_id = 1;

    SAVEPOINT sp1;

    UPDATE accounts
    SET balance = balance + 50
    WHERE account_id = 2;

    -- An error occurs
    ROLLBACK TO SAVEPOINT sp1;

    UPDATE accounts
    SET balance = balance + 25
    WHERE account_id = 3;

    COMMIT;
    ```

4. Setting Isolation Levels:
    ```sql
    SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;

    BEGIN TRANSACTION;

    SELECT balance
    FROM accounts
    WHERE account_id = 1;

    -- Perform other operations...

    COMMIT;
    ```

### Summary
Transactions are essential for ensuring data integrity and consistency in SQL databases, particularly in multi-user environments. By understanding and effectively using transaction commands (BEGIN TRANSACTION, COMMIT, ROLLBACK), savepoints, and isolation levels, you can manage complex operations and handle errors gracefully. Mastery of these concepts will help you maintain a robust and reliable database system.

## 12. Database Views
### Database Views
A database view is a virtual table that provides a way to present data from one or more tables in a specific, pre-defined format. Views do not store data themselves; instead, they store a query that retrieves data from the underlying tables. This can simplify complex queries, enhance security by restricting access to certain data, and provide a consistent, abstracted way to access data.


#### Benefits of Views
* Simplification: Simplify complex queries by encapsulating them in a view.
* Security: Restrict access to specific rows and columns in the tables by providing selective access through views.
* Consistency: Ensure that users see consistent, formatted data.
Abstraction: Hide the complexity of the underlying database schema.


#### Creating Views
* Syntax:
    ```sql
    CREATE VIEW view_name AS
    SELECT column1, column2, ...
    FROM table_name
    WHERE condition;
    ```

* Example:
    ```sql
    CREATE VIEW EmployeeDetails AS
    SELECT first_name, last_name, department_id, salary
    FROM employees
    WHERE status = 'Active';
    ```
* Explanation: This view, EmployeeDetails, selects the first name, last name, department ID, and salary of active employees.

#### Querying Views
* Syntax:
    ```sql  
    SELECT column1, column2, ...
    FROM view_name
    WHERE condition;
    ```

* Example:
    ```sql
    SELECT * FROM EmployeeDetails WHERE department_id = 2;
    ```

* Explanation: This query retrieves all columns from the EmployeeDetails view for employees in department 2.

#### Updating Views
Views can sometimes be updatable, allowing you to insert, update, or delete rows in the underlying tables through the view. However, certain conditions must be met for a view to be updatable, such as not using aggregate functions, DISTINCT, GROUP BY, etc.

* Example:
    ```sql
    UPDATE EmployeeDetails
    SET salary = salary + 5000
    WHERE department_id = 2;
    ```

* Explanation: This query increases the salary of employees in department 2 by 5000 through the EmployeeDetails view.

#### Managing Views
* Altering Views:
    ```sql
    CREATE OR REPLACE VIEW view_name AS
    SELECT column1, column2, ...
    FROM table_name
    WHERE condition;
    ```

* Dropping Views:
    ```sql
    DROP VIEW view_name;
    ```
* Example:
    ```sql
    DROP VIEW EmployeeDetails;
    ```
* Explanation: This query removes the EmployeeDetails view from the database.

### Practical Examples
1. Creating a View:
    ```sql
    CREATE VIEW ActiveEmployees AS
    SELECT employee_id, first_name, last_name, department_id
    FROM employees
    WHERE status = 'Active';
    ```

2. Querying a View:
    ```sql
    SELECT * FROM ActiveEmployees WHERE department_id = 3;
    ```

3. Updating Data Through a View:
    ```sql
    UPDATE ActiveEmployees
    SET department_id = 4
    WHERE employee_id = 10;
    ```

4. Creating a Complex View:
    ```sql
    CREATE VIEW DepartmentSummary AS
    SELECT d.department_id, d.department_name, COUNT(e.employee_id) AS employee_count, AVG(e.salary) AS average_salary
    FROM departments d
    LEFT JOIN employees e ON d.department_id = e.department_id
    GROUP BY d.department_id, d.department_name;
    ```

5. Querying the Complex View:
    ```sql
    SELECT * FROM DepartmentSummary WHERE employee_count > 10;
    ```

6. Altering a View:
    ```sql
    CREATE OR REPLACE VIEW ActiveEmployees AS
    SELECT employee_id, first_name, last_name, department_id, hire_date
    FROM employees
    WHERE status = 'Active';
    ```

7. Dropping a View:
    ```sql
    DROP VIEW ActiveEmployees;
    ```

### Summary
Database views are powerful tools that provide a way to simplify complex queries, enhance security, ensure consistent data presentation, and abstract the underlying database schema. By using views, you can create virtual tables that encapsulate query logic, making it easier to manage and access data. Understanding how to create, query, update, and manage views is essential for effective database management and optimization.

## 13. More Performance Tuning
### Using LIMIT/OFFSET Efficiently
The LIMIT and OFFSET clauses are used to paginate through a large dataset by specifying the number of rows to return and the starting point within the result set. This is particularly useful for displaying results in a user-friendly way, such as in web applications.

* Syntax
  * LIMIT: Specifies the maximum number of rows to return.
  * OFFSET: Specifies the number of rows to skip before starting to return rows.
* Example
    ```sql
    SELECT column1, column2
    FROM table_name
    ORDER BY column1
    LIMIT 10 OFFSET 20;
    ```


* Explanation: This query retrieves 10 rows starting from the 21st row of the result set.
* Best Practices for Using LIMIT/OFFSET
  * Order By Clause: Always use ORDER BY with LIMIT and OFFSET to ensure consistent and predictable results.
  * Indexing: Ensure the columns used in the ORDER BY clause are indexed to improve performance.
  * Avoid Large OFFSETs: Large offsets can be inefficient because the database engine still processes the skipped rows. Consider using an alternative approach for deep pagination.
  * Keyset Pagination: For more efficient pagination, use keyset pagination instead of OFFSET for large datasets. This approach involves using a WHERE clause to filter results based on the last retrieved row.

* Keyset Pagination Example
    ```sql
    SELECT column1, column2
    FROM table_name
    WHERE column1 > last_retrieved_value
    ORDER BY column1
    LIMIT 10;
    ```

* Explanation: This query retrieves the next set of rows starting after the last retrieved value, which is more efficient than using large offsets.

### Caching Strategies
Caching is a technique to store frequently accessed data in a fast storage medium (like memory) to reduce the load on the database and improve query performance. Effective caching strategies can significantly enhance the performance of your application.

#### Types of Caching
* Application-Level Caching: Cache data within the application layer using tools like Memcached or Redis.
* Database-Level Caching: Some databases support internal caching mechanisms to store query results.
* HTTP Caching: For web applications, use HTTP headers to cache responses at the client or proxy level.

#### Best Practices for Caching
  * Cache Frequently Accessed Data: Identify and cache data that is frequently read but infrequently updated.
  * Invalidate Cache When Data Changes: Ensure that the cache is invalidated or updated when the underlying data changes to maintain consistency.
  * Use Appropriate Expiry Times: Set expiry times for cached data to ensure it is refreshed periodically.
  * Cache Key Design: Use a consistent and efficient key naming convention for caching.
  
#### Example: Using Redis for Caching
    
* Pseudo-Code:

    ```sql

    -- Check if the result is in the cache
    IF cache_exists('employees_department_1') THEN
        RETURN cache('employees_department_1');
    ELSE
        -- Query the database
        result = SELECT * FROM employees WHERE department_id = 1;
        -- Store the result in the cache
        cache('employees_department_1', result);
        RETURN result;
    END IF;
    ```

* Explanation: This pseudo-code checks if the query result is already cached. If it is, the result is returned from the cache. If not, the database is queried, the result is cached, and then returned.

#### Example: Database-Level Caching (MySQL Query Cache)
  * Enabling Query Cache:
    ```sql
    SET GLOBAL query_cache_size = 1048576;  -- 1MB cache size
    SET GLOBAL query_cache_type = 1;        -- Enable query cache
    ```

  * Using SQL_CACHE Hint:
    ```sql
    SELECT SQL_CACHE * FROM employees WHERE department_id = 1;
    ```

  * Explanation: This query instructs MySQL to cache the result of the query. Subsequent identical queries will return the cached result instead of querying the database again.

### Stored Procedures
Stored procedures are precompiled collections of one or more SQL statements that are stored in the database. They can be used to encapsulate complex business logic, improve performance, and ensure consistent execution of operations.

#### Benefits of Stored Procedures
* Performance: Stored procedures are precompiled and stored in the database, which can lead to faster execution compared to ad-hoc queries.
* Security: Stored procedures can help protect against SQL injection attacks by parameterizing inputs. Additionally, you can grant execute permissions to users without giving them direct access to the underlying tables.
* Maintainability: Encapsulating complex logic within stored procedures makes it easier to maintain and update the logic without changing the application code.
* Reusability: Once created, stored procedures can be reused across different applications and by different users.

#### Creating Stored Procedures
* Syntax:

  ```sql
  CREATE PROCEDURE procedure_name (parameters)
  BEGIN
      -- SQL statements
  END;
  ```
* Example:

  ```sql
  CREATE PROCEDURE GetEmployeeDetails (IN emp_id INT)
  BEGIN
      SELECT first_name, last_name, department_id, salary
      FROM employees
      WHERE employee_id = emp_id;
  END;
  ```
* Explanation: This stored procedure, GetEmployeeDetails, takes an employee ID as an input parameter and retrieves the corresponding employee details.

#### Executing Stored Procedures
* Syntax:

  ```sql
  CALL procedure_name (parameters);
  ```
* Example:
  ```sql
  CALL GetEmployeeDetails(1);
  ```

* Explanation: This command executes the GetEmployeeDetails stored procedure with the employee ID 1.

#### Using Parameters in Stored Procedures
* Input Parameters (IN): Used to pass values into the procedure.

* Output Parameters (OUT): Used to return values from the procedure.

* Input/Output Parameters (INOUT): Used to pass values into the procedure and return updated values.

##### Example with Input and Output Parameters:

```sql
CREATE PROCEDURE GetEmployeeSalary (IN emp_id INT, OUT emp_salary DECIMAL(10, 2))
BEGIN
    SELECT salary INTO emp_salary
    FROM employees
    WHERE employee_id = emp_id;
END;
```
##### Executing the Procedure with Output Parameter:

```sql
DECLARE @salary DECIMAL(10, 2);
CALL GetEmployeeSalary(1, @salary);
SELECT @salary;
```

* Explanation: This stored procedure, GetEmployeeSalary, takes an employee ID as an input parameter and returns the corresponding salary as an output parameter.

#### Error Handling in Stored Procedures
##### Example with Error Handling:

```sql
CREATE PROCEDURE UpdateEmployeeSalary (IN emp_id INT, IN new_salary DECIMAL(10, 2))
BEGIN
    DECLARE EXIT HANDLER FOR SQLEXCEPTION
    BEGIN
        -- Rollback any changes on error
        ROLLBACK;
    END;

    START TRANSACTION;
    UPDATE employees
    SET salary = new_salary
    WHERE employee_id = emp_id;
    COMMIT;
END;
```

* Explanation: This stored procedure, UpdateEmployeeSalary, updates an employee's salary within a transaction. If an error occurs, the transaction is rolled back to ensure data integrity.

#### Practical Examples
1. Creating a Simple Stored Procedure:

    ```sql
    CREATE PROCEDURE ListAllEmployees()
    BEGIN
        SELECT * FROM employees;
    END;
    ```

2. Executing the Simple Stored Procedure:

    ```sql
    CALL ListAllEmployees();
    ```
3. Stored Procedure with Input Parameter:

      ```sql
      CREATE PROCEDURE GetDepartmentEmployees (IN dept_id INT)
      BEGIN
          SELECT first_name, last_name
          FROM employees
          WHERE department_id = dept_id;
      END;
      ```
4. Executing the Stored Procedure with Input Parameter:

    ```sql
    CALL GetDepartmentEmployees(2);
    ```

5. Stored Procedure with Input and Output Parameters:

    ```sql
    CREATE PROCEDURE CountDepartmentEmployees (IN dept_id INT, OUT emp_count INT)
    BEGIN
        SELECT COUNT(*) INTO emp_count
        FROM employees
        WHERE department_id = dept_id;
    END;
    ```
6. Executing the Stored Procedure with Output Parameter:

    ```sql
    DECLARE @count INT;
    CALL CountDepartmentEmployees(2, @count);
    SELECT @count;
    ```

7. Stored Procedure with Error Handling:

    ```sql
    CREATE PROCEDURE DeleteEmployee (IN emp_id INT)
    BEGIN
        DECLARE EXIT HANDLER FOR SQLEXCEPTION
        BEGIN
            -- Rollback any changes on error
            ROLLBACK;
        END;

        START TRANSACTION;
        DELETE FROM employees
        WHERE employee_id = emp_id;
        COMMIT;
    END;
    ```
8. Executing the Stored Procedure with Error Handling:
    ```sql
    CALL DeleteEmployee(3);
    ```

### Summary
Efficiently using LIMIT and OFFSET clauses for pagination and implementing effective caching strategies are essential techniques for optimizing SQL query performance. Proper pagination ensures that queries are manageable and performant, even for large datasets. Caching reduces the load on the database and accelerates data retrieval by storing frequently accessed data in a faster storage medium. Combining these techniques can significantly enhance the performance and scalability of your database-driven applications.

Stored procedures are a powerful tool in SQL that can encapsulate complex business logic, improve performance, enhance security, and ensure consistent execution of operations. By using stored procedures, you can create reusable, maintainable, and efficient database operations that can be executed by different applications and users. Understanding how to create, execute, and manage stored procedures, along with proper error handling and use of parameters, is essential for effective database management and optimization.


## Notes:
* In Postgres, SERIAL is now

## Resources