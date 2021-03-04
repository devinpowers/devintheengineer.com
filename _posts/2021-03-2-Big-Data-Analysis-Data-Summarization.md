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




Lets start using Python and a NBA Combine data csv file!

```python
import pandas as p

data = p.read_csv('nba_draft_combine_all_years.csv',header=0)
data
```

Output:

|     	| Unnamed: 0 	|                Player 	| Year 	| Draft pick 	| Height (No Shoes) 	| Height (With Shoes) 	| Wingspan 	| Standing reach 	| Vertical (Max) 	| Vertical (Max Reach) 	| Vertical (No Step) 	| Vertical (No Step Reach) 	| Weight 	| Body Fat 	| Hand (Length) 	| Hand (Width) 	| Bench 	| Agility 	| Sprint 	|
|----:	|-----------:	|----------------------:	|-----:	|-----------:	|------------------:	|--------------------:	|---------:	|---------------:	|---------------:	|---------------------:	|-------------------:	|-------------------------:	|-------:	|---------:	|--------------:	|-------------:	|------:	|--------:	|-------:	|
|   0 	|          0 	|         Blake Griffin 	| 2009 	|        1.0 	|             80.50 	|               82.00 	|    83.25 	|          105.0 	|           35.5 	|                140.5 	|               32.0 	|                    137.0 	|  248.0 	|      8.2 	|           NaN 	|          NaN 	|  22.0 	|   10.95 	|   3.28 	|
|   1 	|          1 	|     Terrence Williams 	| 2009 	|       11.0 	|             77.00 	|               78.25 	|    81.00 	|          103.5 	|           37.0 	|                140.5 	|               30.5 	|                    134.0 	|  213.0 	|      5.1 	|           NaN 	|          NaN 	|   9.0 	|   11.15 	|   3.18 	|
|   2 	|          2 	|      Gerald Henderson 	| 2009 	|       12.0 	|             76.00 	|               77.00 	|    82.25 	|          102.5 	|           35.0 	|                137.5 	|               31.5 	|                    134.0 	|  215.0 	|      4.4 	|           NaN 	|          NaN 	|   8.0 	|   11.17 	|   3.14 	|
|   3 	|          3 	|      Tyler Hansbrough 	| 2009 	|       13.0 	|             80.25 	|               81.50 	|    83.50 	|          106.0 	|           34.0 	|                140.0 	|               27.5 	|                    133.5 	|  234.0 	|      8.5 	|           NaN 	|          NaN 	|  18.0 	|   11.12 	|   3.27 	|
|   4 	|          4 	|            Earl Clark 	| 2009 	|       14.0 	|             80.50 	|               82.25 	|    86.50 	|          109.5 	|           33.0 	|                142.5 	|               28.5 	|                    138.0 	|  228.0 	|      5.2 	|           NaN 	|          NaN 	|   5.0 	|   11.17 	|   3.35 	|
| ... 	|        ... 	|                   ... 	|  ... 	|        ... 	|               ... 	|                 ... 	|      ... 	|            ... 	|            ... 	|                  ... 	|                ... 	|                      ... 	|    ... 	|      ... 	|           ... 	|          ... 	|   ... 	|     ... 	|    ... 	|
| 512 	|        512 	|             Peter Jok 	| 2017 	|        NaN 	|             76.25 	|               77.75 	|    80.00 	|          102.0 	|           31.0 	|                133.0 	|               26.5 	|                    128.5 	|  202.0 	|     11.0 	|          8.25 	|         9.50 	|   NaN 	|   11.34 	|   3.41 	|
| 513 	|        513 	|          Rawle Alkins 	| 2017 	|        NaN 	|             74.50 	|               75.75 	|    80.75 	|           99.0 	|           40.5 	|                139.5 	|               31.5 	|                    130.5 	|  223.0 	|     11.0 	|          8.75 	|        10.00 	|   NaN 	|   11.99 	|   3.30 	|
| 514 	|        514 	| Sviatoslav Mykhailiuk 	| 2017 	|        NaN 	|             78.50 	|               79.50 	|    77.00 	|          100.0 	|           33.0 	|                133.0 	|               27.0 	|                    127.0 	|  220.0 	|     11.4 	|          8.00 	|         9.25 	|   NaN 	|   12.40 	|   3.53 	|
| 515 	|        515 	|          Thomas Welsh 	| 2017 	|        NaN 	|             83.50 	|               84.50 	|    84.00 	|          109.5 	|            NaN 	|                  NaN 	|                NaN 	|                      NaN 	|  254.0 	|     10.9 	|          9.00 	|        10.50 	|   NaN 	|     NaN 	|    NaN 	|
| 516 	|        516 	|          V.J. Beachem 	| 2017 	|        NaN 	|             78.25 	|               80.00 	|    82.25 	|          104.5 	|           37.0 	|                141.5 	|               30.0 	|                    134.5 	|  193.0 	|      6.8 	|          8.50 	|         9.00 	|   NaN 	|   11.18 	|   3.26 	|




