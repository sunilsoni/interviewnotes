#Queries


# Find Nth highest salary in SQL - Oracle, MSSQL and MySQL



# Nth maximum salary in MySQL using LIMIT keyword

MySQL  supports a LIMIT keyword, which provides pagination capability. You can find the nth highest salary in MySQL without using subquery as shown below:

The benefit of this approach is that it's faster than a correlated query approach but its vendor dependent. This solution will only work in a MySQL database
```sql
SELECT salary FROM Employee ORDER BY salary DESC LIMIT N-1, 1

```

## 2nd highest salary in MySQL without subquery:


```sql
SELECT salary FROM Employee ORDER BY salary DESC LIMIT 1,1

```

## 3rd highest salary in MySQL using LIMIT clause:

```sql
SELECT salary FROM Employee ORDER BY salary DESC LIMIT 2,1

```




```sql

```

```sql

```

```sql

```

```sql

```






