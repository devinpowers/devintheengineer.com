---
title: 'Big Data Analysis Day 7ish: Data Summarization and Visualization '

date: 2021-3-2

---


Ok Lets SUM UP SOME DATA

### Data Exploration

What is Data Exploration?

- it is the preliminary analysis of the data to better understand its characteristics



## Summary Statistics

- summarizes properties of data

|                     | Quantitative                                 | Qualitative        |
|---------------------|----------------------------------------------|--------------------|
| Single Attributes   | Mean Standard Deviation Median and Quantiles | Frequency Entropy  |
| Pairs of Attributes | Correlation and Covariance                   | Mutual Information |


Lets start using Python

```python
import pandas as p

data = p.read_csv('students.csv',header=0)
data
```

Output:

|    |    status | Gender | Age |  GPA |
|---:|----------:|-------:|----:|-----:|
|  0 |  freshman |   Male |  18 | 3.70 |
|  1 |  freshman |   Male |  20 | 3.30 |
|  2 |  freshman | Female |  19 | 2.50 |
|  3 |  freshman | Female |  17 | 3.70 |
|  4 |  freshman | Female |  18 | 4.00 |
|  5 |  freshman | Female |  19 | 3.60 |
|  6 | sophomore |   Male |  19 | 2.50 |
|  7 | sophomore |   Male |  19 | 3.25 |
|  8 | sophomore |   Male |  19 | 4.00 |
|  9 | sophomore |   Male |  21 | 2.33 |
| 10 | sophomore | Female |  20 | 3.45 |
| 11 | sophomore | Female |  20 | 2.75 |
| 12 |    junior |   Male |  23 | 3.85 |
| 13 |    junior | Female |  22 | 3.33 |
| 14 |    junior | Female |  22 | 3.65 |
| 15 |    senior |   Male |  25 | 3.45 |
| 16 |    senior | Female |  23 | 3.75 |


Lets convert Series to a DataFrame using *to_frame()* in Pandas

```python
from pandas import Series

data.GPA.to_frame()
```

Output:

|    |  GPA |
|---:|-----:|
|  0 | 3.70 |
|  1 | 3.30 |
|  2 | 2.50 |
|  3 | 3.70 |
|  4 | 4.00 |
|  5 | 3.60 |
|  6 | 2.50 |
|  7 | 3.25 |
|  8 | 4.00 |
|  9 | 2.33 |
| 10 | 3.45 |
| 11 | 2.75 |
| 12 | 3.85 |
| 13 | 3.33 |
| 14 | 3.65 |
| 15 | 3.45 |
| 16 | 3.75 |

OK awesome, lets **Summarize** this data

```python
print("Average GPA: ", data.GPA.mean())
print("Standard deviation of GPA: ", data.GPA.std())
print("Quantiles of GPA:\n", data.GPA.quantile([.25,.5,.75]))

```

Output:

```python
Average GPA:  3.3594117647058828
Standard deviation of GPA:  0.5320534581721476
Quantiles of GPA:
 0.25    3.25
0.50    3.45
0.75    3.70
Name: GPA, dtype: float64
```

Lets look at the Grade Level

```python
data.status.to_frame()
```

Output:

|    |    status |
|---:|----------:|
|  0 |  freshman |
|  1 |  freshman |
|  2 |  freshman |
|  3 |  freshman |
|  4 |  freshman |
|  5 |  freshman |
|  6 | sophomore |
|  7 | sophomore |
|  8 | sophomore |
|  9 | sophomore |
| 10 | sophomore |
| 11 | sophomore |
| 12 |    junior |
| 13 |    junior |
| 14 |    junior |
| 15 |    senior |
| 16 |    senior |


```python

print("Frequency distribution of Status:\n", data.status.value_counts())
```

Output:

```python
Frequency distribution of Status:
sophomore    6
freshman     6
junior       3
senior       2
Name: status, dtype: int64
```