Lets First clean up some of this data and take only the **Columns** that were intrested in using!

**Columns that I am intrested in:** Player, Year, Height (No Shoes), Wingspan, Vertical (Max), Weight, Body Fat

Lets create a new DataFrame using just those Columns!


This file is awesome becuase we actually do need to *Clean* it!, we have alot of *missing data* (NaN)


```python
data_update = data[['Player','Year', 'Height (No Shoes)', 'Wingspan', 'Vertical (Max)', 'Weight', 'Body Fat']]

data_update
```


Output:

|     	|                Player 	| Year 	| Height (No Shoes) 	| Wingspan 	| Vertical (Max) 	| Weight 	| Body Fat 	|   	|
|----:	|----------------------:	|-----:	|------------------:	|---------:	|---------------:	|-------:	|---------:	|---	|
|   0 	|         Blake Griffin 	| 2009 	|             80.50 	|    83.25 	|           35.5 	|  248.0 	|      8.2 	|   	|
|   1 	|     Terrence Williams 	| 2009 	|             77.00 	|    81.00 	|           37.0 	|  213.0 	|      5.1 	|   	|
|   2 	|      Gerald Henderson 	| 2009 	|             76.00 	|    82.25 	|           35.0 	|  215.0 	|      4.4 	|   	|
|   3 	|      Tyler Hansbrough 	| 2009 	|             80.25 	|    83.50 	|           34.0 	|  234.0 	|      8.5 	|   	|
|   4 	|            Earl Clark 	| 2009 	|             80.50 	|    86.50 	|           33.0 	|  228.0 	|      5.2 	|   	|
| ... 	|                   ... 	|  ... 	|               ... 	|      ... 	|            ... 	|    ... 	|      ... 	|   	|
| 512 	|             Peter Jok 	| 2017 	|             76.25 	|    80.00 	|           31.0 	|  202.0 	|     11.0 	|   	|
| 513 	|          Rawle Alkins 	| 2017 	|             74.50 	|    80.75 	|           40.5 	|  223.0 	|     11.0 	|   	|
| 514 	| Sviatoslav Mykhailiuk 	| 2017 	|             78.50 	|    77.00 	|           33.0 	|  220.0 	|     11.4 	|   	|
| 515 	|          Thomas Welsh 	| 2017 	|             83.50 	|    84.00 	|            NaN 	|  254.0 	|     10.9 	|   	|
| 516 	|          V.J. Beachem 	| 2017 	|             78.25 	|    82.25 	|           37.0 	|  193.0 	|      6.8 	|   	|



Lets look into *Height* more...


Lets use *Series.to_frame()* function to convert the given series object to a dataframe

```python
from pandas import Series

data_update["Height (No Shoes)"].to_frame()
```

Output:

|     	| Height (No Shoes) 	|
|----:	|------------------:	|
|   0 	|             80.50 	|
|   1 	|             77.00 	|
|   2 	|             76.00 	|
|   3 	|             80.25 	|
|   4 	|             80.50 	|
| ... 	|               ... 	|
| 512 	|             76.25 	|
| 513 	|             74.50 	|
| 514 	|             78.50 	|
| 515 	|             83.50 	|
| 516 	|             78.25 	|


As we can see in the output, the Series.to_frame() function has successfully converted the *"Height (No Shoes) "* series object to a dataframe.

