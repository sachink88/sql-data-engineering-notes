<think>

We are creating a comprehensive SQL foundation document in Markdown format. The structure will be:
1. Introduction to SQL, DBMS, RDBMS
2. DDL (Data Definition Language) with basic structure and definitions
3. DML (Data Manipulation Language) with basic structure and definitions
4. DQL (Data Query Language) with basic structure and definitions
5. Query Execution Flow across different databases
6. Strong foundation for SQL starters

We'll create a single, well-structured Markdown file that covers all these topics in detail.
</think>

# 📘 SQL Foundation Guide: From Basics to Execution

This document provides a comprehensive foundation for understanding SQL, database management systems, and the core language components. It's designed for beginners and includes cross-database execution flows.

---

# 🔹 1. What is SQL?

## Definition
**SQL (Structured Query Language)** is a domain-specific language used in programming and designed for managing data held in a relational database management system (RDBMS), or for stream processing in a relational data stream management system.

## Key Characteristics
- **Declarative Language**: You specify what you want, not how to get it
- **Standardized**: ANSI/ISO standard with dialect variations
- **Set-based**: Operates on sets of data rather than individual records
- **Portable**: Core syntax works across all RDBMS platforms

## Components of SQL
```
SQL is divided into four main sub-languages:
1. DDL (Data Definition Language) - Defines database structure
2. DML (Data Manipulation Language) - Manages data within tables
3. DQL (Data Query Language) - Retrieves data from database
4. DCL (Data Control Language) - Controls access to database
```

---

# 🔹 2. What is DBMS?

## Definition
**DBMS (Database Management System)** is software that enables users to define, create, maintain and control access to the database.

## Key Functions
1. **Data Storage Management**: Stores data in structured format
2. **Data Manipulation**: Provides tools to add, modify, delete data
3. **Data Security**: Controls user access and permissions
4. **Data Integrity**: Ensures data consistency and accuracy
5. **Backup and Recovery**: Protects against data loss

## Types of DBMS
```
DBMS Categories:
├── Hierarchical DBMS
├── Network DBMS
├── Relational DBMS (RDBMS)
├── Object-Oriented DBMS
└── NoSQL DBMS
```

---

# 🔹 3. What is RDBMS?

## Definition
**RDBMS (Relational Database Management System)** is a database management system based on the relational model. Data is stored in tables (relations) and relationships are maintained through keys.

## Core Concepts
1. **Tables**: Data organized in rows and columns
2. **Rows (Records)**: Individual entries in a table
3. **Columns (Fields)**: Attributes of each record
4. **Keys**: Unique identifiers for records
5. **Relationships**: Connections between tables

## Key Components
```
RDBMS Architecture:
├── Tables (Relations)
├── Keys (Primary, Foreign, Unique)
├── Indexes (Performance optimization)
├── Views (Virtual tables)
├── Stored Procedures (Reusable code)
└── Triggers (Automatic actions)
```

## Popular RDBMS
| Database | Vendor | Key Features |
|----------|--------|-------------|
| SQL Server | Microsoft | Windows-centric, enterprise features |
| Oracle | Oracle Corp. | Enterprise-grade, high security |
| MySQL | Oracle (formerly Sun) | Open-source, web-friendly |
| PostgreSQL | Global Development Group | Open-source, standards-compliant |
| SQLite | D. Richard Hipp | Lightweight, serverless |

---

# 🔹 4. DDL (Data Definition Language)

## Definition
**DDL (Data Definition Language)** is used to define and modify the structure of database objects in the database.

## Purpose
- Create database objects (tables, indexes, views)
- Modify existing database objects
- Remove database objects
- Define constraints and relationships

## Basic Structure
```sql
DDL Command Syntax:
├── CREATE [OBJECT TYPE] [OBJECT NAME]
├── ALTER [OBJECT TYPE] [OBJECT NAME]
├── DROP [OBJECT TYPE] [OBJECT NAME]
├── TRUNCATE [TABLE NAME]
└── COMMENT ON [OBJECT] IS 'TEXT'
```

## Common DDL Commands

### CREATE
**Definition**: Creates new database objects
```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    department VARCHAR(50),
    salary DECIMAL(10, 2)
);
```

### ALTER
**Definition**: Modifies existing database objects
```sql
ALTER TABLE employees
ADD COLUMN hire_date DATE;

ALTER TABLE employees
MODIFY COLUMN name VARCHAR(150);

ALTER TABLE employees
DROP COLUMN hire_date;
```

### DROP
**Definition**: Removes database objects
```sql
DROP TABLE employees;
```

### TRUNCATE
**Definition**: Removes all rows from a table (fast operation)
```sql
TRUNCATE TABLE employees;
```

### Constraints in DDL
```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,                    -- Primary Key
    name VARCHAR(100) NOT NULL,            -- Not Null
    email VARCHAR(100) UNIQUE,             -- Unique
    department_id INT,                     -- Foreign Key
    salary DECIMAL(10, 2) CHECK (salary > 0), -- Check
    status VARCHAR(20) DEFAULT 'ACTIVE'     -- Default
);
```

---

# 🔹 5. DML (Data Manipulation Language)

## Definition
**DML (Data Manipulation Language)** is used to manage data within database objects. It allows users to insert, modify, and delete data.

## Purpose
- Insert new records into tables
- Update existing records
- Delete records from tables
- Manage transactions

## Basic Structure
```sql
DML Command Syntax:
├── INSERT INTO [TABLE] (COLUMNS) VALUES (VALUES)
├── UPDATE [TABLE] SET [COLUMN=VALUE] WHERE [CONDITION]
├── DELETE FROM [TABLE] WHERE [CONDITION]
└── MERGE INTO [TABLE] ... (UPSERT operation)
```

