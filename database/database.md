# Database


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

Syntax - 
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

Syntax- 
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

Syntax- 
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

Syntax −
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

Syntax  −

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

Syntax−

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


SQL - Indexes
---------
Indexes are special lookup tables that the database search engine can use to speed up data retrieval. Simply put, an index is a pointer to data in a table. An index in a database is very similar to an index in the back of a book.

For example, if you want to reference all pages in a book that discusses a certain topic, you first refer to the index, which lists all the topics alphabetically and are then referred to one or more specific page numbers.

An index helps to speed up SELECT queries and WHERE clauses, but it slows down data input, with the UPDATE and the INSERT statements. Indexes can be created or dropped with no effect on the data.

Creating an index involves the CREATE INDEX statement, which allows you to name the index, to specify the table and which column or columns to index, and to indicate whether the index is in an ascending or descending order.

Indexes can also be unique, like the UNIQUE constraint, in that the index prevents duplicate entries in the column or combination of columns on which there is an index.

The CREATE INDEX Command
---------

The basic syntax of a CREATE INDEX is as follows.
```sql
CREATE INDEX index_name ON table_name;
```

Single-Column Indexes

A single-column index is created based on only one table column. The basic syntax is as follows.

```sql
CREATE INDEX index_name
ON table_name (column_name);
```

Unique Indexes
---------
Unique indexes are used not only for performance, but also for data integrity. A unique index does not allow any duplicate values to be inserted into the table. The basic syntax is as follows.

```sql
CREATE UNIQUE INDEX index_name
on table_name (column_name);
```

Composite Indexes
---------
A composite index is an index on two or more columns of a table. Its basic syntax is as follows.
```sql
CREATE INDEX index_name
on table_name (column1, column2);
```

Whether to create a single-column index or a composite index, take into consideration the column(s) that you may use very frequently in a query's WHERE clause as filter conditions.

Should there be only one column used, a single-column index should be the choice. Should there be two or more columns that are frequently used in the WHERE clause as filters, the composite index would be the best choice.

Implicit Indexes
---------
Implicit indexes are indexes that are automatically created by the database server when an object is created. Indexes are automatically created for primary key constraints and unique constraints.

The DROP INDEX Command
---------

An index can be dropped using SQL DROP command. Care should be taken when dropping an index because the performance may either slow down or improve.

The basic syntax is as follows −
```sql
DROP INDEX index_name;
```

When should indexes be avoided?
---------

Although indexes are intended to enhance a database's performance, there are times when they should be avoided.

The following guidelines indicate when the use of an index should be reconsidered.

- Indexes should not be used on small tables.
- Tables that have frequent, large batch updates or insert operations.
- Indexes should not be used on columns that contain a high number of NULL values.
- Columns that are frequently manipulated should not be indexed.




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

SQL
-------------
SQL stands for Structured Query Language. SQL is a standard language for storing, manipulating, and retrieving data in relational database systems.

NoSQL
-------------
NoSQL or `non-SQL` is a non-relational database that does not require a fixed schema and is easy to scale.

NoSQL does not necessarily mean that a database does not support SQL. Instead, it means that the database is not an RDBMS.

While traditional RDBMS rely on SQL syntax to store and query data, on the other hand, NoSQL database systems use other technologies and programming languages to store structured, unstructured or semi-structured data.


SQL vs NoSQL
-------------

|Comparing       | SQL	                                |NoSQL   |
|------------------|--------------------------|-------------------------------------------|
|Query Language 	    |  Structured query language (SQL)                 | No declarative query language                |
| Database type      |         Table          |     Key-value, document, wide-column, and graph            |
|  Schema     |    Predefined               |    Dynamic             |
| Data model      |   Relational                |  Non-relational               |
|  Popular database examples     | MySQL, PostgreSQL, Oracle, and MS-SQL                  |  MongoDB, Apache HBase, Amazon DynamoDB, Redis, Couchbase, Cassandra, and Elasticsearch               |
| Ability to scale      |  Vertical                 |   Horizontal              |
| ACID vs BASE      |    ACID               |     BASE            |
|  Advantages     |   Cross-platform support, secure and free                | Easy to use, high performance, and flexible tool                |
|  Disadvantages     |  Complex to maintain and inefficient if processing big data, complex relational database systems are difficult to export into other systems, not good for handling various data types                 | Data is less structured, NoSQL databases are not as reliable (no ACID support), NoSQL databases are newer and may offer less features than their SQL counterparts                |
| Use cases      |  ACID support, complex queries, no changes or growth                 | Real-time data, volumes of data with no structure, agile business, cloud computing                |