Now lets look at some basic statistics like Mean and Standard Deviation of *Height*

```python
print("Average Height: ", data_update["Height (No Shoes)"].mean())
print("Standard deviation of Height: ", data_update["Height (No Shoes)"].std())
print("Quantiles of Height%:\n", data_update["Height (No Shoes)"].quantile([.25,.5,.75]))
```

Output:

```python
Average Height:  77.60928433268859
Standard deviation of Height:  3.287632579106095
Quantiles of Height%:
 0.25    75.25
0.50    77.75
0.75    80.00
Name: Height (No Shoes), dtype: float64
```

Lets look into another column, *Year* (which is the year the player was drafted).

```python
data_update["Year"].to_frame()
```

Output:

|     	| Year 	|
|----:	|-----:	|
|   0 	| 2009 	|
|   1 	| 2009 	|
|   2 	| 2009 	|
|   3 	| 2009 	|
|   4 	| 2009 	|
| ... 	|  ... 	|
| 512 	| 2017 	|
| 513 	| 2017 	|
| 514 	| 2017 	|
| 515 	| 2017 	|
| 516 	| 2017 	|

```python
print("Frequency distribution of Years:\n ", data_update["Year"].value_counts())
```

Output:

```python
Frequency distribution of Years:
  2015    63
2013    62
2016    61
2012    61
2017    60
2014    59
2011    53
2009    50
2010    48
Name: Year, dtype: int64
```


### Lets look at the Entropy

```python
import numpy as np

prob = data_update["Year"].value_counts()
prob = prob/sum(prob)
print("Entropy = ", -np.dot(prob.transpose(),np.log(prob)/np.log(2)))
```

Output:

```python
Entropy =  3.163693718146242
```

#### Multivariate Statistics

**Covariance** and **Correlation**

```python
data_update_2 = data[["Weight","Height (No Shoes)"]]
data_update_2
```

Output:

|     	| Weight 	| Height (No Shoes) 	|
|----:	|-------:	|------------------:	|
|   0 	|  248.0 	|             80.50 	|
|   1 	|  213.0 	|             77.00 	|
|   2 	|  215.0 	|             76.00 	|
|   3 	|  234.0 	|             80.25 	|
|   4 	|  228.0 	|             80.50 	|
| ... 	|    ... 	|               ... 	|
| 512 	|  202.0 	|             76.25 	|
| 513 	|  223.0 	|             74.50 	|
| 514 	|  220.0 	|             78.50 	|
| 515 	|  254.0 	|             83.50 	|
| 516 	|  193.0 	|             78.25 	|


**Covariance**

```python
data_update_2.cov()
```

Output:

|                   	|     Weight 	| Height (No Shoes) 	|
|------------------:	|-----------:	|------------------:	|
|            Weight 	| 609.277023 	|         60.195793 	|
| Height (No Shoes) 	|  60.195793 	|         10.808528 	|

**Correlation**

```python
data_update_2.corr()
```

Output:

|                   	|   Weight 	| Height (No Shoes) 	|
|------------------:	|---------:	|------------------:	|
|            Weight 	| 1.000000 	|          0.741515 	|
| Height (No Shoes) 	| 0.741515 	|          1.000000 	|

#### Some Plotting with this Data!

```python
%matplotlib inline
```
**BoxPlot**

```python
data_update_2.boxplot()
```

!["Insert Image"](/images/big_data/data_sum/nba_box_plot.png)


**Histogram**

```python
%matplotlib inline
data_update_2['Height (No Shoes)'].hist(normed=True)
data_update_2['Height (No Shoes)'].plot(kind='kde',style='k--')
```

!["Insert Image"](/images/big_data/data_sum/nba_hist.png)


**Scatter Plot**

```python
data_update_2.plot.scatter(x ='Weight', y = 'Height (No Shoes)', color = 'blue')
```

!["Insert Image"](/images/big_data/data_sum/nba_scatter.png)






## Another Example Using School Grade File!!

Lets convert Series to a DataFrame using *to_frame()* in Pandas

```python
import pandas as p

data = p.read_csv('students.csv',header=0)
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