## Common DML Commands

### INSERT
**Definition**: Adds new rows to a table
```sql
-- Insert specific columns
INSERT INTO employees (id, name, department, salary)
VALUES (1, 'John Doe', 'IT', 75000);

-- Insert all columns
INSERT INTO employees
VALUES (2, 'Jane Smith', 'HR', 65000);

-- Insert multiple rows
INSERT INTO employees (id, name, department, salary)
VALUES 
    (3, 'Mike Johnson', 'Finance', 80000),
    (4, 'Sarah Williams', 'IT', 72000),
    (5, 'David Brown', 'Marketing', 68000);
```

### UPDATE
**Definition**: Modifies existing rows in a table
```sql
-- Update single row
UPDATE employees
SET salary = 78000
WHERE id = 1;

-- Update multiple columns
UPDATE employees
SET department = 'IT', salary = 70000
WHERE id = 2;

-- Update multiple rows
UPDATE employees
SET salary = salary * 1.05
WHERE department = 'IT';
```

### DELETE
**Definition**: Removes rows from a table
```sql
-- Delete specific row
DELETE FROM employees
WHERE id = 5;

-- Delete multiple rows
DELETE FROM employees
WHERE department = 'Marketing';

-- Delete all rows (use TRUNCATE for better performance)
DELETE FROM employees;
```

### MERGE (UPSERT)
**Definition**: Combines insert and update operations
```sql
-- SQL Server/Oracle syntax
MERGE INTO employees AS target
USING (SELECT 6, 'Tom Wilson', 'IT', 76000) AS source
ON (target.id = source.id)
WHEN MATCHED THEN
    UPDATE SET name = source.name, department = source.department
WHEN NOT MATCHED THEN
    INSERT (id, name, department, salary)
    VALUES (source.id, source.name, source.department, source.salary);
```

---

# 🔹 6. DQL (Data Query Language)

## Definition
**DQL (Data Query Language)** is used to retrieve data from the database. It's the most commonly used part of SQL.

## Purpose
- Retrieve specific data from database
- Filter and sort results
- Aggregate and summarize data
- Join multiple tables for complex queries

## Basic Structure
```sql
DQL Command Syntax:
SELECT [COLUMNS]
FROM [TABLE(S)]
WHERE [CONDITIONS]
GROUP BY [COLUMNS]
HAVING [CONDITIONS]
ORDER BY [COLUMNS]
LIMIT [ROWS];
```

## Common DQL Commands

### Basic SELECT
**Definition**: Retrieves data from database
```sql
-- Select all columns
SELECT * FROM employees;

-- Select specific columns
SELECT id, name, department FROM employees;

-- Select with alias
SELECT id AS employee_id, name AS employee_name FROM employees;
```

### WHERE Clause
**Definition**: Filters rows based on conditions
```sql
-- Comparison operators
SELECT * FROM employees WHERE salary > 70000;

-- Logical operators
SELECT * FROM employees 
WHERE department = 'IT' AND salary > 70000;

-- Pattern matching
SELECT * FROM employees WHERE name LIKE 'J%';

-- IN operator
SELECT * FROM employees WHERE department IN ('IT', 'Finance');

-- BETWEEN operator
SELECT * FROM employees WHERE salary BETWEEN 60000 AND 80000;

-- NULL handling
SELECT * FROM employees WHERE manager_id IS NULL;
```

### GROUP BY and Aggregate Functions
**Definition**: Groups rows and calculates aggregates
```sql
-- Basic aggregation
SELECT department, COUNT(*) AS employee_count
FROM employees
GROUP BY department;

-- Multiple aggregates
SELECT 
    department,
    COUNT(*) AS employee_count,
    AVG(salary) AS avg_salary,
    MAX(salary) AS max_salary,
    MIN(salary) AS min_salary
FROM employees
GROUP BY department;

-- HAVING clause (filter groups)
SELECT 
    department,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 70000;
```

### ORDER BY
**Definition**: Sorts result set
```sql
-- Ascending order
SELECT * FROM employees ORDER BY name;

-- Descending order
SELECT * FROM employees ORDER BY salary DESC;

-- Multiple columns
SELECT * FROM employees ORDER BY department, salary DESC;
```

### LIMIT (Row Limiting)
**Definition**: Restricts number of rows returned
```sql
-- SQL Server
SELECT TOP 10 * FROM employees ORDER BY salary DESC;

-- MySQL/PostgreSQL
SELECT * FROM employees ORDER BY salary DESC LIMIT 10;

-- Oracle
SELECT * FROM employees WHERE ROWNUM <= 10 ORDER BY salary DESC;
```

---

# 🔹 7. Query Execution Flow (Cross-Database)

## General Execution Order
Regardless of the database system, SQL queries follow a logical execution order:

```
1. FROM (including JOINs)
2. WHERE
3. GROUP BY
4. HAVING
5. SELECT
6. DISTINCT
7. ORDER BY
8. LIMIT/TOP (varies by database)
```

## Detailed Execution Flow

### Step 1: FROM Clause
- Identifies source tables
- Applies JOIN operations
- Creates virtual table (V1)

```sql
-- Example
FROM employees e
JOIN departments d ON e.dept_id = d.id
```

### Step 2: WHERE Clause
- Filters rows based on conditions
- Creates virtual table (V2)

```sql
-- Example
WHERE e.salary > 50000 AND d.location = 'New York'
```

### Step 3: GROUP BY Clause
- Groups rows by specified columns
- Creates virtual table (V3)

```sql
-- Example
GROUP BY d.department_name
```

### Step 4: HAVING Clause
- Filters groups based on conditions
- Creates virtual table (V4)

