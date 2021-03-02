---
title: 'Big Data Analysis Day 6: Data Preprocessing '

date: 2021-2-28

---

#### How do we **Transform Raw Data** into a more useful representation ?

- Data Cleaning
    * Noise, Outliers, Duplicate Data, Missing Values
- Aggregation
- Sampling
- Feature Extraction
- Discretization


#### Sampling

What is Sampling?

- Sampling is a technique use for **data reduction**, it's key principle for effective sampling is to find a representative sample

- There are different Types of Sampling

    * Simple Random Sampling: Equal probability of selecting any particular item in the dataset
    * Stratified Sampling: split the data into several partition, then draw random samples from each partition
    * Sampling without Replacement: As each item is selected, it is removed from the population
    * Sample with Replacement: Items are not removed from the population as they're selected for the sample, therefore the same item can be selected more than once



Python Examples:

```python
import pandas as p
data = p.read_csv('diabetes.csv', header= 0)
data[:5]
```
Output:
```python
	preg	plas	pres	skin	insu	mass	pedi	age	    class
0	6	    148	    72	    35	    0	    33.6	0.627	50	    tested_positive
1	1	    85  	66	    29  	0	    26.6	0.351	31	    tested_negative
2	8	    183	    64	    0	    0	    23.3	0.672	32	    tested_positive
3	1	    89	    66	    23	    94	    28.1	0.167	21	    tested_negative
4	0	    137	    40	    35	    168	    43.1	2.288	33	    tested_positive
```

Now we will use the **DataFrame.sample()** in Pandas, the sample method returns a **random sample** of items from our dataframe

**Parameters**

**n** = int -> Number of items from axis to return

Other Parameters in the link below

[Pandas Documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sample.html)

```python
sample = data.sample(n = 5)
sample
```

Output:

```python
        preg	plas	pres	skin	insu	mass	pedi	age	class
351	    4	    137	    84	    0	    0	    31.2	0.252	30	tested_negative
466	    0	    74	    52	    10	    36	    27.8	0.269	22	tested_negative
528	    0	    117	    66	    31	    188	    30.8	0.493	22	tested_negative
683	    4	    125	    80  	0	    0	    32.3	0.536	27	tested_positive
3	    1	    89	    66	    23	    94	    28.1	0.167	21	tested_negative
```

Now we have **5 random samples** (rows) from our CSV file



#### Aggregation

What is Aggregation?

- Data Aggregation is high-level data which is acquired by combining individual-level data

Why?

* Data Reduction : smaller data set means less memory and processing time for programmers
* More **Stable** Data : less **noise** to deal with
* Change of Scale


#### Discretization

- Discretization is the process of transferring continuous functions, models, variables, and equations into **discrete counterparts**. (think of bins)

Lets first look at Ordinal and Numeric Attributes

**Ordinal Attributes** are where order matters but not the difference between values

* *Examples:* social economic status (low income, middle income, high income)

**Numeric Attribute** is data expressed in numbers 

* *Examples:*  Weight, Height, Salary


We use **Discretization** to split the range of **numeric attributes** into discrete number of intervals (split age groups: 20-30, 31-40, 41-50, 51-60, etc)

**Unsupervised Discretization**

*Is  splits the range of the numeric attributes into bins*

- There is **Equal Interval Width**, which splits the range of numeric attribute into equal length intervals (bins), its easy to implement, but susceptible to outliers

- There is **Equal Frequency**, which splits the range of numeric attribute in such a way that each interval (bin) has the same number of points, reduces outliers, but may not be consistent with structure of the data

[Pandas Documentation on Cutting ](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.cut.html)

Python Examples of both using **age** to put into bins

```python
data.age.describe()
```

Output:
```python
count    768.000000
mean      33.240885
std       11.760232
min       21.000000
25%       24.000000
50%       29.000000
75%       41.000000
max       81.000000
Name: age, dtype: float64
```
**Equal Interval Width** putting *age* paramter into 5 different bins

```python
age_bins = p.cut(data.age, 5)
age_bins.head()
```

Output:
```python
0     (45.0, 57.0]
1    (20.94, 33.0]
2    (20.94, 33.0]
3    (20.94, 33.0]
4    (20.94, 33.0]
Name: age, dtype: category
Categories (5, interval[float64]): [(20.94, 33.0] < (33.0, 45.0] < (45.0, 57.0] < (57.0, 69.0] < (69.0, 81.0]]
```
We can see the 5 **equal-width** bins : (20.94, 33.0] < (33.0, 45.0] < (45.0, 57.0] < (57.0, 69.0] < (69.0, 81.0] 

Lets put them into 5 **equal-frequency** bins
```python
age_bins = p.cut(data.age, [20,40,50,60,81])
age_bins.head()
```

