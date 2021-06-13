Database
===============

## SQL

Joins
---------
The SQL Joins clause is used to combine records from two or more tables in a database. A JOIN is a means for combining fields from two tables by using values common to each.

- [Pictorial Reference](https://commons.wikimedia.org/wiki/File:SQL_Joins.svg)
- **Inner join**: Rows common in both T1 and T2
- **Left outer join**: All rows in T1
- **Right outer join**: All rows in T2
- **Full join**: All rows in T1 and T2
- **Cross join**: All rows in T1 * all rows in T2

Inner join
---------
The INNER JOIN creates a new result table by combining column values of two tables (table1 and table2) based upon the join-predicate. The query compares each row of table1 with each row of table2 to find all pairs of rows which satisfy the join-predicate. When the join-predicate is satisfied, column values for each matched pair of rows of A and B are combined into a result row.

Syntax
The basic syntax of the INNER JOIN is as follows.
```sql
SELECT table1.column1, table2.column2...
FROM table1
INNER JOIN table2
ON table1.common_field = table2.common_field;
```

```sql
SQL> SELECT  ID, NAME, AMOUNT, DATE
FROM CUSTOMERS
INNER JOIN ORDERS
ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID;
```



Left outer join
---------
The SQL LEFT JOIN returns all rows from the left table, even if there are no matches in the right table. This means that if the ON clause matches 0 (zero) records in the right table; the join will still return a row in the result, but with NULL in each column from the right table.

This means that a left join returns all the values from the left table, plus matched values from the right table or NULL in case of no matching join predicate.

Syntax
The basic syntax of a LEFT JOIN is as follows.
```sql
SELECT table1.column1, table2.column2...
FROM table1
LEFT JOIN table2
ON table1.common_field = table2.common_field;
```

```sql
SQL> SELECT  ID, NAME, AMOUNT, DATE
FROM CUSTOMERS
LEFT JOIN ORDERS
ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID;
```


Right outer join
---------
The SQL RIGHT JOIN returns all rows from the right table, even if there are no matches in the left table. This means that if the ON clause matches 0 (zero) records in the left table; the join will still return a row in the result, but with NULL in each column from the left table.

This means that a right join returns all the values from the right table, plus matched values from the left table or NULL in case of no matching join predicate.

Syntax
The basic syntax of a RIGHT JOIN is as follow.
```sql
SELECT table1.column1, table2.column2...
FROM table1
RIGHT JOIN table2
ON table1.common_field = table2.common_field;
```

```sql
SQL> SELECT  ID, NAME, AMOUNT, DATE
FROM CUSTOMERS
RIGHT JOIN ORDERS
ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID;
```
Full join
---------
The SQL FULL JOIN combines the results of both left and right outer joins.

The joined table will contain all records from both the tables and fill in NULLs for missing matches on either side.

Syntax
The basic syntax of a FULL JOIN is as follows −
```sql
SELECT table1.column1, table2.column2...
FROM table1
FULL JOIN table2
ON table1.common_field = table2.common_field;
```

```sql
SQL> SELECT  ID, NAME, AMOUNT, DATE
FROM CUSTOMERS
FULL JOIN ORDERS
ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID;
```


If your Database does not support FULL JOIN (MySQL does not support FULL JOIN), then you can use UNION ALL clause to combine these two JOINS as shown below.
```sql
SQL> SELECT  ID, NAME, AMOUNT, DATE
FROM CUSTOMERS
LEFT JOIN ORDERS
ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID
UNION ALL
SELECT  ID, NAME, AMOUNT, DATE
FROM CUSTOMERS
RIGHT JOIN ORDERS
ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID

```

Cross join
---------
The CARTESIAN JOIN or CROSS JOIN returns the Cartesian product of the sets of records from two or more joined tables. Thus, it equates to an inner join where the join-condition always evaluates to either True or where the join-condition is absent from the statement.

Syntax
The basic syntax of the CARTESIAN JOIN or the CROSS JOIN is as follows −
```sql
SELECT table1.column1, table2.column2...
FROM  table1, table2 [, table3 ]
```

```sql
SQL> SELECT  ID, NAME, AMOUNT, DATE
FROM CUSTOMERS, ORDERS;
```

Self Join
---------
The SQL SELF JOIN is used to join a table to itself as if the table were two tables; temporarily renaming at least one table in the SQL statement.

Syntax
The basic syntax of SELF JOIN is as follows −
```sql
SELECT a.column_name, b.column_name...
FROM table1 a, table1 b
WHERE a.common_field = b.common_field;
```

```sql
SQL> SELECT  a.ID, b.NAME, a.SALARY
FROM CUSTOMERS a, CUSTOMERS b
WHERE a.SALARY < b.SALARY;
```

Keys
---------

- **Primary key**: Uniquely identify the row. Cannot be null.
- **Candidate key**: Can be chosen as primary key
- **Composite key**: Combination of multiple columns
- **Foreign key**: Column referencing other table's primary key

Indexes
---------

- Improves speed of data retrieval.
- Primary and foreign keys are indexed by default.
- **Non-clustered index**: Rows are unordered (stored in heap). While index is stored separately as sorted column.
- **Clustered index**: The rows themselves are ordered (thus there can be only 1 clustered index per table).
- **Composite index**: Index on multiple columns (c1,c2,c3). Order of columns should match the where clauses for maximum efficiency.
- **Cardinality**: Uniqueness of rows (eg: PassportID vs Gender column values).
- **Bitmap-index**: Used when cardinality is very low (eg: Gender column).
- **Data structures used**: Bit arrays, hashmaps or B+Trees (most common).

Queries
---------

- **Union**: Merges content of 2 structurally compatible tables
- **Group By**: Used to aggregate (avg, sum, count) values. Aggregate column should be same as group-by column.
- **Having**: Adding where clauses on top of group-by.

Frequently asked queries
---------

- Find all departments with sales more than 1000

```sql
SELECT department, SUM(sales) AS "Total sales"
FROM order_details	
GROUP BY department
HAVING SUM(sales) > 1000;
```

- Print all employee ids with their manager ids

```sql
SELECT e1.emp_id, e1.emp_mgr_id 
FROM employee e1 LEFT JOIN employee e2 
   ON e1.emp_mgr_id = e2.emp_id
```

- Print all manager names with count of directs

```sql
SELECT e2.ename, count(e1.ename) 
FROM employee_s e1 LEFT OUTER JOIN employee_s e2 
  ON e1.manager_id = e2.eid 
group by e2.ename;
```

- Print 10th highest salary

```sql
SELECT Salary FROM
(  SELECT DISTINCT Salary FROM Employee ORDER BY Salary DESC LIMIT 10 ) 
AS Emp ORDER BY Salary LIMIT 1;
```

For more information:

- [Cheat sheet](http://files.zeroturnaround.com/pdf/zt_sql_cheat_sheet.pdf)
- [Clustered vs Non-clustered indexes](https://docs.microsoft.com/en-us/sql/relational-databases/indexes/clustered-and-nonclustered-indexes-described)
- [DB Index Wiki](https://en.wikipedia.org/wiki/Database_index)