```sql
-- Example
HAVING COUNT(e.id) > 5
```

### Step 5: SELECT Clause
- Selects specified columns
- Applies aliases and expressions
- Creates virtual table (V5)

```sql
-- Example
SELECT 
    d.department_name,
    COUNT(e.id) AS employee_count,
    AVG(e.salary) AS avg_salary
```

### Step 6: DISTINCT Clause
- Removes duplicate rows
- Creates virtual table (V6)

```sql
-- Example
SELECT DISTINCT d.department_name
```

### Step 7: ORDER BY Clause
- Sorts result set
- Creates virtual table (V7)

```sql
-- Example
ORDER BY avg_salary DESC
```

### Step 8: LIMIT/TOP Clause (Database-Specific)
- Restricts number of rows
- Creates final result set

```sql
-- SQL Server
SELECT TOP 5 ...

-- MySQL/PostgreSQL
... LIMIT 5

-- Oracle
... WHERE ROWNUM <= 5
```

## Cross-Database Execution Differences

### SQL Server Execution
```sql
-- Execution Flow
1. FROM
2. ON (JOIN conditions)
3. WHERE
4. GROUP BY
5. WITH CUBE/ROLLUP
6. HAVING
7. SELECT
8. DISTINCT
9. ORDER BY
10. TOP

-- Example
SELECT TOP 5 
    d.department_name,
    COUNT(e.id) AS employee_count
FROM employees e
JOIN departments d ON e.dept_id = d.id
WHERE e.status = 'Active'
GROUP BY d.department_name
HAVING COUNT(e.id) > 0
ORDER BY COUNT(e.id) DESC;
```

### MySQL Execution
```sql
-- Execution Flow
1. FROM
2. ON (JOIN conditions)
3. WHERE
4. GROUP BY
5. HAVING
6. SELECT
7. DISTINCT
8. ORDER BY
9. LIMIT

-- Example
SELECT 
    d.department_name,
    COUNT(e.id) AS employee_count
FROM employees e
JOIN departments d ON e.dept_id = d.id
WHERE e.status = 'Active'
GROUP BY d.department_name
HAVING COUNT(e.id) > 0
ORDER BY COUNT(e.id) DESC
LIMIT 5;
```

### PostgreSQL Execution
```sql
-- Execution Flow
1. FROM
2. WHERE
3. GROUP BY
4. HAVING
5. WINDOW functions
6. SELECT
7. DISTINCT
8. ORDER BY
9. LIMIT
10. OFFSET

-- Example
SELECT 
    d.department_name,
    COUNT(e.id) AS employee_count
FROM employees e
JOIN departments d ON e.dept_id = d.id
WHERE e.status = 'Active'
GROUP BY d.department_name
HAVING COUNT(e.id) > 0
ORDER BY COUNT(e.id) DESC
LIMIT 5 OFFSET 0;
```

### Oracle Execution
```sql
-- Execution Flow
1. FROM
2. WHERE
3. START WITH (CONNECT BY)
4. CONNECT BY
5. GROUP BY
6. HAVING
7. MODEL
8. SELECT
9. DISTINCT
10. ORDER BY
11. ROWNUM/FETCH FIRST

-- Example
SELECT 
    d.department_name,
    COUNT(e.id) AS employee_count
FROM employees e
JOIN departments d ON e.dept_id = d.id
WHERE e.status = 'Active'
GROUP BY d.department_name
HAVING COUNT(e.id) > 0
ORDER BY COUNT(e.id) DESC
FETCH FIRST 5 ROWS ONLY;
```

---

# 🔹 8. Building a Strong SQL Foundation

## Essential Concepts to Master

### 1. Database Design Fundamentals
- **Normalization**: Organize data to reduce redundancy
- **Primary Keys**: Unique identifier for each record
- **Foreign Keys**: Relationships between tables
- **Indexes**: Improve query performance

### 2. Core SQL Skills
```
SQL Skill Hierarchy:
├── Basic Queries (SELECT, FROM, WHERE)
├── Filtering (AND, OR, IN, LIKE, BETWEEN)
├── Joins (INNER, LEFT, RIGHT, FULL)
├── Aggregation (GROUP BY, HAVING)
├── Subqueries (Nested SELECTs)
├── Advanced (Window Functions, CTEs)
└── Optimization (Indexes, Execution Plans)
```

### 3. Best Practices for Beginners
1. **Start Simple**: Master basic SELECT before complex queries
2. **Understand Your Data**: Know table structures and relationships
3. **Test Incrementally**: Build queries step by step
4. **Use Comments**: Document complex logic
5. **Format Consistently**: Use proper indentation and capitalization

### 4. Learning Path
```
SQL Learning Journey:
Week 1: Basic SELECT statements
Week 2: Filtering and sorting
Week 3: Joins and relationships
Week 4: Aggregation and grouping
Week 5: Subqueries and CTEs
Week 6: Advanced functions
Week 7: Performance basics
Week 8: Real-world projects
```

### 5. Common Pitfalls to Avoid
1. **SELECT *** - Only select needed columns
2. **Missing WHERE** - Always filter when possible
3. **Incorrect JOINs** - Understand relationship types
4. **NULL Handling** - Use IS NULL/IS NOT NULL
5. **Transaction Management** - Use BEGIN/COMMIT/ROLLBACK

---

# 🔹 9. Practical Examples for Beginners

## Example 1: Basic Query
```sql
-- Retrieve all employees
SELECT * FROM employees;

-- Retrieve specific columns
SELECT id, name, department FROM employees;

-- Retrieve with alias
SELECT id AS employee_id, name AS employee_name FROM employees;
```

