---
title: 'Big Data Analysis Day 2: Representation '

date: 2021-2-25

---

In this lesson Section, I will talk about Data and reading different kinds of file (csv and json)


**What is Data?**

Data is a collection of objects and their attributes, with object being a 'data point' and an attribute being a property or characteristic  of a data object


**What Types of Data Exists?**

* Record-Based Data

    - Collection of unordered tuples, where each tupe represents an object and contains a set of field (attributes) that characterize properties of the object
    - Examples:  Census data, web server logs, document data, transaction data

* Ordered Data

    - Collection of ordered tuples
    - Examples: sequence and time series data

* Graph-Based Data:

    - Data is a collection of linked objects and attributes in which consits of G = (V, E), where G = Graph, V = vertices (a set of nodes), and E = edges (a set of links )
    - Check out my Graphs in my Data Structures and Algorithms Page!!!!
    -[Graph data Structure Page](https://devintheengineer.com/algorithms/intro_graph)
    - Examples: Web Traversal Pattern


**How do we Represent Data?**

- Structured Data in relational databases -> SQL
- Unstructured Data
- Flat files (CSV)
- Complex (JSON, XML, KML, etc)


**How do we load data?**

Note: **Parse a file using regular expressions** is an important skill to learn/develop


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
* names: Which is the **attribute names** (just in case if the csv file doesnt contain them!!)

```python
import pandas as p
data = p.read_csv('covid.csv',header=0)
```

We can also load data this way:

```python
p.read_table(file_name, sep, header = 'infer ', names)
```
Where:

* file_name : name of csv we want to open
* sep : separator/delimiter between the columns (',' in csv files)
* header : Column that contains the attribute name (or None)
* names: Attribute names (if not given in the CSV file)


Now lets check out the data with in Pandas is stored in a **DataFrame Object** lets work with it!


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


Lets Look at the First 5 Rows

```python
data[:5]
```

Output:
```python
	Sex	Age	Vaccine Type	Facility Type	Number of Doses	Week	Month	Year	Data as of
0	F	20-29 years	Moderna	Public Health Provider	1	52	December	2020	23-Dec-20
1	F	20-29 years	Moderna	Public Health Provider	1	53	December	2020	28-Dec-20
2	F	20-29 years	Pfizer	Hospital	            1	51	December	2020	19-Dec-20
3	F	20-29 years	Pfizer	Public Health Provider	1	53	December	2020	29-Dec-20
4	F	30-39 years	Moderna	Public Health Provider	2	52	December	2020	23-Dec-20

```


Working with the dataframe

```python

data[:5][['Sex','Age', 'Vaccine Type']]
```
Output:
```python
	Sex	Age	Vaccine Type
0	F	20-29 years	Moderna
1	F	20-29 years	Moderna
2	F	20-29 years	Pfizer
3	F	20-29 years	Pfizer
4	F	30-39 years	Moderna
```

other things.

```python
data.columns.values
```
Output:

```python
array(['Sex', 'Age', 'Vaccine Type', 'Facility Type', 'Number of Doses',
       'Week', 'Month', 'Year', 'Data as of'], dtype=object)
```

Lets check out the dimensions of the DataFrame (tuple: (rows, columns))

```python
data.shape
```
Output:
```python
(10866, 9)
```

Lets check out the Number of each vaccine has been admitted:

```python
vaccine_counts = data['Vaccine Type'].value_counts()
```

```python
vaccine_counts
```
Output:

```python
Pfizer     8137
Moderna    2729
Name: Vaccine Type, dtype: int64
```

Awesome, not lets import matplotlib library and start plotting !!

```python
%matplotlib inline
import matplotlib
```
```python
vaccine_counts.plot( kind = 'bar', rot= 0)
```

Output:

![inserting an Image](/images/big_data/covid_vaccines.jpg)



**Working with JSON files**

- JSON files are Javascript Object Notation and thier properties are encoded as **key-value** pairs that are seperated by (:)

How would you work with a JSON file using Python?

```python
import json

f =  open('example.json',)

data = json.load(f) 
```

```python
for i in data['users']:
    print(i)
```

Output:

```python
{'userId': 1, 'firstName': 'Krish', 'lastName': 'Lee', 'phoneNumber': '123456', 'emailAddress': 'krish.lee@learningcontainer.com'}
{'userId': 2, 'firstName': 'racks', 'lastName': 'jacson', 'phoneNumber': '123456', 'emailAddress': 'racks.jacson@learningcontainer.com'}
{'userId': 3, 'firstName': 'denial', 'lastName': 'roast', 'phoneNumber': '33333333', 'emailAddress': 'denial.roast@learningcontainer.com'}
{'userId': 4, 'firstName': 'devid', 'lastName': 'neo', 'phoneNumber': '222222222', 'emailAddress': 'devid.neo@learningcontainer.com'}
{'userId': 5, 'firstName': 'jone', 'lastName': 'mac', 'phoneNumber': '111111111', 'emailAddress': 'jone.mac@learningcontainer.com'}
```

closing the file stream for JSON:

```python
f.close()
```
**Other ways that we commonly Represent Data**

- Matrix (matrices)
    * numpy library in Python is good for dealing with matrices


**Issues with Data Representation**

- How to handle "missing values" in the data

    * Can use values like NULL or N/A when values are missing

### Types of Attributes

* Atrribute type depends on the properties of its values



Next -> Data Collection


