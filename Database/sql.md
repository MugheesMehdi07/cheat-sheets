
# SQL Cheat Sheet

This cheat sheet provides a concise overview of essential SQL commands and their usage, which is crucial for interacting with relational databases.

## Basic SQL Syntax

### SELECT Statement

- **Select all columns from a table:**
  ```sql
  SELECT * FROM table_name;
  ```

- **Select specific columns from a table:**
  ```sql
  SELECT column1, column2 FROM table_name;
  ```

- **Select with condition:**
  ```sql
  SELECT * FROM table_name WHERE condition;
  ```

### INSERT Statement

- **Insert data into a table:**
  ```sql
  INSERT INTO table_name (column1, column2) VALUES (value1, value2);
  ```

### UPDATE Statement

- **Update data in a table:**
  ```sql
  UPDATE table_name SET column1 = value1 WHERE condition;
  ```

### DELETE Statement

- **Delete data from a table:**
  ```sql
  DELETE FROM table_name WHERE condition;
  ```

## Filtering, Sorting, and Grouping

### WHERE Clause

- **Filter records:**
  ```sql
  SELECT * FROM table_name WHERE condition;
  ```

### ORDER BY Clause

- **Sort results:**
  ```sql
  SELECT * FROM table_name ORDER BY column ASC|DESC;
  ```

### GROUP BY Clause

- **Group rows that have the same values in specified columns:**
  ```sql
  SELECT column, COUNT(*) FROM table_name GROUP BY column;
  ```

### HAVING Clause

- **Filter groups:**
  ```sql
  SELECT column, COUNT(*) FROM table_name GROUP BY column HAVING condition;
  ```

## Join Operations

- **INNER JOIN:**
  ```sql
  SELECT columns FROM table1
  INNER JOIN table2 ON table1.column = table2.column;
  ```

- **LEFT JOIN:**
  ```sql
  SELECT columns FROM table1
  LEFT JOIN table2 ON table1.column = table2.column;
  ```

- **RIGHT JOIN:**
  ```sql
  SELECT columns FROM table1
  RIGHT JOIN table2 ON table1.column = table2.column;
  ```

- **FULL OUTER JOIN:**
  ```sql
  SELECT columns FROM table1
  FULL OUTER JOIN table2 ON table1.column = table2.column;
  ```

## Advanced SQL Operations

### Subqueries

- **Using a subquery in WHERE clause:**
  ```sql
  SELECT * FROM table1 WHERE column IN (SELECT column FROM table2);
  ```

### UNION

- **Combine the results of two queries:**
  ```sql
  SELECT column FROM table1
  UNION
  SELECT column FROM table2;
  ```

### Functions

- **Common functions:**
  ```sql
  SELECT COUNT(*), MAX(column), MIN(column), AVG(column) FROM table_name;
  ```

## Transaction Control

- **Start a transaction:**
  ```sql
  START TRANSACTION;
  ```

- **Commit a transaction:**
  ```sql
  COMMIT;
  ```

- **Rollback a transaction:**
  ```sql
  ROLLBACK;
  ```

## Database Management

### Create a Table

- **Create a new table:**
  ```sql
  CREATE TABLE table_name (
    column1 datatype CONSTRAINT,
    column2 datatype,
    column3 datatype
  );
  ```

### Alter a Table

- **Add a column:**
  ```sql
  ALTER TABLE table_name ADD column_name datatype;
  ```

- **Drop a column:**
  ```sql
  ALTER TABLE table_name DROP COLUMN column_name;
  ```

### Drop a Table

- **Remove a table:**
  ```sql
  DROP TABLE table_name;
  ```

## Resources

- [SQL Tutorial on W3Schools](https://www.w3schools.com/sql/)
- [SQL Documentation on PostgreSQL](https://www.postgresql.org/docs/)