## Example 2: Filtering Data
```sql
-- Single condition
SELECT * FROM employees WHERE department = 'IT';

-- Multiple conditions with AND
SELECT * FROM employees 
WHERE department = 'IT' AND salary > 70000;

-- Multiple conditions with OR
SELECT * FROM employees 
WHERE department = 'IT' OR department = 'Finance';

-- Using IN operator
SELECT * FROM employees 
WHERE department IN ('IT', 'Finance', 'HR');

-- Using LIKE for pattern matching
SELECT * FROM employees 
WHERE name LIKE 'S%';

-- Using BETWEEN for range
SELECT * FROM employees 
WHERE salary BETWEEN 50000 AND 80000;

-- Handling NULL values
SELECT * FROM employees 
WHERE manager_id IS NULL;
```

## Example 3: Sorting and Limiting
```sql
-- Sort by single column
SELECT * FROM employees ORDER BY name;

-- Sort by multiple columns
SELECT * FROM employees ORDER BY department, name;

-- Sort descending
SELECT * FROM employees ORDER BY salary DESC;

-- Limit results (SQL Server)
SELECT TOP 10 * FROM employees ORDER BY salary DESC;

-- Limit results (MySQL/PostgreSQL)
SELECT * FROM employees ORDER BY salary DESC LIMIT 10;

-- Limit results (Oracle)
SELECT * FROM employees 
WHERE ROWNUM <= 10 
ORDER BY salary DESC;
```

## Example 4: Basic Joins
```sql
-- Inner Join (matching rows only)
SELECT e.name, d.department_name
FROM employees e
INNER JOIN departments d ON e.dept_id = d.id;

-- Left Join (all employees, with departments if available)
SELECT e.name, d.department_name
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.id;

-- Right Join (all departments, with employees if available)
SELECT e.name, d.department_name
FROM employees e
RIGHT JOIN departments d ON e.dept_id = d.id;

-- Full Join (all employees and departments)
SELECT e.name, d.department_name
FROM employees e
FULL JOIN departments d ON e.dept_id = d.id;
```

## Example 5: Aggregation
```sql
-- Count employees by department
SELECT department, COUNT(*) AS employee_count
FROM employees
GROUP BY department;

-- Average salary by department
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department;

-- Multiple aggregates
SELECT 
    department,
    COUNT(*) AS employee_count,
    AVG(salary) AS avg_salary,
    MAX(salary) AS max_salary,
    MIN(salary) AS min_salary
FROM employees
GROUP BY department;

-- Filter aggregated results
SELECT 
    department,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 70000;
```

---

# 🔹 10. Summary and Next Steps

## Key Takeaways
1. **SQL** is a standardized language for relational databases
2. **DBMS** manages data storage and retrieval
3. **RDBMS** organizes data in related tables
4. **DDL** defines database structure
5. **DML** manipulates data within tables
6. **DQL** retrieves data from databases
7. **Query execution** follows a logical order across all databases

## For Strong SQL Foundation
1. **Practice Regularly**: Write queries daily
2. **Understand Execution**: Know how queries are processed
3. **Learn Database Design**: Understand normalization and relationships
4. **Master Core Concepts**: Focus on SELECT, FROM, WHERE, JOIN, GROUP BY
5. **Explore Advanced Topics**: Window functions, CTEs, optimization

## Recommended Resources
- **Online Courses**: Khan Academy, Coursera, Udemy
- **Documentation**: Official docs for your RDBMS
- **Practice Platforms**: LeetCode, HackerRank, SQLZoo
- **Books**: "SQL in 10 Minutes" by Ben Forta
- **Communities**: Stack Overflow, Reddit r/SQL

---

This comprehensive guide provides a solid foundation for understanding SQL, database systems, and the core language components. By mastering these concepts and practicing regularly, you'll build a strong foundation for working with relational databases and writing efficient SQL queries across different database systems.


-----

# 📘 SQL Master Cheat Sheet (Cross-Database)

## Table of Contents
1. Core SQL Keywords (DQL)
2. Row Limiting
3. Joins
4. Set Operations
5. Aggregate Functions
6. DML (Data Manipulation)
7. DDL (Data Definition)
8. Constraints
9. Transactions
10. String Functions
11. Date Functions
12. Comparison Operators
13. Logical Operators
14. Example Queries
15. Global Keyword Map
16. Why Differences Exist (Important)
17. Data Engineering Keywords
18. Best Practices
19. Common Mistakes
20. Final Summary

## Each section will include:
- Syntax and examples
- Cross-database differences where applicable
- Notes and best practices


# 📘 SQL Master Cheat Sheet (Cross-Database)

## This document covers:
- SQL Keywords
- Operators (Comparison + Logical)
- Cross-Database Differences
- Data Engineering Notes

## Supports:
- ## SQL Server | MySQL | PostgreSQL | Oracle

---

# 🔹 1. Core SQL Keywords (DQL)

| Keyword | Syntax | Notes |
|--------|--------|------|
| SELECT | SELECT col FROM table | Retrieve data |
| FROM | FROM table | Source table |
| WHERE | WHERE condition | Filtering |
| GROUP BY | GROUP BY col | Aggregation |
| HAVING | HAVING condition | Filter groups |
| ORDER BY | ORDER BY col ASC/DESC | Sorting |

---

# 🔹 2. Row Limiting

| Database | Syntax |
|----------|--------|
| SQL Server | `SELECT TOP n * FROM table` |
| MySQL | `SELECT * FROM table LIMIT n` |
| PostgreSQL | `LIMIT n OFFSET m` |
| Oracle | `ROWNUM <= n` or `FETCH FIRST n ROWS ONLY` |

