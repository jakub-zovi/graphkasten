---
tags:
  - cs
  - cs/databases
created: 2024-10-29T21:14
modified: 2025-08-09T11:27
published:
sources:
topics:
  - SQL
  - Relational Databases
  - Query Language
  - DDL and DML
  - Joins
authors:
ai-assisted:
hidden:
public: true
---
# SQL
[Wikipedia:](https://en.wikipedia.org/wiki/SQL)
> Structured Query Language (SQL)  is a domain-specific language used to manage data, especially in a relational database management system (RDBMS). It is particularly useful in handling structured data, i.e., data incorporating relations among entities and variables.

**TODO:** structure below reference into sub notes.

# SQL Quick Reference Guide
Source: ChatGPT[^1]

## 1. Data Definition Language (DDL)
### Create Table
```sql
CREATE TABLE table_name (
    column1 datatype constraint,
    column2 datatype constraint,
    ...
);
```

### Alter Table
```sql
ALTER TABLE table_name
ADD column_name datatype;

ALTER TABLE table_name
DROP COLUMN column_name;

ALTER TABLE table_name
MODIFY column_name datatype;
```

### Drop Table
```sql
DROP TABLE table_name;
```

### Truncate Table
```sql
TRUNCATE TABLE table_name;
```

---

## 2. Data Manipulation Language (DML)
### Insert Data
```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```

### Update Data
```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

### Delete Data
```sql
DELETE FROM table_name
WHERE condition;
```

---

## 3. Data Query Language (DQL)
### Select Data
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition
GROUP BY column
HAVING condition
ORDER BY column ASC|DESC
LIMIT number;
```

---

## 4. Data Control Language (DCL)
### Grant Permissions
```sql
GRANT privilege ON object TO user;
```

### Revoke Permissions
```sql
REVOKE privilege ON object FROM user;
```

---

## 5. Transaction Control Language (TCL)
### Commit
```sql
COMMIT;
```

### Rollback
```sql
ROLLBACK;
```

### Savepoint
```sql
SAVEPOINT savepoint_name;
ROLLBACK TO savepoint_name;
```

---

## 6. Common SQL Clauses
### Where Clause
```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```

### Like Clause
```sql
SELECT column1, column2
FROM table_name
WHERE column_name LIKE pattern;
```

### Between Clause
```sql
SELECT column1, column2
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```

### In Clause
```sql
SELECT column1, column2
FROM table_name
WHERE column_name IN (value1, value2, ...);
```

---

## 7. Aggregate Functions
### Count
```sql
SELECT COUNT(column_name) FROM table_name;
```

### Sum
```sql
SELECT SUM(column_name) FROM table_name;
```

### Avg
```sql
SELECT AVG(column_name) FROM table_name;
```

### Min
```sql
SELECT MIN(column_name) FROM table_name;
```

### Max
```sql
SELECT MAX(column_name) FROM table_name;
```

---

## 8. Joins
### Inner Join
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### Left Join
```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```

### Right Join
```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```

### Full Outer Join
```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

---

## 9. Subqueries
### Inline Subquery
```sql
SELECT column1, column2
FROM table_name
WHERE column_name = (SELECT column_name FROM table_name WHERE condition);
```

### Correlated Subquery
```sql
SELECT column1
FROM table1
WHERE column1 = (SELECT column2 FROM table2 WHERE table1.column3 = table2.column3);
```

---

## 10. Indexes
### Create Index
```sql
CREATE INDEX index_name ON table_name (column1, column2, ...);
```

### Drop Index
```sql
DROP INDEX index_name;
```

---

## 11. Views
### Create View
```sql
CREATE VIEW view_name AS
SELECT columns
FROM table_name
WHERE condition;
```

### Drop View
```sql
DROP VIEW view_name;
```

---

## 12. Constraints
### Add Constraint
```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name constraint_type (column_name);
```

### Drop Constraint
```sql
ALTER TABLE table_name
DROP CONSTRAINT constraint_name;
```

---

### Notes
- Replace `table_name`, `column_name`, and other placeholders with actual table and column names.
- Use semicolons (`;`) to terminate SQL statements.

[^1]: Hello, provide me a quick reference page for the common SQL commands. Structure the page into a markdown.