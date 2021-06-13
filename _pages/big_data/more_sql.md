---
permalink: /Big_Data/big_data/more_sql
title: "More on SQL"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"

toc: true
toc_label: "Table of Contents" 

---

Basic things in SQL


Basic **Keywords** in SQL

## SELECT

* The keyword is used to *select* data from a database, the data returned is stored in a result table often called the result-set

* Used with the **FROM** keyword which means *from which table you're refering to*

**Example:**

```sql
SELECT ContactName, CustomerName, City, Country

-- or you can just use the astrick *

-- SELECT *

FROM Customers

```
* You can *select* certain columns from a table or use the astrick **SELECT *** which implies selecting the entire table! The above query Selects the 3 columns from the Customer table.


### SELECT DISTINCT 

* Theres also a Select **Distinct** statement that is used to return only distinct or *different* values

**Example:**

```sql

SELECT DISTINCT Country

FROM Customers

```

* This query will only return *Countrys* will no repeats


## WHERE


### AND, OR, and NOT Operators

* Different clauses that can be combined with the WHERE clause to filter data

* If you combine any of the operators make sure you use *parenthesis*


## ORDER BY

* Keyword is used to *sort* the result-set in either ascending or descending order (ascending order by default)

* To sort by descending order, use **DESC** keyword

Basic Syntax (One Column)

```sql
SELECT *
FROM Table_Name

ORDER BY  Column1 DESC 
```

* This will return a result-set table that is in *descending order* based on Column1


Basic Syntax: (For Several Columns)

```sql
SELECT Column1, Column2, Column3, ...
FROM Table_Name

ORDER BY Column1, Column3, Column2, ... ASC|DESC
```

* This syntax orders by Column1 first, then by Column3, then Column2...

## NULL VALUES

# WAYS TO UPDATE TABLES/DATABASE

## INSERT INTO

## UPDATE

## DELETE
* Delete is used to *delete* existing records in a table

# FUNCTIONS IN SQL

## SQL LIMIT

Want to return just the first 5 records from a table?

* If yes, use the keyword **LIMIT** in (MySQL) after picking the table to return the first 5

**Note:** For Oracle, SQL Server, MS Access and others there are different SQL statements

Basic Syntax:

```sql
SELECT *

FROM Customers

LIMIT 5

```

## COUNT, AVG, and SUM

* We can use basic functions
* Count() will return the number of rows that match a specifed criterion

## MIN and MAX

* The MIN() function will return the smallest value from the selected column
* The MAX() function will return the largest value from the slected column

Very straight forward

Basic Syntax for MIN()

```sql

SELECT MIN(column_name)
FROM table_name
```
Basic Syntax for MAX()

```sql
SELECT MAX(column_name)
FROM table_name
```

### AS 

* Keyword used to change the name in the result-set table

Example using **AS** keyword

```sql
SELECT MIN(Price) AS SmallestPrice
FROM Products
```

* This query will return the smallest value from the *Price* column in the *Products* table and return the result-set table column name as **SmallestPrice**

### LIKE Operator and Wildcards

* Wildcards are *characters* used to substitue one or more characters in a string, they're used with the **LIKE** operator

Here are some common Wildcard Characters (theres different ones for MS Access, SQL Server, MySQL, Oracle, etc)

* ** * **

* **?**

* **[]**

* **-**

* **!**

* **#**



* The LIKE keyword is used in a *WHERE* clause to search for specified pattern (Wildcard) in a column

HELLO WORLD!!✊🏼