Database Types
-------------

Database types depend on the way the data is stored.
 `SQL` has a table-based database. Table database stores data into tables with fixed rows and columns.

`NoSQL` has 4 types of databases:
1. Key-value database – Stores every data element as an attribute name or key together with its value.
2. Document database – Stores data in JSON, BSON, or XML documents.
3. Wide-column database – Stores and groups data into columns instead of rows.
4. Graph database – Optimized to capture and search the connections between data elements.

**Schema**
-------------

A database schema is a structure that defines how a database is constructed. It defines how the data is organized and how the relations among data are associated. There are two types of schemas:

- Predefined
- Dynamic

SQL needs a predefined schema for unstructured data. You need to predefine data structure in the form of tables before you start to use SQL to manipulate data.

However, a NoSQL database does not require a predefined schema. NoSQL uses a dynamic schema for unstructured data. A dynamic schema allows storing data before applying schema. Schema completely depends on how you want to store data.


**Data Model**
-------------

The data model shows the logical structure of the database. It organizes elements of data and standardizes how they relate to each other. There are two types of data models:

- Relational
- Nonrelational

We can observe differences between these data models by looking at the multiple entities. Consider an order from a restaurant as an example and two entities: Order and Delivery Address.

SQL uses a `relational data model`. SQL relational model uses many-to-many relationship. In many-to-many relationship, a single Order row can relate to several Delivery Address rows. Similarly, each Delivery address row can relate to several Order rows.

NoSQL uses a `nonrelational data model` that does not use relationships. NoSQL databases denormalize data by duplicating Delivery address in each Order row that contains that delivery address. Therefore, data is stored multiple times. This enables easy storage and data retrieval and increases the speed of the query.


**Ability to Scale**
-------------
Database scalability is the ability to hold increasing amounts of data without sacrificing performance. There are two types of scalability:

- Vertical
- Horizontal

SQL databases are vertically scalable. In vertical scaling, data resides on a single node, and the only way to scale up is by adding more hardware resources, such as CPU and RAM, to one existing machine. This makes vertical scaling more costly. An additional downside of vertical scaling is that it runs on one machine so if the server goes down, your application will go down too.

NoSQL databases are horizontally scalable. In horizontal scaling, each node contains only part of the data which allows you to add more machines to the existing group of distributed systems. This makes horizontal scaling cheaper and quicker.

**ACID vs BASE**
-------------
SQL databases use the ACID consistency model. ACID stands for:

- Atomic – All operations in a transaction succeed or every operation is rolled back. Partial success is not allowed.
- Consistent – Each transaction moves the database from one valid state to another. Transaction can’t leave the database in an inconsistent state.
- Isolated – Transactions can’t interfere with each other.
- Durable – The results of applying a transaction are permanent, even in the presence of failures.

The main feature of the ACID model is consistency. When you complete a transaction, its data is consistent and stable.

NoSQL databases use the BASE consistency model. BASE stands for:

- Basically Available – All users can perform a query. The database spreads data across several systems so in case that a failure happens to a segment of data, the database will not experience a complete outage.
- Soft State – Database state can change over time.
- Eventual Consistency – If the system is functioning and we wait long enough, the database will eventually become consistent.

The advantage of the BASE consistency model is that transactions are committed faster. Databases that use the BASE model prefer availability over consistency of replicated data.

**Use Cases**
-------------

Not every database fits every business needs. Let’s take a closer look at use cases for both types of databases.

Reasons to use an SQL database:
-------------

- When you need ACID support – With ACID support you get data consistency and 100% data integrity.
- When you are working with complex queries and reports – SQL is a better fit for complex query environments when compared to NoSQL.
- When you don’t anticipate a lot of changes or growth – If your business is not growing exponentially, there is no
  reason to use a system designed to support an increase in data volume.

Reasons to use a NoSQL database:
-------------