Output:
```python
0    (40, 50]
1    (20, 40]
2    (20, 40]
3    (20, 40]
4    (20, 40]
Name: age, dtype: category
Categories (4, interval[int64]): [(20, 40] < (40, 50] < (50, 60] < (60, 81]]
```

The Output above Discretize into 5 **equal frequency** bins: (20, 40] < (40, 50] < (50, 60] < (60, 81]


**Supervised Discretization Example**

In this example, let *Buy* be the **class attribute** and were intrested in discretize the *Age* attribute, we want the bins to be as close to homogeneous as possible

- Supervised Discretization methods take the class into account when setting discretization boundaries

| Age | Buy |
|-----|-----|
| 10  | No  |
| 15  | No  |
| 18  | Yes |
| 19  | Yes |
| 24  | No  |
| 29  | Yes |
| 30  | Yes |
| 31  | Yes |
| 40  | No  |
| 44  | No  |
| 55  | No  |
| 64  | No  |

*Unsupervised Discretization* Approach

**Equal Width:** interval = (64-10)/3 = 54/3 = 18

|         | Yes | No |
|---------|-----|----|
| <28     | 2   | 3  |
| (28,46) | 3   | 2  |
| > 46    | 0   | 2  |

**Equal Frequency:**

|             | Yes | No |
|-------------|-----|----|
| <21.5       | 2   | 2  |
| (21.5,35.5) | 3   | 1  |
| > 35.5      | 0   | 4  |

We can see that both approaches can produce intervals that contain *non-homogeneous* classes


**Using Supervised Discretization**


|              | Yes | No |
|--------------|-----|----|
| <16.5        | 0   | 2  |
| (16.5, 35.5) | 5   | 1  |
| > 35.5       | 0   | 4  |

We see that our goal is to ensure that each bin contains data points from *one class*, in the above table we can see a more **homogeneous** classes representation


### Different Supervised Discretization Techniques

**Entropy-based Discretization**

- A very common **Supervised Discretization method**
- Entropy is a measure of **impurity** (randomness in a set) (Remember Thermodynamics)
- Measure of Disorder
    * Measured from range of 0 to 1
    * **Higher entropy** implies data points are from a large number of classes (heterogeneous)
    * **Lower entropy** implies *most* of the data points are from the same class 

!["insert image"](/images/big_data/entropy.png)

Where:

**pi**: is the fraction of the data objects belonging to class **i**

example: For Bin 2 below:

P(Yes) = 1/6 and P(No) = 5/6 

**Entropy** = -(1/6)log2(1/6)) - (5/6)log2(1/6) = *0.65*

If we look back on our table above:

*using the Entropy Equation*

**Bin 1**

|     |   |
|-----|---|
| Yes | 6 |
|-----|---|
|  No | 6 |

Calculating the Entropy = *0*

**Bin 2**

|     |   |
|-----|---|
| Yes | 1 |
|-----|---|
| No  | 5 |

Calculating the Entropy = *0.65*

**Bin 3**

|     |   |
|-----|---|
| Yes | 2 |
|-----|---|
| No  | 4 |


Calculating the Entropy = *0.92*

As we can see after calculating the entropy of each *bin*, as the bin becomes less homogeneous, the entropy increases (value is closer to 1)!

How would one come up with the best way to split the data into Bins?

- kinda trial and error

### Curse of Dimensionality

* The Curse of Dimensionality indicates that the number of samples needed to estimate an arbitrary function with a given level of accuracy grows exponentially with respect to the number of input variables

![insert image](/images/big_data/curse_dim.png)

* As the number of dimensions increases, the higher chance for the model to overfit *noisy* observations and need for more examples to figure out which attributes are most relevant to predict the different classes

*Lets Look at where this would occur:*

Lets say we want to *build a model* to **predict if a user will buy an item at a store by using their age.** We will be using the previous table that we've been working with!

| Age | Buy |
|-----|-----|
| 10  | No  |
| 15  | No  |
| 18  | Yes |
| 19  | Yes |
| 24  | No  |
| 29  | Yes |
| 30  | Yes |
| 31  | Yes |
| 40  | No  |
| 44  | No  |
| 55  | No  |
| 64  | No  |

Lets add more features like time spent at the store:

| Age | Buy | Time Spent |
|-----|-----|------------|
| 10  | No  | 40         |
| 15  | No  | 105        |
| 18  | Yes | 100        |
| 19  | Yes | 110        |
| 24  | No  | 95         |
| 29  | Yes | 180        |
| 30  | Yes | 120        |
| 31  | Yes | 100        |
| 40  | No  | 60         |
| 44  | No  | 44         |
| 55  | No  | 110        |
| 64  | No  | 74         |


