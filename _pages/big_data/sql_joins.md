---
permalink: /Big_Data/big_data/sql_joins
title: "JOINS in SQL"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"

---


### INNER JOIN 


- A **JOIN** clause is used to *combine rows* from two or more tables, based on a related column between them.



**INNER JOIN Syntax**

Called INNER JOIN or just JOIN

The INNER JOIN keyword selects records that have matching values in *both tables*.

Syntax of a INNER JOIN:

```sql
SELECT Column_Name(s)
FROM Table_1
INNER JOIN Table_2 -- or just JOIN
ON Table_1.Column_Name = Table_2.Column_Name  -- What they have in common
```


Example of an INNER JOIN:

```sql
SELECT employee.emp_id, employee.first_name, branch.branch_name
FROM employee
INNER JOIN branch    -- or just use the keyword JOIN
ON employee.emp_id = branch.mgr_id
```





### LEFT JOIN

The **LEFT JOIN** will grab everything from the left table and any missing values will be **NULL**

Example of an LEFT JOIN:

```sql
SELECT employee.emp_id, employee.first_name, branch.branch_name
FROM employee
LEFT JOIN branch    
ON employee.emp_id = branch.mgr_id
```


### RIGHT JOIN


The **RIGHT JOIN** will grab everything from the right table and any missing values will be **NULL**

Example of an RIGHT JOIN:

```sql
SELECT employee.emp_id, employee.first_name, branch.branch_name
FROM employee
RIGHT JOIN branch    
ON employee.emp_id = branch.mgr_id
```

### FULL JOIN

* **FULL or (OUTER) JOIN** returns unmatched rows from both tables.

**NOTE:** A Full join *isnt* supported in MySQL or SQLite which I've used the most


![inserting an Image](/images/big_data/SQL/sql_joins.jpg)
