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



