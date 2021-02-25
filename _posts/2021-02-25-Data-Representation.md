---
title: 'Big Data Analysis Day 2: Representation '

date: 2021-2-25

---

In this lesson Section, I will talk about Data and reading different kinds of file (csv and json)


**What is Data?**

Data is a collection of objects and their attributes, with object being a 'data point' and an attribute being a property or characteristic  of a data object


**What Types of Data Exists?**

* Record-Based Data

    - Collection of unordered tuples, where is 

* Ordered Data

    - Collection

* Graph-Based Data:

    - Data is a collection of linked objects and attributes
    - Check out my Graphs in my Data Structures and Algorithms Page!!!!


**How do we Represent Data?**

- Structured Data in relational databases -> SQL
- Unstructured Data
- Flat files (CSV)
- Complex (JSON, XML, etc)


**How do we load data?**

- Parse a file using regular expressions is an important skill to learn/develop


**Working with CSV Files**


- using import csv, numpy, and pandas library

This covid.csv file can be found:

[Covid Vacine file](url here)

```python
with open('covid.csv','r') as f:
    column_names = f.readline().strip().split(',')  # stripping first column headers of commas
    data = [] 
    for line in f:
        data.append(line.strip().split(','))       #iterating through each row and stipping commas
```

Lets check out the Column Names

```python
column_names
```

Output:

```
['\ufeffSex',
 'Age',
 'Vaccine Type',
 'Facility Type',
 'Number of Doses',
 'Week',
 'Month',
 'Year',
 'Data as of']
```

How about the data

```python
data
```
Output:

```python
[['F',
  '20-29 years',
  'Moderna',
  'Public Health Provider',
  '1',
  '52',
  'December',
  '2020',
  '23-Dec-20'],
  ....
```


Ok awesome, now lets use the Pandas Library to help look at the data in a more organized way!

For CSV Files:

```python
data = read_csv(file_name, header, names)
```
Which:
* file_name: name of the file .csv
* header: Column that contains the "attributes", which is usually column 0
* names: Which is the attribute names (just in case if the csv file doesnt contain them!!)

```python
import pandas as p
data = p.read_csv('covid.csv',header=0)

# can use read_table as well -> p.read_table('covid.csv', sep = ',', header = 'infer ')
```
Now lets check out the data with in Pandas is stored in a **DataFrame Object**


```python
data
```

Output:
```python
	Sex	Age	Vaccine Type	Facility Type	Number of Doses	Week	Month	Year	Data as of
0	F	20-29 years	Moderna	Public Health Provider	1	52	December	2020	23-Dec-20
1	F	20-29 years	Moderna	Public Health Provider	1	53	December	2020	28-Dec-20
2	F	20-29 years	Pfizer	Hospital	1	51	December	2020	19-Dec-20
3	F	20-29 years	Pfizer	Public Health Provider	1	53	December	2020	29-Dec-20
4	F	30-39 years	Moderna	Public Health Provider	2	52	December	2020	23-Dec-20
...	...	...	...	...	...	...	...	...	...
10861	M	60-69 years	Pfizer	Hospital	1	52	December	2020	20-Dec-20
10862	M	60-69 years	Pfizer	Hospital	1	52	December	2020	21-Dec-20
10863	M	60-69 years	Pfizer	Hospital	1	52	December	2020	23-Dec-20
10864	M	60-69 years	Pfizer	Hospital	1	52	December	2020	26-Dec-20
10865	M	70-79 years	Pfizer	Hospital	1	51	December	2020	19-Dec-20
```

This looks way **cleaner** and easier to manage!










**Working with JSON files**


**Issues with Data Representation**



