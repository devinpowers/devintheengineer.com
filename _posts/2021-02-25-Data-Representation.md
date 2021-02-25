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








**Working with JSON files**


**Issues with Data Representation**



