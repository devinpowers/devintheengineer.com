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


## Exercise 1


Lets work on another CSV with Pandas!

Lets use Baltimore Crime Dataset that can be easily download from here:

[Baltimore Crime Dataset](https://data.world/baltimore/baltimore-crime-data)


Lets use pandas to read/load the file into a data frame object 
```python
import pandas as pd

data = pd.read_csv('Baltimore_crime_data.csv')

```

Lets display the first 10 rows of the data frame
```
data.head(10)
```

Output:

```python
	CrimeDate	CrimeTime	CrimeCode	Location	             Description	Inside/Outside	Weapon	   Post	District	Neighborhood	             Longitude	  Latitude      	Location 1	           Premise	Total Incidents
0	11/04/2017	23:39:00	4E	5700 HAZELWOOD CIR	            COMMON ASSAULT	I	            HANDS	    444.0	NORTHEASTERN	Frankford	            -76.53114	39.33952	(39.3395200000, -76.5311400000)	APT/CONDO	1
1	11/04/2017	23:16:00	4E	200 N MOUNT ST	                COMMON ASSAULT	I	            HANDS	    711.0	WESTERN	Franklin Square	                -76.64393	39.29141	(39.2914100000, -76.6439300000)	APT/CONDO	1
2	11/04/2017	23:15:00	6C	1100 E NORTH AVE	            LARCENY     	I	            NaN	        342.0	EASTERN	East Baltimore Midway	        -76.60333	39.31177	(39.3117700000, -76.6033300000)	GROCERY/CO	1
3	11/04/2017	23:15:00	7A	4800 ERDMAN AVE	                AUTO THEFT  	O	            NaN	        433.0	NORTHEASTERN	Armistead Gardens	    -76.55972	39.30727	(39.3072700000, -76.5597200000)	STREET	    1
4	11/04/2017	23:00:00	4E	6400 ELRAY DR	                COMMON ASSAULT	                NaN	HANDS	632.0	NORTHWESTERN	Cheswolde	            -76.69162	39.36942	(39.3694200000, -76.6916200000)	NaN	        1
5	11/04/2017	22:20:00	3K	2800 SPELMAN RD	                ROBBERY - RESIDENCE	I	        NaN	        922.0	SOUTHERN	Cherry Hill	                -76.62859	39.24659	(39.2465900000, -76.6285900000)	ROW/TOWNHO	1
6	11/04/2017	21:30:00	4E	1500 HAZEL ST	                COMMON ASSAULT	I	            HANDS	    911.0	SOUTHERN	Curtis Bay          	    -76.58975	39.22601	(39.2260100000, -76.5897500000)	ROW/TOWNHO	1
7	11/04/2017	21:20:00	3B	4400 PARK HEIGHTS AVE	        ROBBERY - STREET	            NaN	NaN	    614.0	NORTHWESTERN	Central Park Heights    -76.66676	39.34000	(39.3400000000, -76.6667600000)	NaN	        1
8	11/04/2017	20:39:00	4C	HEIGHTS AV & W COLD SPRING LN	AGG. ASSAULT	                NaN	OTHER	614.0	NORTHWESTERN	Central Park Heights    -76.66645	39.33963	(39.3396300000, -76.6664500000)	NaN     	1
9	11/04/2017	20:32:00	4B	2700 E MONUMENT ST	            AGG. ASSAULT		            KNIFE	    323.0	EASTERN	Madison-Eastend	                -76.57941	39.29899	(39.2989900000, -76.5794100000)	STREET	    1
```

Now lets organize the Dataframes a bit


```python
from pandas import DataFrame
```

Lets create a DataFrame of only Auto Thefts 

```python
auto_theft = data[data["Description"]=="AUTO THEFT"]
```


```python
auto_theft[:5]
```

Output:

```python
CrimeDate	CrimeTime	CrimeCode	Location	Description	Inside/Outside	Weapon	Post	District	Neighborhood	Longitude	Latitude	Location 1	Premise	Total Incidents
3	11/04/2017	23:15:00	7A	4800 ERDMAN AVE	AUTO THEFT	O	NaN	433.0	NORTHEASTERN	Armistead Gardens	-76.55972	39.30727	(39.3072700000, -76.5597200000)	STREET	1
13	11/04/2017	19:35:00	7A	NORTH AV & EUTAW PL	AUTO THEFT	O	NaN	132.0	CENTRAL	Bolton Hill	-76.63404	39.31047	(39.3104700000, -76.6340400000)	GAS STATIO	1
40	11/04/2017	12:30:00	7A	3800 SHANNON DR	AUTO THEFT	O	NaN	432.0	NORTHEASTERN	Belair-Edison	-76.55854	39.32009	(39.3200900000, -76.5585400000)	STREET	1
105	11/03/2017	17:30:00	7A	3200 ELMLEY AVE	AUTO THEFT	NaN	NaN	434.0	NORTHEASTERN	Belair-Edison	-76.57787	39.31706	(39.3170600000, -76.5778700000)	NaN	1
115	11/03/2017	15:42:00	7A	2400 PELHAM AVE	AUTO THEFT	NaN	NaN	431.0	NORTHEASTERN	Mayfield	-76.57737	39.32894	(39.3289400000, -76.5773700000)	NaN	1

```

Lets create a DataFrame of Auto Thefts from each District

```python
auto_counts = DataFrame(auto_theft["District"])
```

```python
auto_counts[:5]
```

Output:
```python

District
3	NORTHEASTERN
13	CENTRAL
40	NORTHEASTERN
105	NORTHEASTERN
115	NORTHEASTERN
```

Awesome, now lets sum up and order them by alphabetically

```python

auto_counts = DataFrame(auto_theft["District"].value_counts().sort_index())

```

```python
auto_counts
```

Output:

```python
	        District
CENTRAL	        1797
EASTERN	        1914
NORTHEASTERN	5155
NORTHERN	    2826
NORTHWESTERN	3635
SOUTHEASTERN	2737
SOUTHERN	    3140
SOUTHWESTERN	3476
WESTERN	        2912

```

Now Lets Create DataFrames for all the Types of Crimes

```python

auto_theft = data[data["Description"]=="AUTO THEFT"]
auto_counts = DataFrame(auto_theft["District"].value_counts().sort_index())


assault = data[data["Description"]=="COMMON ASSAULT"]
assault_counts = DataFrame(assault["District"].value_counts().sort_index())

robbery = data[data["Description"]=="ROBBERY - STREET"]
robbery_counts = DataFrame(robbery["District"].value_counts().sort_index())

homicide = data[data["Description"]=="HOMICIDE"]
homicide_counts = DataFrame(homicide["District"].value_counts().sort_index())

counts = pd.concat([auto_counts,assault_counts,robbery_counts,homicide_counts], axis=1) ## combine
counts.columns = ['Auto Theft', 'Assault', 'Robbery', 'Homicide'] ## Give new Dataframe column names

```

```python
counts
```

```python
	             Auto Theft	Assault	Robbery	Homicide
CENTRAL     	1797	5387	    2696	112
EASTERN	        1914	5303    	1408	242
NORTHEASTERN	5155	7077	    2881	217
NORTHERN	    2826	4229	    2154	119
NORTHWESTERN	3635	4234	    1809	223
SOUTHEASTERN	2737	6376	    3002	99
SOUTHERN	    3140	5388	    1916	136
SOUTHWESTERN	3476	4483	    1373	212
WESTERN	        2912	4520	    1227	264

```

```python
counts = DataFrame(data["Description"].value_counts())
```

```python
counts
````

Output:

```python
                    Description
LARCENY	                62531
COMMON ASSAULT	        47018
BURGLARY	            44048
LARCENY FROM AUTO	    37309
AGG. ASSAULT	        28550
AUTO THEFT	            27597
ROBBERY - STREET	    18469
ROBBERY - COMMERCIAL	4331
ASSAULT BY THREAT	    3609
SHOOTING	            3055
ROBBERY - RESIDENCE	    2965
RAPE	                1721
HOMICIDE	            1624
ROBBERY - CARJACKING	1623
ARSON	                1510
```

```python
import matplotlib
%matplotlib inline

counts.plot(kind='bar') 

```

Output:

![Insert](/images/big_data/Baltimore_crime.png)


Lets look at some other things to possibly Graph/Plot

Maybe Latitude and Longitude??

```python
long = data["Longitude"]
lat = data["Latitude"]
```

Lets plot!

```python
fig, ax = plot.subplots(figsize=(20, 12))
ax.scatter(x = long, y = lat)
plot.xlabel("Longitude")
plot.ylabel("Latitude")
```

Output:
![Insert](/images/big_data/balt_lat.png)

What does that graph above look like?

![Insert](/images/big_data/Baltimore_map.png)

