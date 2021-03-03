---
title: 'Big Data Analysis Day 7ish: Data Summarization and Visualization '

date: 2021-3-2

---


### Data Exploration

What is Data Exploration?

- it is the preliminary analysis of the data to better understand its characteristics



## Summary Statistics

- summarizes *properties of data*

|                     | Quantitative                                    | Qualitative        |
|---------------------|-------------------------------------------------|--------------------|
| Single Attributes   | Mean, Standard Deviation, Median, and Quantiles | Frequency Entropy  |
| Pairs of Attributes | Correlation and Covariance                      | Mutual Information |


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



Lets Look at the Entropy

```python
import numpy as np

prob = data.status.value_counts()
prob = prob/sum(prob)

print("Entropy = ", -np.dot(prob.transpose(),np.log(prob)/np.log(2)))

```

Output:

```python
Entropy =  1.865437105319908
```

### Multivariate Statistics

**Covariance**

- Measures the strength of association between a pair of *quantitative variables*


```python
data[['Age','GPA']]
```

Output:

|    | Age |  GPA |
|---:|----:|-----:|
|  0 |  18 | 3.70 |
|  1 |  20 | 3.30 |
|  2 |  19 | 2.50 |
|  3 |  17 | 3.70 |
|  4 |  18 | 4.00 |
|  5 |  19 | 3.60 |
|  6 |  19 | 2.50 |
|  7 |  19 | 3.25 |
|  8 |  19 | 4.00 |
|  9 |  21 | 2.33 |
| 10 |  20 | 3.45 |
| 11 |  20 | 2.75 |
| 12 |  23 | 3.85 |
| 13 |  22 | 3.33 |
| 14 |  22 | 3.65 |
| 15 |  25 | 3.45 |
| 16 |  23 | 3.75 |


```python
data.cov()
```

Output:

|     |      Age |      GPA |
|----:|---------:|---------:|
| Age | 4.566176 | 0.034522 |
| GPA | 0.034522 | 0.283081 |



**Correlation Coefficient**

- Normalized measure of association between a pair of quantitative variables


```python
data.corr()
```

|     	|      Age 	|      GPA 	|
|----:	|---------:	|---------:	|
| Age 	| 1.000000 	| 0.030364 	|
| GPA 	| 0.030364 	| 1.000000 	|


**Covariance vs Correlation**

- add more




### Mutual Information

- measure of association between two qualitative variables
- Mutual information is a *quantity* that measures a relationship between two random variables that are sampled simultaneously. 

New DataFrame using Columns Gender and Status

```python
data2 = data[["Gender", "status"]] 
```
Output:

|    	| Gender 	|    status 	|
|---:	|-------:	|----------:	|
|  0 	|   Male 	|  freshman 	|
|  1 	|   Male 	|  freshman 	|
|  2 	| Female 	|  freshman 	|
|  3 	| Female 	|  freshman 	|
|  4 	| Female 	|  freshman 	|
|  5 	| Female 	|  freshman 	|
|  6 	|   Male 	| sophomore 	|
|  7 	|   Male 	| sophomore 	|
|  8 	|   Male 	| sophomore 	|
|  9 	|   Male 	| sophomore 	|
| 10 	| Female 	| sophomore 	|
| 11 	| Female 	| sophomore 	|
| 12 	|   Male 	|    junior 	|
| 13 	| Female 	|    junior 	|
| 14 	| Female 	|    junior 	|
| 15 	|   Male 	|    senior 	|
| 16 	| Female 	|    senior 	|


Lets work with this new DataFrame

```python
from pandas import crosstab

freq = crosstab(data2.Gender,data2.status)
freq
```

Output:

| status 	| freshman 	| junior 	| senior 	| sophomore 	|
|-------:	|---------:	|-------:	|-------:	|----------:	|
| Gender 	|          	|        	|        	|           	|
| Female 	|        4 	|      2 	|      1 	|         2 	|
|   Male 	|        2 	|      1 	|      1 	|         4 	|


```python
total = freq.sum().sum()
Pxy = freq/total
Pxy
```

Output:

| status 	| freshman 	|   junior 	|   senior 	| sophomore 	|
|-------:	|---------:	|---------:	|---------:	|----------:	|
| Gender 	|          	|          	|          	|           	|
| Female 	| 0.235294 	| 0.117647 	| 0.058824 	|  0.117647 	|
|   Male 	| 0.117647 	| 0.058824 	| 0.058824 	|  0.235294 	|


Lets measure the Mutual Information now.

```python
from pandas import DataFrame

Px = freq.sum(axis=1)/total
Px
```

Output:

```python
Gender
Female    0.529412
Male      0.470588
dtype: float64
```

```python
Px = DataFrame([Px,Px,Px,Px],index=Pxy.columns).T
Px
```
Output:

| status 	| freshman 	|   junior 	|   senior 	| sophomore 	|
|-------:	|---------:	|---------:	|---------:	|----------:	|
| Gender 	|          	|          	|          	|           	|
| Female 	| 0.529412 	| 0.529412 	| 0.529412 	|  0.529412 	|
|   Male 	| 0.470588 	| 0.470588 	| 0.470588 	|  0.470588 	|

