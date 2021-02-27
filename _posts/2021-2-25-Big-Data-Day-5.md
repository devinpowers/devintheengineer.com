---
title: 'Big Data Analysis Day 5: Data Quality and Pandas Library '

date: 2021-2-25

---



Working with **Raw** data

**What are some Data Quality Issues that we might encounter?**

- Noise
- Outliers
- Duplicate Data
- Missing Values

Lets dive into each one...

**Noise**

Noise refers to the incorrect/modified values of data, some data is very stable and possesses little variabilty, while other data swings wildly and unpredictably from one value to another

How do we deal with Noise?

Dealing with noise depends on the type of data, for time series low pass filters are often used, for document data we can use software or lookup dictionary

**Outliers**

Are data objects with charactersitics that are considerbly different than most of the other data objects in the data set!


**Duplicate Data**

- Where data set may include data objects that are duplicates (common problem when merging data from multiple sources)

How do we handle Duplicate Data?



**Missing Values**

Why is there missing values?
- Information/data wasn't collected
- Attributes may not apply to all cases

How do we handle missing values?

- We could remove data objects with missing values
- Ignore the missing values during analysis


One of the best Python libraries with Data Analysis is **Pandas** as we already know

The Pandas Library has two main data structures

1. **Series**: a one-dimensional array-like object
2. **DataFrame**: spreadsheet-like data structure containing a collection of ordered columns



**Series**