Now we can use two attributes *age* and *Time Spent* to predict if a user will buy an item from the store.

Lets add even more features to our table!

| Age | Buy | Time Spent | Member | # Friends |
|-----|-----|------------|--------|-----------|
| 10  | No  | 40         | 2      | 5         |
| 15  | No  | 105        | 0      | 10        |
| 18  | Yes | 100        | 0      | 5         |
| 19  | Yes | 110        | 5      | 30        |
| 24  | No  | 95         | 0      | 2         |
| 29  | Yes | 180        | 2      | 20        |
| 30  | Yes | 120        | 4      | 5         |
| 31  | Yes | 100        | 2      | 70        |
| 40  | No  | 60         | 0      | 11        |
| 44  | No  | 44         | 0      | 8         |
| 55  | No  | 110        | 1      | 2         |
| 64  | No  | 74         | 1      | 0         |



This is when  the *Curse of Dimensionality* could come into play.

How do we **Overcome the Curse of Dimensionality**?

1. Feature Subset Selection: Where we *pick a set of attributes* to build our prediction model that eliminate the irrelevant and highly correlated ones

2. Feature Extraction: Where we construct a new set of attributes based on combination of our original attributes

**Python Example of Feature Selection**

Here is our table:

| Age | Buy | Time Spent | Member | # Friends | Amount Spent ($) |
|-----|-----|------------|--------|-----------|------------------|
| 10  | No  | 40         | 2      | 5         | 0                |
| 15  | No  | 105        | 0      | 10        | 0                |
| 18  | Yes | 100        | 0      | 5         | 20.5             |
| 19  | Yes | 110        | 5      | 30        | 55.45            |
| 24  | No  | 95         | 0      | 2         | 0                |
| 29  | Yes | 180        | 2      | 20        | 100.5            |
| 30  | Yes | 120        | 4      | 5         | 35.5             |
| 31  | Yes | 100        | 2      | 70        | 200.5            |
| 40  | No  | 60         | 0      | 11        | 0                |
| 44  | No  | 44         | 0      | 8         | 0                |
| 55  | No  | 110        | 1      | 2         | 0                |
| 64  | No  | 74         | 1      | 0         | 0                |


For our model, we should select the *non-correlated features* when doing our analysis.



```python
import pandas as p
data = p.read_csv('buy.csv', header=0')
```
Use .corr() function in Pandas

```python
data.corr()
```

Output (Correlation Matrix):

|                 |       age | membershipYears | numberOfFriends | AmountSpent | NumPurchases |
|----------------:|----------:|----------------:|----------------:|------------:|-------------:|
|             age |  1.000000 |       -0.334731 |       -0.253233 |   -0.303731 |    -0.393919 |
| membershipYears | -0.334731 |        1.000000 |        0.343459 |    0.851307 |     0.900591 |
| numberOfFriends | -0.253233 |        0.343459 |        1.000000 |    0.085086 |     0.288885 |
|     AmountSpent | -0.303731 |        0.851307 |        0.085086 |    1.000000 |     0.853188 |
|    NumPurchases | -0.393919 |        0.900591 |        0.288885 |    0.853188 |     1.000000 |


Now we can select the *non-correlated* features for our analysis


### Feature Selection Example

* Where we create a new set of attributes from our original *raw* data

Example: Face Detection in Images

### Principal Component Analysis

* A common approach for **Feature Extraction**
* Construct a new set of dimensions (attributes) that better represents (captures) variability of the data 

```python
import pandas as p
data = p.read_csv('buy.csv', header=0)
data
```

Output:

|    | Age | Membership Years | Number Of Friends | Amount Spent | Number of Purchases |
|---:|----:|-----------------:|------------------:|-------------:|--------------------:|
|  0 |  21 |                2 |                 5 |          100 |                   2 |
|  1 |  38 |                0 |                10 |           10 |                   1 |
|  2 |  18 |                0 |                 5 |           25 |                   1 |
|  3 |  19 |                5 |                30 |         1000 |                  25 |
|  4 |  24 |                0 |                 2 |           50 |                   3 |
|  5 |  29 |                2 |                20 |          200 |                   7 |
|  6 |  30 |                4 |                 5 |         1500 |                  15 |
|  7 |  31 |                2 |                70 |          150 |                   5 |
|  8 |  40 |                0 |                11 |           70 |                   4 |
|  9 |  44 |                0 |                 8 |           10 |                   1 |
| 10 |  55 |                1 |                 2 |           80 |                   3 |
| 11 |  64 |                1 |                 0 |           30 |                   1 |


```python
data.corr()
```

Output:

