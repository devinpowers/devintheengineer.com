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