```python
Py = freq.sum(axis=0)/total
Py = DataFrame([Py, Py],index=Pxy.index)
Py
```

Output:

| status 	| freshman 	|   junior 	|   senior 	| sophomore 	|
|-------:	|---------:	|---------:	|---------:	|----------:	|
| Gender 	|          	|          	|          	|           	|
| Female 	| 0.352941 	| 0.176471 	| 0.117647 	|  0.352941 	|
|   Male 	| 0.352941 	| 0.176471 	| 0.117647 	|  0.352941 	|

```python
import numpy as np

temp = Pxy/Px
temp = temp/Py
temp = Pxy*np.log(temp)/np.log(2)
print ("Mutual Information = ", temp.sum().sum())
```

Output:

```python
Mutual Information =  0.06959445749750665
```


### Data Visualization

- Powerful technique for data exploration.

**3 Important things to consider when developing Visual Analytics**

1. Representation
2. Arrangement
3. Selection

**Representation**

How to map the data to a visual format

- Data Objects and their attributes and relationships can be translated into graphical elements such as points, lines, shapes, and colors.

**Arrangement**

- Placement of visual elements within a display
- Can make a large difference in how easy it is to understand the data


**Selection**

- Is the elimination of certain objects and attributes

- Way include/involve the choosing a subset of attributes or objects


Lets look back at our OG Data and work to Plot it!

```python
data
```

Output:

|    	|    status 	| Gender 	| Age 	|  GPA 	|
|---:	|----------:	|-------:	|----:	|-----:	|
|  0 	|  freshman 	|   Male 	|  18 	| 3.70 	|
|  1 	|  freshman 	|   Male 	|  20 	| 3.30 	|
|  2 	|  freshman 	| Female 	|  19 	| 2.50 	|
|  3 	|  freshman 	| Female 	|  17 	| 3.70 	|
|  4 	|  freshman 	| Female 	|  18 	| 4.00 	|
|  5 	|  freshman 	| Female 	|  19 	| 3.60 	|
|  6 	| sophomore 	|   Male 	|  19 	| 2.50 	|
|  7 	| sophomore 	|   Male 	|  19 	| 3.25 	|
|  8 	| sophomore 	|   Male 	|  19 	| 4.00 	|
|  9 	| sophomore 	|   Male 	|  21 	| 2.33 	|
| 10 	| sophomore 	| Female 	|  20 	| 3.45 	|
| 11 	| sophomore 	| Female 	|  20 	| 2.75 	|
| 12 	|    junior 	|   Male 	|  23 	| 3.85 	|
| 13 	|    junior 	| Female 	|  22 	| 3.33 	|
| 14 	|    junior 	| Female 	|  22 	| 3.65 	|
| 15 	|    senior 	|   Male 	|  25 	| 3.45 	|
| 16 	|    senior 	| Female 	|  23 	| 3.75 	|



**Histogram and Kernal Density Plots**

- Shows the distribution of values in a single variable
- Kernel density plots: smoothed version of histogram

```python
%matplotlib inline
data['Age'].hist(normed=True)
data['Age'].plot(kind='kde',style='k--', 'color'= green)
```
Output:

!["Insert Image"](/images/big_data/data_sum/hist.png)



**Box Plots**

- Another way to display the distribution of data

- "Whiskers" of the plot shows the max and minimum values

```python
data.boxplot()
```

Output:
!["Insert Image"](/images/big_data/data_sum/box_plot.png)



**Scatter Plots**

```python
data.plot.scatter(x='Age',y='GPA', color = 'green')
```

Output:
!["Insert Image"](/images/big_data/data_sum/scatter.png)



### Visualizing Multivariate Data


**Parallel Coordinates**



```python
data = p.read_csv('diabetes.csv',header='infer')
data.head()
````
Output:

|   	| preg 	| plas 	| pres 	| skin 	| insu 	| mass 	|  pedi 	| age 	|           class 	|
|--:	|-----:	|-----:	|-----:	|-----:	|-----:	|-----:	|------:	|----:	|----------------:	|
| 0 	|    6 	|  148 	|   72 	|   35 	|    0 	| 33.6 	| 0.627 	|  50 	| tested_positive 	|
| 1 	|    1 	|   85 	|   66 	|   29 	|    0 	| 26.6 	| 0.351 	|  31 	| tested_negative 	|
| 2 	|    8 	|  183 	|   64 	|    0 	|    0 	| 23.3 	| 0.672 	|  32 	| tested_positive 	|
| 3 	|    1 	|   89 	|   66 	|   23 	|   94 	| 28.1 	| 0.167 	|  21 	| tested_negative 	|
| 4 	|    0 	|  137 	|   40 	|   35 	|  168 	| 43.1 	| 2.288 	|  33 	| tested_positive 	|

```python
import pandas
from pandas.plotting import parallel_coordinates
%matplotlib inline

parallel_coordinates(data, 'class')
```

Output:

!["Insert Image"](/images/big_data/data_sum/parallel.png)


### Visualization of Big Data


* Pie Chart
* Bar Chart
* Line Chart
* Bubble Plot
* Tree Map
* Scatter Plot
* Graph/Network-Based