**Example:**
```sql
-- SQL Server
SELECT TOP 10 * FROM employees;

-- MySQL/PostgreSQL
SELECT * FROM employees LIMIT 10;

-- Oracle
SELECT * FROM employees WHERE ROWNUM <= 10;
```

---

# 🔹 3. Joins

| Join Type | Syntax | Notes |
|-----------|--------|-------|
| INNER JOIN | `FROM table1 INNER JOIN table2 ON table1.id = table2.id` | Returns matching rows |
| LEFT JOIN | `FROM table1 LEFT JOIN table2 ON table1.id = table2.id` | Returns all rows from left table |
| RIGHT JOIN | `FROM table1 RIGHT JOIN table2 ON table1.id = table2.id` | Returns all rows from right table |
| FULL JOIN | `FROM table1 FULL JOIN table2 ON table1.id = table2.id` | Returns all rows from both tables |

👉 Oracle uses `OUTER` keyword explicitly: `LEFT OUTER JOIN`

**Example:**
```sql
SELECT e.name, d.department_name
FROM employees e
INNER JOIN departments d ON e.dept_id = d.id;
```

---

# 🔹 4. Set Operations

| Operation | SQL Server | MySQL | PostgreSQL | Oracle |
|----------|------------|-------|------------|--------|
| UNION | ✔ | ✔ | ✔ | ✔ |
| UNION ALL | ✔ | ✔ | ✔ | ✔ |
| INTERSECT | ✔ | ✔ | ✔ | ✔ |
| EXCEPT | ✔ | ✔ | ✔ | ❌ |
| MINUS | ❌ | ❌ | ❌ | ✔ |

**Example:**
```sql
-- Works in all databases
SELECT employee_id FROM employees_2020
UNION
SELECT employee_id FROM employees_2021;

-- Oracle uses MINUS instead of EXCEPT
SELECT employee_id FROM employees_2020
MINUS
SELECT employee_id FROM employees_2021;
```

---

# 🔹 5. Aggregate Functions

| Function | Syntax | Description |
|----------|--------|-------------|
| SUM() | `SUM(column)` | Returns the sum of values |
| AVG() | `AVG(column)` | Returns the average value |
| COUNT() | `COUNT(column)` or `COUNT(*)` | Counts rows or non-null values |
| MIN() | `MIN(column)` | Returns minimum value |
| MAX() | `MAX(column)` | Returns maximum value |

**Example:**
```sql
SELECT 
    COUNT(*) AS total_employees,
    AVG(salary) AS average_salary,
    MAX(salary) AS highest_salary
FROM employees;
```

---

# 🔹 6. DML (Data Manipulation)

| Command | Syntax | Description |
|---------|--------|-------------|
| INSERT | `INSERT INTO table VALUES (val1, val2)` | Adds new rows |
| UPDATE | `UPDATE table SET col=value WHERE condition` | Modifies existing rows |
| DELETE | `DELETE FROM table WHERE condition` | Removes rows |

**Examples:**
```sql
-- Insert new employee
INSERT INTO employees (name, department, salary)
VALUES ('John Doe', 'IT', 75000);

-- Update salary
UPDATE employees
SET salary = 80000
WHERE name = 'John Doe';

-- Delete employee
DELETE FROM employees
WHERE name = 'John Doe';
```

---

# 🔹 7. DDL (Data Definition)

| Command | Syntax | Description |
|---------|--------|-------------|
| CREATE TABLE | `CREATE TABLE table (col type, ...)` | Creates new table |
| ALTER TABLE | `ALTER TABLE table ADD column` | Modifies table structure |
| DROP TABLE | `DROP TABLE table` | Removes table |
| TRUNCATE | `TRUNCATE TABLE table` | Removes all rows (fast) |

**Examples:**
```sql
-- Create table
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    department VARCHAR(50),
    salary DECIMAL(10, 2)
);

-- Add column
ALTER TABLE employees ADD hire_date DATE;

-- Drop table
DROP TABLE employees;

-- Truncate table (remove all data)
TRUNCATE TABLE employees;
```

---

# 🔹 8. Constraints

| Constraint | Syntax | Description |
|------------|--------|-------------|
| PRIMARY KEY | `PRIMARY KEY (col)` | Unique identifier |
| FOREIGN KEY | `FOREIGN KEY (col) REFERENCES table(col)` | Referential integrity |
| NOT NULL | `col type NOT NULL` | Must have value |
| UNIQUE | `col type UNIQUE` | All values unique |
| CHECK | `col type CHECK (condition)` | Value must satisfy condition |
| DEFAULT | `col type DEFAULT value` | Default value |

**Example:**
```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    department VARCHAR(50) DEFAULT 'Unassigned',
    salary DECIMAL(10, 2) CHECK (salary > 0),
    manager_id INT,
    FOREIGN KEY (manager_id) REFERENCES employees(id)
);
```

---

# 🔹 9. Transactions

| Command | Syntax | Description |
|---------|--------|-------------|
| BEGIN TRANSACTION | `BEGIN TRANSACTION` | Starts transaction |
| COMMIT | `COMMIT` | Saves changes |
| ROLLBACK | `ROLLBACK` | Undoes changes |
| SAVEPOINT | `SAVEPOINT name` | Creates savepoint |

**Examples:**
```sql
-- SQL Server
BEGIN TRANSACTION;
    UPDATE accounts SET balance = balance - 100 WHERE id = 1;
    UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;

-- MySQL
START TRANSACTION;
    -- operations
COMMIT;

-- PostgreSQL
BEGIN;
    -- operations
COMMIT;

-- Oracle
SET TRANSACTION;
    -- operations
COMMIT;
```

---

# 🔹 10. String Functions

