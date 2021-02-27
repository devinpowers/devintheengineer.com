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
prices.index
```
Output:

```python
RangeIndex(start=0, stop=8, step=1)
```

We can change the Index from numbers to anything we would like!

Let use an example of the stockmarket, with timestamp being the index and prices being the value and put them together in a Series

```python
timestamp = ['1/5/2019', '1/6/2019', '1/8/2019','1/4/2019','1/19/2019', '1/1/2019','1/11/2019','1/12/2019']
prices = [40.50, 41.22, 40.65, 39.80, 40.43, 41.69, 42.02, 44.38]

stockprice = Series(prices, index = timestamp)
```

```python
stockprice
```

Output:
```python
1/5/2019     40.50
1/6/2019     41.22
1/8/2019     40.65
1/14/2019     39.80
1/19/2019    40.43
1/21/2019     41.69
1/23/2019    42.02
1/30/2019    44.38
dtype: float64
```

```python
stockprice['1/8/2019']
```
Ouput:
```python
40.65
```




**DataFrame**
