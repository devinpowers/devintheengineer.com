---
title: '100 Days of Machine Learning '

date: 2021-2-16

---

### Day One!

##### Introduction to Regression

What is Regression and how is it used in Machine Learning?

- The goal of "regression" is to take continous data and find an equation that "best" fits the data so that were able to forecast out a specifc value

```python
import pandas as pd
import quandl
```

# lets us the quandl api to get stock information from Apple

```python
df = quandl.get("WIKI/AAPL")

```
machine learning.....


## Day TWO:


Lets use pandas read_csv function to load our file into a data fram object and display the data frame!

[Downloaded From HERE!! ] (https://data.world/baltimore/baltimore-crime-data)

```python
import pandas as pd

data = pd.read_csv('Baltimore_crime_data.csv') 

```
```python
data
```

Output:

```python
	CrimeDate	CrimeTime	CrimeCode	Location	Description	Inside/Outside	Weapon	Post	District	Neighborhood	Longitude	Latitude	Location 1	Premise	Total Incidents
0	11/04/2017	23:39:00	4E	5700 HAZELWOOD CIR	COMMON ASSAULT	I	HANDS	444.0	NORTHEASTERN	Frankford	-76.53114	39.33952	(39.3395200000, -76.5311400000)	APT/CONDO	1
1	11/04/2017	23:16:00	4E	200 N MOUNT ST	COMMON ASSAULT	I	HANDS	711.0	WESTERN	Franklin Square	-76.64393	39.29141	(39.2914100000, -76.6439300000)	APT/CONDO	1
2	11/04/2017	23:15:00	6C	1100 E NORTH AVE	LARCENY	I	NaN	342.0	EASTERN	East Baltimore Midway	-76.60333	39.31177	(39.3117700000, -76.6033300000)	GROCERY/CO	1
3	11/04/2017	23:15:00	7A	4800 ERDMAN AVE	AUTO THEFT	O	NaN	433.0	NORTHEASTERN	Armistead Gardens	-76.55972	39.30727	(39.3072700000, -76.5597200000)	STREET	1
4	11/04/2017	23:00:00	4E	6400 ELRAY DR	COMMON ASSAULT	NaN	HANDS	632.0	NORTHWESTERN	Cheswolde	-76.69162	39.36942	(39.3694200000, -76.6916200000)	NaN	
```

Now lets create a Pandas DataFrame Object named counts that contains the number of auto thefts, assaults, homicides, and robberies for each district. 

```python
from pandas import DataFrame

auto_theft = data[data["Description"]=="AUTO THEFT"]
auto_counts = DataFrame(auto_theft["District"].value_counts().sort_index())

assault = data[data["Description"]=="COMMON ASSAULT"]
assault_counts = DataFrame(assault["District"].value_counts().sort_index())

robbery = data[data["Description"]=="ROBBERY - STREET"]
robbery_counts = DataFrame(robbery["District"].value_counts().sort_index())

homicide = data[data["Description"]=="HOMICIDE"]
homicide_counts = DataFrame(homicide["District"].value_counts().sort_index())

counts = pd.concat([auto_counts,assault_counts,robbery_counts,homicide_counts], axis=1)

# Heres a Count 
counts.columns = ['Auto Theft', 'Assault', 'Robbery', 'Homicide']

```
Lets check out the count object!

```python
counts
```

Output:
```python
	Auto Theft	Assault	Robbery	Homicide
CENTRAL	1797	5387	2696	112
EASTERN	1914	5303	1408	242
NORTHEASTERN	5155	7077	2881	217
NORTHERN	2826	4229	2154	119
NORTHWESTERN	3635	4234	1809	223
SOUTHEASTERN	2737	6376	3002	99
SOUTHERN	3140	5388	1916	136
SOUTHWESTERN	3476	4483	1373	212
WESTERN	2912	4520	1227	264


```

Now lets plot

```python

counts = DataFrame(data["Description"].value_counts())

import matplotlib
%matplotlib inline

counts.plot(kind='bar')   

```
Output:

![inserting an Image](/images/data_science/week1/balt.jpg)


Lets create a function that contains a regular expression that parse the CrimeData column in the DataFrame and returns the year of Crime!

```python
import re

def getYear(CrimeDate):
    
    regex = r'/'         
    fields = re.split(regex, CrimeDate)
    return fields[2]   

data['Year'] = data['CrimeDate'].apply(getYear)    
function to the CrimeDate column
data[['CrimeDate','Year']].head()

```

Ouput:

```python
	CrimeDate	Year
0	11/04/2017	2017
1	11/04/2017	2017
2	11/04/2017	2017
3	11/04/2017	2017
4	11/04/2017	2017

```