| Function | SQL Server | Others | Description |
|----------|------------|--------|-------------|
| Length | `LEN()` | `LENGTH()` | Returns string length |
| Substring | `SUBSTRING()` | `SUBSTR()` (Oracle) | Extracts substring |
| Concatenation | `CONCAT()` | `CONCAT()` / `||` | Combines strings |
| Lowercase | `LOWER()` | `LOWER()` | Converts to lowercase |
| Uppercase | `UPPER()` | `UPPER()` | Converts to uppercase |
| Replace | `REPLACE()` | `REPLACE()` | Replaces substring |

**Examples:**
```sql
-- Length (SQL Server)
SELECT LEN('Hello') AS length;

-- Length (Others)
SELECT LENGTH('Hello') AS length;

-- Substring (SQL Server, MySQL, PostgreSQL)
SELECT SUBSTRING('Hello World', 1, 5) AS substring;

-- Substring (Oracle)
SELECT SUBSTR('Hello World', 1, 5) AS substring;

-- Concatenation
SELECT CONCAT('Hello', ' ', 'World') AS greeting;

-- Oracle also supports || operator
SELECT 'Hello' || ' ' || 'World' AS greeting FROM DUAL;

-- Lowercase
SELECT LOWER('HELLO') AS lowercase;

-- Uppercase
SELECT UPPER('hello') AS uppercase;

-- Replace
SELECT REPLACE('Hello World', 'World', 'SQL') AS replaced;
```

---

# 🔹 11. Date Functions

| Purpose | SQL Server | MySQL/PostgreSQL | Oracle |
|---------|------------|------------------|--------|
| Current Date | `GETDATE()` | `NOW()` or `CURRENT_TIMESTAMP` | `SYSDATE` |
| Add Date | `DATEADD()` | `DATE_ADD()` or `+` | `+` |
| Date Diff | `DATEDIFF()` | `TIMESTAMPDIFF()` or `-` | `-` |

**Examples:**
```sql
-- Current date/time
-- SQL Server
SELECT GETDATE() AS current_datetime;

-- MySQL/PostgreSQL
SELECT NOW() AS current_datetime;

-- Oracle
SELECT SYSDATE AS current_datetime FROM DUAL;

-- Add 7 days to current date
-- SQL Server
SELECT DATEADD(day, 7, GETDATE()) AS next_week;

-- MySQL
SELECT DATE_ADD(NOW(), INTERVAL 7 DAY) AS next_week;

-- PostgreSQL
SELECT NOW() + INTERVAL '7 days' AS next_week;

-- Oracle
SELECT SYSDATE + 7 AS next_week FROM DUAL;

-- Date difference in days
-- SQL Server
SELECT DATEDIFF(day, '2023-01-01', '2023-01-10') AS days_diff;

-- MySQL
SELECT TIMESTAMPDIFF(DAY, '2023-01-01', '2023-01-10') AS days_diff;

-- PostgreSQL
SELECT DATE('2023-01-10') - DATE('2023-01-01') AS days_diff;

-- Oracle
SELECT TO_DATE('2023-01-10') - TO_DATE('2023-01-01') AS days_diff FROM DUAL;
```

---

# 🔹 12. Comparison Operators

| Operation | SQL Server | MySQL | PostgreSQL | Oracle | Example |
|-----------|------------|-------|------------|--------|---------|
| Equal | = | = | = | = | `WHERE salary = 50000` |
| Not Equal | <> / != | <> / != | <> / != | <> | `WHERE salary <> 50000` |
| Greater Than | > | > | > | > | `WHERE salary > 50000` |
| Less Than | < | < | < | < | `WHERE salary < 50000` |
| Greater or Equal | >= | >= | >= | >= | `WHERE salary >= 50000` |
| Less or Equal | <= | <= | <= | <= | `WHERE salary <= 50000` |
| Between | BETWEEN | BETWEEN | BETWEEN | BETWEEN | `WHERE salary BETWEEN 30000 AND 70000` |
| In List | IN | IN | IN | IN | `WHERE department IN ('HR','IT')` |
| Like Pattern | LIKE | LIKE | LIKE | LIKE | `WHERE name LIKE 'S%'` |
| Null Check | IS NULL | IS NULL | IS NULL | IS NULL | `WHERE end_date IS NULL` |
| Not Null | IS NOT NULL | IS NOT NULL | IS NOT NULL | IS NOT NULL | `WHERE end_date IS NOT NULL` |

**Examples:**
```sql
-- Equal
SELECT * FROM employees WHERE salary = 50000;

-- Not equal
SELECT * FROM employees WHERE salary <> 50000;

-- Greater than
SELECT * FROM employees WHERE salary > 50000;

-- Less than
SELECT * FROM employees WHERE salary < 50000;

-- Greater or equal
SELECT * FROM employees WHERE salary >= 50000;

-- Less or equal
SELECT * FROM employees WHERE salary <= 50000;

-- Between
SELECT * FROM employees WHERE salary BETWEEN 30000 AND 70000;

-- In list
SELECT * FROM employees WHERE department IN ('HR','IT','Finance');

-- Like pattern (starts with 'S')
SELECT * FROM employees WHERE name LIKE 'S%';

-- Like pattern (contains 'son')
SELECT * FROM employees WHERE name LIKE '%son%';

-- Like pattern (ends with 'n')
SELECT * FROM employees WHERE name LIKE '%n';

-- Null check
SELECT * FROM employees WHERE end_date IS NULL;

-- Not null check
SELECT * FROM employees WHERE end_date IS NOT NULL;
```

---

# 🔹 13. Logical Operators