|                 |      ages | membershipYears | numberOfFriends | AmountSpent | NumPurchases |
|----------------:|----------:|----------------:|----------------:|------------:|-------------:|
|             age |  1.000000 |       -0.334731 |       -0.253233 |   -0.303731 |    -0.393919 |
| membershipYears | -0.334731 |        1.000000 |        0.343459 |    0.851307 |     0.900591 |
| numberOfFriends | -0.253233 |        0.343459 |        1.000000 |    0.085086 |     0.288885 |
|     AmountSpent | -0.303731 |        0.851307 |        0.085086 |    1.000000 |     0.853188 |
|    NumPurchases | -0.393919 |        0.900591 |        0.288885 |    0.853188 |     1.000000 |

We can Note that **Membership Years**, **Amount Spend**, and the **number of purchases** are correlated


*Now lets Compute the Principal Components*

[ insert example of Principal Components here]


### Exercises to help learn how to use some of the Preprocessing Functions in Python

[Using Dataset from here](https://archive.ics.uci.edu/ml/datasets/Auto+MPG)


[Regular Expression Documentation](https://docs.python.org/3/library/re.html)

```python
import pandas as pd
import re
```

```python
column_names = ['MPG','Cylinders','Displacement','Horsepower','Weight','Acceleration','Model Year','Origin','Car Name']
```

```python
def load_data(row):
    
    reg = '\s+' # this splits by 'spaces'
    
    fields = pd.Series([None if x == '?' else x for x in re.split(reg, row)])
    return fields
```


```python
temp_data = pd.read_csv("auto-mpg.data", sep = '\t', header = None)
```


```python
temp_data
```

Output:

```python
	            0	                                        1
0	18.0 8 307.0 130.0 3504. 12...	chevrolet chevelle malibu
1	15.0 8 350.0 165.0 3693. 11...	buick skylark 320
2	18.0 8 318.0 150.0 3436. 11...	plymouth satellite

```

```python
data = pd.DataFrame(temp_data[0].apply(load_data))
data
```

```python
	0	    1	    2	    3	    4	    5	 6	7
0	18.0	8	307.0	130.0	3504.	12.0	70	1
1	15.0	8	350.0	165.0	3693.	11.5	70	1
2	18.0	8	318.0	150.0	3436.	11.0	70	1
```


Lets add the first 8 Columns to the DataFrame Data 
```python
data.columns = column_names[:8]
column_names[:8]
```

Lets print the dataframe!

```python
data.head()
```

Output:

```python
	MPG	Cylinders	Displacement	Horsepower	Weight	Acceleration	Model Year	Origin
0	18.0	8	        307.0	        130.0	3504.	    12.0	        70	        1
1	15.0	8	        350.0	        165.0	3693.	    11.5	        70	        1
2	18.0	8	        318.0	        150.0	3436.	    11.0	        70	        1
3	16.0	8	        304.0	        150.0	3433.	    12.0	        70      	1
4	17.0	8	        302.0	        140.0	3449.	    10.5	        70	        1
```


Lets add the last column to the DataFrame
```python
data[column_names[8]] = temp_data[1]
data.head()
```

Output:

Here our Updated table with all the Correct Column names

|   |  MPG | Cylinders | Displacement | Horsepower | Weight | Acceleration | Model Year | Origin |                  Car Name |
|--:|-----:|----------:|-------------:|-----------:|-------:|-------------:|-----------:|-------:|--------------------------:|
| 0 | 18.0 |         8 |        307.0 |      130.0 |  3504. |         12.0 |         70 |      1 | chevrolet chevelle malibu |
| 1 | 15.0 |         8 |        350.0 |      165.0 |  3693. |         11.5 |         70 |      1 |         buick skylark 320 |
| 2 | 18.0 |         8 |        318.0 |      150.0 |  3436. |         11.0 |         70 |      1 |        plymouth satellite |
| 3 | 16.0 |         8 |        304.0 |      150.0 |  3433. |         12.0 |         70 |      1 |             amc rebel sst |
| 4 | 17.0 |         8 |        302.0 |      140.0 |  3449. |         10.5 |         70 |      1 |               ford torino |


Let do some more Preprocessing Stuff with our DataFrame, lets use the **describe()** function to obtain some statistics of the dataframe.

```python
data.describe()
```


Output:

|        |  MPG | Cylinders | Displacement | Horsepower | Weight | Acceleration | Model Year | Origin |   Car Name |
|-------:|-----:|----------:|-------------:|-----------:|-------:|-------------:|-----------:|-------:|-----------:|
|  count |  398 |       398 |          398 |        392 |    398 |          398 |        398 |    398 |        398 |
| unique |  129 |         5 |           82 |         93 |    351 |           96 |         13 |      3 |        305 |
|    top | 13.0 |         4 |        97.00 |      150.0 |  1985. |         14.5 |         73 |      1 | ford pinto |
|   freq |   20 |       204 |           21 |         22 |      4 |           23 |         40 |    249 |          6 |



Looking at the table above generated from the describe() function we can see that there most be missing values from the "Horsepower" Column since the **count** for every single other Column is at 398 while the Horsepower column only has 392.

Lets take a extra look at the **Horsepower** Column to see the missing values and handle them.

```python
missing_index = list(data[data['Horsepower'].isnull()].index)
missing_index
```

Output:

Heres a list of the indexes in which the Horsepower value is missing:
```python
[32, 126, 330, 336, 354, 374]
```
Lets locate the missing **Horsepower** rows!

```python
data.loc[missing_index]
```
Output:

|     |  MPG | Cylinders | Displacement | Horsepower | Weight | Acceleration | Model Year | Origin |             Car Name |
|----:|-----:|----------:|-------------:|-----------:|-------:|-------------:|-----------:|-------:|---------------------:|
|  32 | 25.0 |         4 |        98.00 |       None |  2046. |         19.0 |         71 |      1 |           ford pinto |
| 126 | 21.0 |         6 |        200.0 |       None |  2875. |         17.0 |         74 |      1 |        ford maverick |
| 330 | 40.9 |         4 |        85.00 |       None |  1835. |         17.3 |         80 |      2 | renault lecar deluxe |
| 336 | 23.6 |         4 |        140.0 |       None |  2905. |         14.3 |         80 |      1 |   ford mustang cobra |
| 354 | 34.5 |         4 |        100.0 |       None |  2320. |         15.8 |         81 |      2 |          renault 18i |
| 374 | 23.0 |         4 |        151.0 |       None |  3035. |         20.5 |         82 |      1 |        amc concord d |


What should we fill the missing values with? We could take the median values of all the other vehicles horsepower and use that as the Horsepower values.

```python
median = data['Horsepower'].median()
median
```

Output:

```python
93.5
```

Lets not update all the *none* values in our table set equal to the median value of 93.5

```python
data['Horsepower'] = data["Horsepower"].fillna(data["Horsepower"].median())
```

Let's check those missing index's again

```python
data.loc[missing_index]
```

Output:

|     |  MPG | Cylinders | Displacement | Horsepower | Weight | Acceleration | Model Year | Origin |             Car Name |
|----:|-----:|----------:|-------------:|-----------:|-------:|-------------:|-----------:|-------:|---------------------:|
|  32 | 25.0 |         4 |        98.00 |       93.5 |  2046. |         19.0 |         71 |      1 |           ford pinto |
| 126 | 21.0 |         6 |        200.0 |       93.5 |  2875. |         17.0 |         74 |      1 |        ford maverick |
| 330 | 40.9 |         4 |        85.00 |       93.5 |  1835. |         17.3 |         80 |      2 | renault lecar deluxe |
| 336 | 23.6 |         4 |        140.0 |       93.5 |  2905. |         14.3 |         80 |      1 |   ford mustang cobra |
| 354 | 34.5 |         4 |        100.0 |       93.5 |  2320. |         15.8 |         81 |      2 |          renault 18i |
| 374 | 23.0 |         4 |        151.0 |       93.5 |  3035. |         20.5 |         82 |      1 |       amc concord dl |

Awesome, we have successfully cleaned the missing data!


Now lets create a new DataFream object containing different cars and then take a random samplings from it!

```python
data["Car Name]
```

Output:

```python
0      chevrolet chevelle malibu
1              buick skylark 320
2             plymouth satellite
3                  amc rebel sst
4                    ford torino
                 ...            
393              ford mustang gl
394                    vw pickup
395                dodge rampage
396                  ford ranger
397                   chevy s-10
Name: Car Name, Length: 398, dtype: object
```

Let pick a *toyota corolla*!

```python
data_frame_2 = data[(data["Car Name"] =="toyota corolla")]
data_frame_2.describe()
```

Output:

|        |  MPG | Cylinders | Displacement | Horsepower | Weight | Acceleration | Model Year | Origin |       Car Name |
|-------:|-----:|----------:|-------------:|-----------:|-------:|-------------:|-----------:|-------:|---------------:|
|  count |    5 |         5 |            5 |          5 |      5 |            5 |          5 |      5 |              5 |
| unique |    5 |         1 |            2 |          2 |      5 |            5 |          5 |      1 |              1 |
|    top | 32.2 |         4 |        108.0 |      75.00 |   2245 |         16.9 |         75 |      3 | toyota corolla |
|   freq |    1 |         5 |            3 |          4 |      1 |            1 |          1 |      5 |              5 |


Now lets add another Car to the new DataFrame! This time lets pick the Chevy Impala

```python
data_frame_2 = data_frame_2.append(data[(data["Car Name"] =="chevrolet impala")])
data_frame_2
```

Output:

|     |  MPG | Cylinders | Displacement | Horsepower | Weight | Acceleration | Model Year | Origin |         Car Name |
|----:|-----:|----------:|-------------:|-----------:|-------:|-------------:|-----------:|-------:|-----------------:|
| 167 | 29.0 |         4 |        97.00 |      75.00 |  2171. |         16.0 |         75 |      3 |   toyota corolla |
| 205 | 28.0 |         4 |        97.00 |      75.00 |  2155. |         16.4 |         76 |      3 |   toyota corolla |
| 321 | 32.2 |         4 |        108.0 |      75.00 |  2265. |         15.2 |         80 |      3 |   toyota corolla |
| 356 | 32.4 |         4 |        108.0 |      75.00 |  2350. |         16.8 |         81 |      3 |   toyota corolla |
| 382 | 34.0 |         4 |        108.0 |      70.00 |   2245 |         16.9 |         82 |      3 |   toyota corolla |
|   6 | 14.0 |         8 |        454.0 |      220.0 |  4354. |          9.0 |         70 |      1 | chevrolet impala |
|  38 | 14.0 |         8 |        350.0 |      165.0 |  4209. |         12.0 |         71 |      1 | chevrolet impala |
|  62 | 13.0 |         8 |        350.0 |      165.0 |  4274. |         12.0 |         72 |      1 | chevrolet impala |
| 103 | 11.0 |         8 |        400.0 |      150.0 |  4997. |         14.0 |         73 |      1 | chevrolet impala |


Maybe lets add another Car to our DataFrame! (Ford Ranger)


```python
data_frame_2 = data_frame_2.append(data[(data["Car Name"] =="ford ranger")])
data_frame_2
```

Output:

|     |  MPG | Cylinders | Displacement | Horsepower | Weight | Acceleration | Model Year | Origin |         Car Name |
|----:|-----:|----------:|-------------:|-----------:|-------:|-------------:|-----------:|-------:|-----------------:|
| 167 | 29.0 |         4 |        97.00 |      75.00 |  2171. |         16.0 |         75 |      3 |   toyota corolla |
| 205 | 28.0 |         4 |        97.00 |      75.00 |  2155. |         16.4 |         76 |      3 |   toyota corolla |
| 321 | 32.2 |         4 |        108.0 |      75.00 |  2265. |         15.2 |         80 |      3 |   toyota corolla |
| 356 | 32.4 |         4 |        108.0 |      75.00 |  2350. |         16.8 |         81 |      3 |   toyota corolla |
| 382 | 34.0 |         4 |        108.0 |      70.00 |   2245 |         16.9 |         82 |      3 |   toyota corolla |
|   6 | 14.0 |         8 |        454.0 |      220.0 |  4354. |          9.0 |         70 |      1 | chevrolet impala |
|  38 | 14.0 |         8 |        350.0 |      165.0 |  4209. |         12.0 |         71 |      1 | chevrolet impala |
|  62 | 13.0 |         8 |        350.0 |      165.0 |  4274. |         12.0 |         72 |      1 | chevrolet impala |
| 103 | 11.0 |         8 |        400.0 |      150.0 |  4997. |         14.0 |         73 |      1 | chevrolet impala |
|   6 | 14.0 |         8 |        454.0 |      220.0 |  4354. |          9.0 |         70 |      1 | chevrolet impala |
|  38 | 14.0 |         8 |        350.0 |      165.0 |  4209. |         12.0 |         71 |      1 | chevrolet impala |
|  62 | 13.0 |         8 |        350.0 |      165.0 |  4274. |         12.0 |         72 |      1 | chevrolet impala |
| 103 | 11.0 |         8 |        400.0 |      150.0 |  4997. |         14.0 |         73 |      1 | chevrolet impala |
| 396 | 28.0 |         4 |        120.0 |      79.00 |  2625. |         18.6 |         82 |      1 |      ford ranger |



Now lets take 3 different Random Samples of size 5 from our New DataFrame.

Sample 1: *Sampling without replacement*

```python
sample1 = data_frame_2.sample(n = 5, replace = False, random_state = 1)
sample1
```
Output:

|     |  MPG | Cylinders | Displacement | Horsepower | Weight | Acceleration | Model Year | Origin |         Car Name |
|----:|-----:|----------:|-------------:|-----------:|-------:|-------------:|-----------:|-------:|-----------------:|
| 356 | 32.4 |         4 |        108.0 |      75.00 |  2350. |         16.8 |         81 |      3 |   toyota corolla |
|  62 | 13.0 |         8 |        350.0 |      165.0 |  4274. |         12.0 |         72 |      1 | chevrolet impala |
|  38 | 14.0 |         8 |        350.0 |      165.0 |  4209. |         12.0 |         71 |      1 | chevrolet impala |
| 321 | 32.2 |         4 |        108.0 |      75.00 |  2265. |         15.2 |         80 |      3 |   toyota corolla |
|  38 | 14.0 |         8 |        350.0 |      165.0 |  4209. |         12.0 |         71 |      1 | chevrolet impala |


Sample 2: *sampling with replacement*


```python
sample2 = data_frame_2.sample(n = 5, replace = True, random_state = 1)
sample2
```

Output:

|     |  MPG | Cylinders | Displacement | Horsepower | Weight | Acceleration | Model Year | Origin |         Car Name |
|----:|-----:|----------:|-------------:|-----------:|-------:|-------------:|-----------:|-------:|-----------------:|
|   6 | 14.0 |         8 |        454.0 |      220.0 |  4354. |          9.0 |         70 |      1 | chevrolet impala |
|  62 | 13.0 |         8 |        350.0 |      165.0 |  4274. |         12.0 |         72 |      1 | chevrolet impala |
| 103 | 11.0 |         8 |        400.0 |      150.0 |  4997. |         14.0 |         73 |      1 | chevrolet impala |
| 103 | 11.0 |         8 |        400.0 |      150.0 |  4997. |         14.0 |         73 |      1 | chevrolet impala |
|   6 | 14.0 |         8 |        454.0 |      220.0 |  4354. |          9.0 |         70 |      1 | chevrolet impala |


Sample 3: *Sample via stratified, where each strata corresponds to number of cylinders of the car (column 2)*

```python
sample3 = data_frame_2[data_frame_2["Car Name"] == "toyota corolla"].sample( n = 2, random_state = 1)  
sample3 = sample3.append(data_frame_2[data_frame_2["Car Name"] == "toyota corolla"].sample(n = 2, random_state = 1 ))

sample3
```


Output:


|     |  MPG | Cylinders | Displacement | Horsepower | Weight | Acceleration | Model Year | Origin |       Car Name |
|----:|-----:|----------:|-------------:|-----------:|-------:|-------------:|-----------:|-------:|---------------:|
| 321 | 32.2 |         4 |        108.0 |      75.00 |  2265. |         15.2 |         80 |      3 | toyota corolla |
| 205 | 28.0 |         4 |        97.00 |      75.00 |  2155. |         16.4 |         76 |      3 | toyota corolla |
| 321 | 32.2 |         4 |        108.0 |      75.00 |  2265. |         15.2 |         80 |      3 | toyota corolla |
| 205 | 28.0 |         4 |        97.00 |      75.00 |  2155. |         16.4 |         76 |      3 | toyota corolla |



Lets apply different Discretization methods to the **MPG** attribute

```python
bins = pd.cut(data["MPG"].astype(float), 5)
bins
```

Output:
```python
0      (16.52, 24.04]
1      (8.962, 16.52]
2      (16.52, 24.04]
3      (8.962, 16.52]
4      (16.52, 24.04]
            ...      
393    (24.04, 31.56]
394     (39.08, 46.6]
395    (31.56, 39.08]
396    (24.04, 31.56]
397    (24.04, 31.56]
Name: MPG, Length: 398, dtype: category
Categories (5, interval[float64]): [(8.962, 16.52] < (16.52, 24.04] < (24.04, 31.56] < (31.56, 39.08] < (39.08, 46.6]]
```

```python
bins = pd.qcut(data["MPG"].astype(float), [0, 0.2, 0.4, 0.6, 0.8, 1.0])
bins.head()
```

Output:

```python
0     (16.0, 20.0]
1    (8.999, 16.0]
2     (16.0, 20.0]
3    (8.999, 16.0]
4     (16.0, 20.0]
Name: MPG, dtype: category
Categories (5, interval[float64]): [(8.999, 16.0] < (16.0, 20.0] < (20.0, 25.0] < (25.0, 31.0] < (31.0, 46.6]]
```

### More Preprocessing Exercises

Lets load the same DataFrame we had in the Car Example again.


```python
import pandas as pd
import re

column_names = ['MPG','Cylinders','Displacement','Horsepower','Weight','Acceleration','Model Year','Origin','Car Name']


def load_data(row):
    
    reg = '\s+' # this splits by 'spaces'
    print("row: ", row)
    fields = pd.Series([None if x == '?' else x for x in re.split(reg, row)])
    return fields


temp_data = pd.read_csv("auto-mpg.data", sep = '\t', header = None)

data = pd.DataFrame(temp_data[0].apply(load_data))

data.columns = column_names[:8]

data[column_names[8]] = temp_data[1]

## lets fill in the Horsepower missing values
data = data.fillna(data.median())

data.head()
```


Output:

|   |  MPG | Cylinders | Displacement | Horsepower | Weight | Acceleration | Model Year | Origin |                  Car Name |
|--:|-----:|----------:|-------------:|-----------:|-------:|-------------:|-----------:|-------:|--------------------------:|
| 0 | 18.0 |         8 |        307.0 |      130.0 |  3504. |         12.0 |         70 |      1 | chevrolet chevelle malibu |
| 1 | 15.0 |         8 |        350.0 |      165.0 |  3693. |         11.5 |         70 |      1 |         buick skylark 320 |
| 2 | 18.0 |         8 |        318.0 |      150.0 |  3436. |         11.0 |         70 |      1 |        plymouth satellite |
| 3 | 16.0 |         8 |        304.0 |      150.0 |  3433. |         12.0 |         70 |      1 |             amc rebel sst |
| 4 | 17.0 |         8 |        302.0 |      140.0 |  3449. |         10.5 |         70 |      1 |               ford torino |


Ok perfect now, lets work with it!

Lets Drop the *Car Name* column from the DataFrame *data* and then calculate the correlation for all the columns.

```python
data = data.drop('Car Name', 1)
corr = data.astype('float').corr() 
corr
```

Output:

|              |       MPG | Cylinders | Displacement | Horsepower |    Weight | Acceleration | Model Year |    Origin |
|-------------:|----------:|----------:|-------------:|-----------:|----------:|-------------:|-----------:|----------:|
|          MPG |  1.000000 | -0.775396 |    -0.804203 |  -0.773453 | -0.831741 |     0.420289 |   0.579267 |  0.563450 |
|    Cylinders | -0.775396 |  1.000000 |     0.950721 |   0.841284 |  0.896017 |    -0.505419 |  -0.348746 | -0.562543 |
| Displacement | -0.804203 |  0.950721 |     1.000000 |   0.895778 |  0.932824 |    -0.543684 |  -0.370164 | -0.609409 |
|   Horsepower | -0.773453 |  0.841284 |     0.895778 |   1.000000 |  0.862442 |    -0.686590 |  -0.413733 | -0.452096 |
|       Weight | -0.831741 |  0.896017 |     0.932824 |   0.862442 |  1.000000 |    -0.417457 |  -0.306564 | -0.581024 |
| Acceleration |  0.420289 | -0.505419 |    -0.543684 |  -0.686590 | -0.417457 |     1.000000 |   0.288137 |  0.205873 |
|   Model Year |  0.579267 | -0.348746 |    -0.370164 |  -0.413733 | -0.306564 |     0.288137 |   1.000000 |  0.180662 |
|       Origin |  0.563450 | -0.562543 |    -0.609409 |  -0.452096 | -0.581024 |     0.205873 |   0.180662 | 1.000     |


Now lets Apply **Principle Component Analysis** to reduce the data to 2-dimensions.

```python
from sklearn.decomposition import PCA
    
pca = PCA(n_components=2)
pca.fit(data.values)

projected = pca.transform(data)
projected = pd.DataFrame(projected,columns=['pc1','pc2'], index=data.index)

projected.head()
```

Output:

|   |        pc1 |       pc2 |
|--:|-----------:|----------:|
| 0 | 543.692090 | 51.046890 |
| 1 | 737.597223 | 79.416262 |
| 2 | 478.223494 | 75.668525 |
| 3 | 473.659818 | 62.795232 |
| 4 | 488.921154 | 56.018148 |


Now that we've done that, we can now use matplotlub to draw a horizontal bar plot to display the contribution of each attribute to the first two principal components.

```python
import matplotlib.pyplot as plt
from pandas import Series
%matplotlib inline

comp = pd.DataFrame(pca.components_, columns=data.columns, index=['pc1','pc2'])
comp

fig,axes = plt.subplots(2,1,sharex=True)
comp.loc['pc1'].plot(kind='barh',ax=axes[0],color='k',alpha=0.7)
axes[0].set_title('1st PC', size = 'x-large')
comp.loc['pc2'].plot(kind='barh',ax=axes[1],color='k',alpha=0.7)
axes[1].set_title('2nd PC', size = 'x-large')
```

Output:

!["insert image"](/images/big_data/pc_graph.png)


Now that we have this graphed, lets draw a 2-Dimensional Scatter Plot of the data points along their first two principal components

```python
projected.plot(kind='scatter',x='pc1',y='pc2', color = 'Green')
```

Output:

!["insert image"](/images/big_data/scatter_.png)