[Pandas Documentation](https://pandas.pydata.org/pandas-docs/stable/reference/series.html)

Lets use an example of Series

```python
from pandas import Series
```

```python
points = Series([40, 24, 25, 29, 32, 33, 45, 54])
points
```
Output:
```python
0    40
1    24
2    25
3    29
4    32
5    33
6    45
7    54
dtype: int64
```


Where on the Left represents the **Index** and the right represents the **Value** and shows the dtype (datatype) which is an integer in this case

```python
points.array
```

Output:
```python
<PandasArray>
[40, 24, 25, 29, 32, 33, 45, 54]
Length: 8, dtype: int64
```

```python
points.values
```

Output:
```python
array([40, 24, 25, 29, 32, 33, 45, 54])
```

```python
points.index
```
Output:

```python
RangeIndex(start=0, stop=8, step=1)
```

We can change the Index from numbers to anything we would like!

Let use an example of the NBA, with timestamp being the index and points being the value and put them together in a Series

```python
timestamp = ['1/5/2019', '1/6/2019', '1/8/2019','1/4/2019','1/19/2019', '1/21/2019','1/23/2019','1/30/2019']
points  = [40, 24, 25, 29, 32, 33, 45, 54]

NBA_ = Series(points, index = timestamp)

```

```python
NBA_
```

Output:
```python
1/5/2019     40
1/6/2019     24
1/8/2019     25
1/4/2019     29
1/19/2019    32
1/21/2019    33
1/23/2019    45
1/30/2019    54
dtype: int64
```

Lets check a random date to see the number of points scored!
```python
NBA_['1/8/2019']
```
Ouput:
```python
25
```

Check the dates when Lebron scored more than 25 Points

```python
NBA_[NBA_ > 25]
```
Ouput:
```python
1/5/2019     40
1/4/2019     29
1/19/2019    32
1/21/2019    33
1/23/2019    45
1/30/2019    54
dtype: int64
```

Lets plot
```python
%matplotlib inline
plt.figure(figsize=(10,5)) 

NBA_.plot(kind = "line", color = 'green')
```

Output:

![inserting image](/images/big_data/nba.png)

**Dealing with Missing Values**

```python
NBA_['1/6/2019'] = None
```

```python
NBA_.count()
```
Ouput:
```
7
```

```python
NBA_.isnull()
```

Output:
```python
1/5/2019     False
1/6/2019      True
1/8/2019     False
1/4/2019     False
1/19/2019    False
1/21/2019    False
1/23/2019    False
1/30/2019    False
dtype: bool
```

How would we fill that Null value (missing value) in ?

Well we could use the median value of all the points scored and then fill it in.

Well there is a Pandas function for that (.fillna(value to fill)) and we can find the median value of our points scored and fill it in our missing value during the time

```python
NBA_.fillna(NBA_.median())
```

Output:
```python
1/5/2019     40.0
1/6/2019     33.0
1/8/2019     25.0
1/4/2019     29.0
1/19/2019    32.0
1/21/2019    33.0
1/23/2019    45.0
1/30/2019    54.0
dtype: float64
```

Note: The data 1/6/2019 was filled in with 33 which is the **median** value of points scored

Another thing that we could do, if we had a **"missing"** value for example

```python
NBA_['1/6/2019'] = None
NBA_
```

Output:
```python
1/5/2019     40.0
1/6/2019      NaN
1/8/2019     25.0
1/4/2019     29.0
1/19/2019    32.0
1/21/2019    33.0
1/23/2019    45.0
1/30/2019    54.0
dtype: float64
```

We could just remove the date

```python
NBA_ = NBA_[NBA_.notnull()]
NBA_
```

Output:
```python
1/5/2019     40.0
1/8/2019     25.0
1/4/2019     29.0
1/19/2019    32.0
1/21/2019    33.0
1/23/2019    45.0
1/30/2019    54.0
dtype: float64
```

or this way:

```python
NBA_ = NBA_.dropna()
NBA_
```

Output:
```python
1/5/2019     40
1/8/2019     25
1/4/2019     29
1/19/2019    32
1/21/2019    33
1/23/2019    45
1/30/2019    54
dtype: object
```

Either or drops the timestamp (index)!

**Lets look at Outliers**

```python
NBA_['1/6/2019'] = 100
```

```python
NBA_.hist()
```

Output:

![inserting an Image](/images/big_data/nba_hist.png)

```python
std_values = (NBA_ - NBA_.mean())/NBA_.std()
std_points = Series(std_values, index = NBA_.index)
std_points.hist()
```
Output:

![inserting an Image](/images/big_data/nba_hist2.png)


```python
std_points[std_points > 2]
```

Output:
```python
1/6/2019    2.28305
dtype: object
```



## DataFrame


Lets work more with DataFrames

```python
import pandas as pd
from pandas import DataFrame
```

```python

data = {'Name': ['Lebron James', 'Steph Curry', 'Kevin Durant','Chris Paul'],
       'Age': [36, 31, 34, 36],
       'Height': [6.8, 6.2, 6.9, 6.0]}
users = DataFrame(data)


```

```python
users
```

Output:
```python

Name	            Age	Height
0	Lebron James	36	6.8
1	Steph Curry	    31	6.2
2	Kevin Durant	34	6.9
3	Chris Paul  	36	6.0
```

```python
users["Age"]
```

Output:
```python
0    36
1    31
2    34
3    36
Name: Age, dtype: int64
```

```python
users.columns
```

Output:

```python
Index(['Name', 'Age', 'Height'], dtype='object')
```

```python
users.shape
```

```python
(4, 3)
```

```python
users.index = [1,2,3,4]
users.transpose()
```

Output:

```python
            	1	            2	        3	        4
Name	Lebron James	Steph Curry 	Kevin Durant	Chris Paul
Age	        36          	31	            34	            36
Height  	6.8	            6.2	            6.9         	6
```

```python
users[users.Age>33]
```
Output:

```python
	Name	        Age	    Height
1	Lebron James	36	    6.8
3	Kevin Durant	34	    6.9
4	Chris Paul      36	    6.0
```

```python
users.describe().transpose()
```

Output:

```python
	    count	mean	std	        min	    25%	    50%	    75%	    max
Age     4.0	    34.250	2.362908	31.0	33.25	35.0	36.000	36.0
Height	4.0 	6.475	0.442531	6.0	    6.15	6.5 	6.825	6.9
```