| Operator | Example | Description |
|----------|---------|-------------|
| AND | `WHERE salary > 50000 AND department = 'IT'` | All conditions must be true |
| OR | `WHERE department = 'HR' OR department = 'IT'` | At least one condition must be true |
| NOT | `WHERE NOT (salary > 50000)` | Negates condition |
| ANY | `WHERE salary > ANY (SELECT salary FROM contractors)` | Compares to any value in subquery |
| ALL | `WHERE salary > ALL (SELECT salary FROM contractors)` | Compares to all values in subquery |
| SOME | Same as ANY | Same as ANY |

**Examples:**
```sql
-- AND operator
SELECT * FROM employees 
WHERE salary > 50000 AND department = 'IT';

-- OR operator
SELECT * FROM employees 
WHERE department = 'HR' OR department = 'IT';

-- NOT operator
SELECT * FROM employees 
WHERE NOT (salary > 50000);

-- Combining AND and OR
SELECT * FROM employees 
WHERE (department = 'HR' OR department = 'IT')
AND salary > 50000;

-- Using parentheses for clarity
SELECT * FROM employees 
WHERE (department = 'HR' OR department = 'IT')
AND (salary > 50000 AND salary < 100000);

-- ANY operator
SELECT * FROM employees
WHERE salary > ANY (SELECT salary FROM contractors WHERE status = 'active');

-- ALL operator
SELECT * FROM employees
WHERE salary > ALL (SELECT salary FROM contractors);
```

---

# 🔹 14. Example Queries

```sql
-- Basic filtering
SELECT * FROM employees
WHERE salary >= 50000
AND department = 'IT';

-- Using BETWEEN
SELECT * FROM employees
WHERE salary BETWEEN 30000 AND 70000
AND department IN ('HR','IT','Finance');

-- Pattern matching
SELECT * FROM employees
WHERE name LIKE 'S%'
AND department = 'IT';

-- Date filtering
SELECT * FROM employees
WHERE hire_date >= '2020-01-01'
AND hire_date <= '2023-12-31';

-- Using IS NULL
SELECT * FROM employees
WHERE end_date IS NULL;

-- Combining conditions
SELECT * FROM employees
WHERE (department = 'IT' OR department = 'Finance')
AND salary > 60000
AND end_date IS NULL;

-- Using subquery
SELECT * FROM employees
WHERE department_id IN (
    SELECT id FROM departments 
    WHERE location = 'New York'
);
```

---

# 🔹 15. Global Keyword Map

| Category | SQL Server | MySQL | PostgreSQL | Oracle |
|----------|------------|-------|------------|--------|
| Row Limiting | TOP | LIMIT | LIMIT | ROWNUM |
| Set Difference | EXCEPT | EXCEPT | EXCEPT | MINUS |
| Auto Increment | IDENTITY | AUTO_INCREMENT | SERIAL | SEQUENCE |
| Current Date | GETDATE() | NOW() | CURRENT_TIMESTAMP | SYSDATE |
| String Length | LEN() | LENGTH() | LENGTH() | LENGTH() |
| Substring | SUBSTRING() | SUBSTRING() | SUBSTRING() | SUBSTR() |
| Concatenation | CONCAT() | CONCAT() | CONCAT() / || | CONCAT() / || |
| Dummy Table | Not needed | Not needed | Not needed | DUAL |
| Upsert | MERGE | INSERT...ON DUPLICATE KEY UPDATE | INSERT...ON CONFLICT | MERGE |
| Output Clause | OUTPUT | Not supported | RETURNING | RETURNING |
| Hierarchical | Not native | Not native | WITH RECURSIVE | CONNECT BY |

---

# 🔹 16. Why Differences Exist (Important)

Database differences exist because systems evolved separately:

* **SQL Server** → Enterprise-focused with strong stored procedure support
* **MySQL** → Web-focused, simple, and fast for read-heavy workloads
* **PostgreSQL** → Standards-compliant with advanced features and extensibility
* **Oracle** → Legacy enterprise systems with focus on control and security

**Key Evolution Points:**
1. **ANSI SQL Compliance** - PostgreSQL follows standards most closely
2. **Performance Focus** - MySQL optimized for web applications
3. **Enterprise Features** - SQL Server and Oracle have advanced security and management
4. **Legacy Support** - Oracle maintains backward compatibility for older systems

---

# 🔹 17. Data Engineering Keywords

| Keyword | Usage | Example |
|---------|-------|---------|
| CASE | Conditional logic | `CASE WHEN condition THEN result END` |
| COALESCE | Handle NULL values | `COALESCE(col1, col2, 'default')` |
| CTE (WITH) | Temporary dataset | `WITH cte AS (SELECT ...)` |
| MERGE | Upsert operation | `MERGE INTO target ...` |
| RETURNING | Get inserted data | `INSERT ... RETURNING id` |
| TRUNCATE | Fast delete | `TRUNCATE TABLE table` |
| PARTITION BY | Window function grouping | `SUM(col) OVER (PARTITION BY dept)` |
| OVER | Window function | `RANK() OVER (ORDER BY salary)` |
| RANK | Ranking function | `RANK() OVER (ORDER BY salary DESC)` |
| DENSE_RANK | Ranking without gaps | `DENSE_RANK() OVER (ORDER BY salary DESC)` |
| ROW_NUMBER | Row numbering | `ROW_NUMBER() OVER (ORDER BY name)` |
| LEAD | Access next row | `LEAD(salary) OVER (ORDER BY hire_date)` |
| LAG | Access previous row | `LAG(salary) OVER (ORDER BY hire_date)` |

