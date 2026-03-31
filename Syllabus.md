# 🎓 SQL Mastery Syllabus & Navigation  
## A Roadmap from Data Basics to Architectural Excellence  

This document provides a granular breakdown of every topic covered in this repository. Each section is designed to build upon the last, ensuring a smooth transition from basic queries to advanced performance tuning.

---

## 🟢 Phase 1: Basic (The Bedrock)  
**Focus:** Building the mental model of how databases store and protect data.

### 🛠 sql_foundation.md
- **What is SQL?**
- **Understanding the 5 Sub-languages:**
  - **DDL**: Data Definition (Structures)
  - **DML**: Data Manipulation (Rows)
  - **DQL**: Data Query (Search)
  - **DCL**: Data Control (Security)
  - **TCL**: Transaction Control (Safety)
- **RDBMS vs NoSQL**
  - Structured tables vs flexible documents
- **The Big 5 Providers**
  - Oracle  
  - SQL Server  
  - DB2  
  - PostgreSQL  
  - MySQL  

---

### 🔢 sql_datatypes.md
- **Storage Efficiency**
  - INT vs BIGINT  
  - FLOAT vs DECIMAL  
- **Character Handling**
  - CHAR vs VARCHAR vs TEXT  
- **The Date Trap**
  - DATETIME vs TIMESTAMP  
  - Timezones across dialects  

---

### 🔒 sql_constraints.md
- **Data Integrity**
- **Key Constraints**
  - PRIMARY KEY  
  - FOREIGN KEY  
  - UNIQUE  
  - CHECK  
- **Defaults**
  - DEFAULT values  
  - NOT NULL  

---

### 🔍 sql_operators.md
- **Logical Filtering**
  - AND, OR, NOT, IN  
- **Range & Patterns**
  - BETWEEN  
  - LIKE (`%`, `_`)  

---

## 🟡 Phase 2: Intermediate (The Data Wrangler)  
**Focus:** Learning to manipulate multi-table datasets and perform complex transformations.

### 🔗 sql_joins.md
- **Visual Logic**
  - INNER JOIN  
  - LEFT JOIN  
  - RIGHT JOIN  
  - FULL JOIN  
  - CROSS JOIN  
- **Advanced Patterns**
  - SELF JOIN (e.g., Org Charts)

---

### 📑 sql_subqueries.md
- **Nested Logic**
  - Scalar subqueries  
  - Row subqueries  
  - Table-valued subqueries  
- **CTEs**
  - Using `WITH` clauses for readability  

---

### 🧪 sql_functions.md
- **Null Handling**
  - COALESCE  
  - NULLIF  
  - ISNULL  
- **Conditional Logic**
  - CASE WHEN  
- **String/Date Formatting**
  - Cross-database equivalents  

---

## 🔴 Phase 3: Advanced (The Performance Pro)  
**Focus:** Skills required for Senior Data Engineers and Database Architects.

### 📈 window_functions.md
- **Analytical Power**
  - `OVER (PARTITION BY ... ORDER BY ...)`  
- **Ranking**
  - ROW_NUMBER  
  - RANK  
  - DENSE_RANK  
- **Navigation**
  - LEAD  
  - LAG  

---

### ⚡ sql_optimization.md
- **Explain Plan**
  - Understanding query execution  
- **Indexing Theory**
  - B-Tree  
  - Hash  
  - Clustered  
  - Non-Clustered  
- **SARGability**
  - Writing index-friendly queries  

---

### 🏛️ sql_database_systems.md
- **Architecture**
  - Buffer Pools  
  - WAL (Write Ahead Logging)  
  - Storage Engines (InnoDB vs MyISAM)  

---

## 🛠️ Cross-Database Quick Reference

| Feature       | MySQL            | PostgreSQL      | SQL Server | Oracle            | DB2               |
|--------------|------------------|-----------------|------------|-------------------|-------------------|
| Pagination   | LIMIT 10         | LIMIT 10        | TOP 10     | FETCH FIRST 10    | FETCH FIRST 10    |
| Concat       | CONCAT(a, b)     | a \|\| b        | a + b      | a \|\| b          | a \|\| b          |
| Cur. Date    | NOW()            | CURRENT_DATE    | GETDATE()  | SYSDATE           | CURRENT DATE      |
| Auto-Inc     | AUTO_INCREMENT   | SERIAL          | IDENTITY   | SEQUENCE          | IDENTITY          |

---

## 🎯 Projects & Practice  

Found in the `/projects` and `/practice` folders:

- **Retail Analytics**
  - End-to-end sales performance tracking  
- **HR Management**
  - Recursive employee hierarchy handling  
- **Financial Auditing**
  - Identifying transaction anomalies  

---

## 🚀 Learning Outcome

By completing this roadmap, you will:
- Master SQL from fundamentals to advanced topics  
- Understand database internals and performance tuning  
- Be ready for Data Engineering and Database Architect roles  

---
