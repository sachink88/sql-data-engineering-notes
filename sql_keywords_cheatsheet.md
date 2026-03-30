
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