**Examples:**
```sql
-- CASE expression
SELECT 
    name,
    salary,
    CASE 
        WHEN salary > 100000 THEN 'High'
        WHEN salary > 50000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_level
FROM employees;

-- COALESCE for NULL handling
SELECT 
    name,
    COALESCE(manager_name, 'No Manager') AS manager
FROM employees;

-- CTE (Common Table Expression)
WITH dept_stats AS (
    SELECT 
        department_id,
        COUNT(*) AS employee_count,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
)
SELECT d.department_name, ds.employee_count, ds.avg_salary
FROM departments d
JOIN dept_stats ds ON d.id = ds.department_id;

-- Window functions
SELECT 
    name,
    department,
    salary,
    RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS dept_rank,
    ROW_NUMBER() OVER (ORDER BY salary DESC) AS overall_rank
FROM employees;

-- LEAD and LAG
SELECT 
    name,
    salary,
    LAG(salary, 1, 0) OVER (ORDER BY hire_date) AS prev_salary,
    LEAD(salary, 1, 0) OVER (ORDER BY hire_date) AS next_salary
FROM employees
WHERE department = 'IT';
```

---

# 🔹 18. Best Practices

✅ **Use ANSI SQL** when possible for portability:
```sql
-- Good (portable)
SELECT e.name, d.department_name
FROM employees e
INNER JOIN departments d ON e.dept_id = d.id;
```

✅ **Write portable queries** by avoiding database-specific features:
```sql
-- Instead of database-specific row limiting:
-- SQL Server: SELECT TOP 10 ...
-- MySQL/PostgreSQL: SELECT ... LIMIT 10
-- Oracle: SELECT ... WHERE ROWNUM <= 10

-- Use OFFSET-FETCH (ANSI standard when possible)
SELECT * FROM employees
ORDER BY salary DESC
OFFSET 0 ROWS FETCH NEXT 10 ROWS ONLY;
```

✅ **Document DB-specific logic**:
```sql
-- PostgreSQL specific
INSERT INTO employees (name) VALUES ('John') RETURNING id;

-- Oracle specific
SELECT * FROM DUAL;
```

✅ **Use parameterized queries** to prevent SQL injection:
```sql
-- Good (parameterized)
PreparedStatement stmt = conn.prepareStatement(
    "SELECT * FROM employees WHERE id = ?"
);
stmt.setInt(1, employeeId);
```

✅ **Use transactions** for data integrity:
```sql
BEGIN TRANSACTION;
    UPDATE accounts SET balance = balance - 100 WHERE id = 1;
    UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```

✅ **Use appropriate indexes** for performance:
```sql
CREATE INDEX idx_employees_department ON employees(department);
```

---

# 🔹 19. Common Mistakes

❌ **Incorrect NULL comparison**:
```sql
-- WRONG
WHERE salary = NULL;

-- CORRECT
WHERE salary IS NULL;
```

❌ **Missing parentheses in complex conditions**:
```sql
-- WRONG (ambiguous)
WHERE department = 'IT' OR department = 'HR' AND salary > 50000;

-- CORRECT (clear intent)
WHERE (department = 'IT' OR department = 'HR') AND salary > 50000;
```

❌ **Using SELECT * in production**:
```sql
-- WRONG (retrieves all columns)
SELECT * FROM employees;

-- CORRECT (specify needed columns)
SELECT id, name, department FROM employees;
```

❌ **Forgetting WHERE clause in UPDATE/DELETE**:
```sql
-- WRONG (updates all rows)
UPDATE employees SET salary = 50000;

-- CORRECT (specify target rows)
UPDATE employees SET salary = 50000 WHERE department = 'IT';
```

❌ **Not using transactions for multi-step operations**:
```sql
-- WRONG (risk of inconsistent data)
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;

-- CORRECT (atomic operation)
BEGIN TRANSACTION;
    UPDATE accounts SET balance = balance - 100 WHERE id = 1;
    UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```

❌ **Using functions on indexed columns in WHERE**:
```sql
-- WRONG (prevents index usage)
WHERE YEAR(hire_date) = 2020;

-- CORRECT (allows index usage)
WHERE hire_date >= '2020-01-01' AND hire_date < '2021-01-01';
```

---

# 📌 Final Summary

* **90% of SQL is the same** across all database systems
* **Key differences** exist in:
  * Row limiting (TOP/LIMIT/ROWNUM)
  * Auto increment (IDENTITY/AUTO_INCREMENT/SERIAL/SEQUENCE)
  * Set operations (EXCEPT/MINUS)
  * Date functions
  * String functions (LEN/LENGTH, SUBSTRING/SUBSTR)
  * Advanced features (CTEs, window functions)

* **Focus on mastering**:
  * WHERE clause filtering
  * JOIN operations
  * GROUP BY aggregations
  * Basic transaction management

* **For cross-database work**:
  * Use ANSI SQL when possible
  * Document database-specific features
  * Test on all target systems

---

# 🚀 Next Step

👉 **Practice with real datasets**:
1. **Filtering** (WHERE clause with various operators)
2. **Joins** (combining data from multiple tables)
3. **Aggregations** (GROUP BY with aggregate functions)
4. **Window functions** (advanced analytics)

👉 **Master these core concepts**:
1. **SELECT-FROM-WHERE** (basic querying)
2. **JOINs** (relating data)
3. **GROUP BY-HAVING** (aggregation)
4. **Subqueries** (nested queries)

👉 **Learn database-specific features** when needed:
1. **SQL Server**: Stored procedures, functions, XML/JSON support
2. **MySQL**: Performance tuning, replication
3. **PostgreSQL**: Advanced data types, extensions
4. **Oracle**: Partitioning, security features

This SQL cheat sheet provides a solid foundation for working with SQL across different database systems. Practice these concepts regularly to become proficient in SQL query writing and database management.