- When you need real-time data – NoSQL does not require schemas, so it makes the information process quicker.
- When you store volumes of data with no structure – NoSQL supports all data types.
- When you run an agile business – NoSQL does not require the preparation process, so it reduces downtime.
- When you want to make most out of cloud computing and storage – For a cloud solution to be scalable, the data must be
  easy to share across multiple servers.

## UNION vs UNION ALL

UNION removes duplicate records (where all columns in the results are the same), UNION ALL does not.

There is a performance hit when using UNION instead of UNION ALL, since the database server must do additional work to
remove the duplicate rows, but usually you do not want the duplicates (especially when developing reports).

To identify duplicates, records must be comparable types as well as compatible types. This will depend on the SQL
system. For example the system may truncate all long text fields to make short text fields for comparison (MS Jet), or
may refuse to compare binary fields (ORACLE)

UNION Example:

```sql
SELECT 'foo' AS bar
UNION
SELECT 'foo' AS bar
```

Result:
```log
+-----+
| bar |
+-----+
| foo |
| foo |
+-----+
2 rows in set (0.00 sec)
```

UNION ALL example:

```sql
SELECT 'foo' AS bar
UNION ALL
SELECT 'foo' AS bar
```

Result:
```log
+-----+
| bar |
+-----+
| foo |
| foo |
+-----+
2 rows in set (0.00 sec)
```

Reference: 
https://stackoverflow.com/questions/49925/what-is-the-difference-between-union-and-union-all
https://www.javatpoint.com/mysql-union-vs-union-all


## TRUNCATE vs DELETE, vs  DROP

|TRUNCATE       | DELETE	                                |DROP   |
|------------------|--------------------------|-------------------------------------------|
|  The TRUNCATE TABLE the command deletes the data inside a table, but not the table itself. TRUNCATE deletes all the rows of a table at once. It only logs once in the transaction log.| The DELETE query deletes all records from a table of a database without deleting the table schemas like columns, indexes, etc.  | The DROP TABLE statement is used to drop an existing table in a database. DROP TABLEquery removes the table definition and all data, indexes, triggers, constraints, and permissions for that table.      |
|  TRUNCATE TABLE table_name;| DELETE FROM table_name WHERE condition;|  DROP TABLE table_name;     |



## TRUNCATE
- TRUNCATE is a Data Definition Language(DDL) command.
- TRUNCATE is executed using a table lock and the whole table is locked to remove all records.
- TRUNCATE removes all rows from a table at once.
- WHERE clause cannot be used with TRUNCATE.
- It is faster performance-wise than DELETE as it only logs once in the transaction log.
- TRUNCATE cannot be used with indexed views.
- To use Truncate on a table, ALTER permission is required on the table.

## DELETE
- DELETE is a Data Manipulation Language(DML) command.
- DELETE is executed using a row lock mechanism, each row in the table is locked for deletion.
- WHERE clause can be used with DELETE query to filter out records and then delete them.
- DELETE maintains an entry in the transaction log for each row deleted. Hence it is slower than TRUNCATE.
- DELETE permission is required on the table to delete the records.
- The DELETE can be used with indexed views.


## DROP
- The DROP command removes a table from the database.
- All the tables’ rows, indexes, and privileges will also be removed.
- No Data Manipulation Language(DML) triggers will be fired.
- DROP is a Data Definition Language(DDL).
- DELETE operations can be rolled back (undone), while DROP and TRUNCATE operations cannot be rolled back.


Reference: https://medium.com/javarevisited/know-the-differences-between-truncate-delete-and-drop-4ee70bb736fb



For more information:

- [Cheat sheet](http://files.zeroturnaround.com/pdf/zt_sql_cheat_sheet.pdf)
- [Clustered vs Non-clustered indexes](https://docs.microsoft.com/en-us/sql/relational-databases/indexes/clustered-and-nonclustered-indexes-described)
- [DB Index Wiki](https://en.wikipedia.org/wiki/Database_index)
- [SQL vs NoSQL: What's the Difference?](https://phoenixnap.com/kb/sql-vs-nosql)
- [SQL vs NoSQL: when to use?](https://www.imaginarycloud.com/blog/sql-vs-nosql/)