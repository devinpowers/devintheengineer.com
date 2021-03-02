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

In this example, let *Buy* be the class attribute and were intrested in discretize the *Age* attribute

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

We can see that both approaches can produce intervals that contain non-homogeneous classes


**Using Supervised Discretization**


|              | Yes | No |
|--------------|-----|----|
| <16.5        | 0   | 2  |
| (16.5, 35.5) | 5   | 1  |
| > 35.5       | 0   | 4  |

We see that our goal is to ensure that each bin contains data points from *one class*



```python
import pandas as p
data = p.read_csv('buy.csv', header=0')
data
```

Output:
```python
	age	membershipYears	numberOfFriends	AmountSpent	NumPurchases
0	21	        2	        5	        100	        2
1	38      	0	        10	        10      	1
2	18	        0	        5	        25      	1
3	19	        5	        30      	1000	    25
4	24      	0	        2	        50          3
5	29	        2	        20	        200	        7
6	30	        4	        5	        1500	    15
7	31      	2	        70	        150	        5
8	40      	0	        11	        70	        4
9	44	        0	        8	        10	        1
10	55      	1	        2	        80	        3
11	64	        1	        0	        30	        1
```

```python
data.corr()
```

Output:
```python
	                    age	    membershipYears	numberOfFriends	AmountSpent	NumPurchases
age             	1.000000	-0.334731	-0.253233	        -0.303731	-0.393919
membershipYears	    -0.334731	1.000000	0.343459	        0.851307	0.900591
numberOfFriends 	-0.253233	0.343459	1.000000	        0.085086	0.288885
AmountSpent	        -0.303731	0.851307	0.085086	        1.000000	0.853188
NumPurchases	    -0.393919	0.900591	0.288885	        0.853188	1.000000
```


**Entropy-based Discretization**

- A very common **Supervised Discretization method**
- Entropy is a measure of **impurity** (randomness in a set) 
- Measure of Disorder
    * Measured from range of 0 to 1
    * Higher entropy implies data points are from a large number of classes (heterogeneous)
    * Lower entropy implies most of the data points are from the same class 


!["insert image"](/images/big_data/entropy.png)



### Feature Selection Example


```python
import pandas as p
data = p.read_csv('buy.csv', header=0)
data
```


Output:
```python
	    age 	membershipYears	numberOfFriends	AmountSpent	NumPurchases
0	    21	        2           	 5	            100     	2
1	    38      	0	            10          	10	        1
2	    18      	0	            5	            25      	1
3	    19      	5	            30	            1000	    25
4	    24      	0	            2	            50      	3
5	    29	        2	            20	            200	        7
6	    30	        4	            5	            1500	    15
7	    31	        2	            70          	150	        5
8	    40         	0	            11	            70	        4
9	    44	        0	            8	            10  	    1
10	    55      	1	            2	            80      	3
11  	64      	1	            0	            30	        1
```

```python
data.corr()
```

Output:

```python
	                    age	membershipYears	numberOfFriends	AmountSpent	NumPurchases
age	                1.000000	-0.334731	-0.253233	-0.303731	-0.393919
membershipYears 	-0.334731	1.000000	0.343459	0.851307	0.900591
numberOfFriends	    -0.253233	0.343459	1.000000	0.085086	0.288885
AmountSpent     	-0.303731	0.851307	0.085086	1.000000	0.853188
NumPurchases	    -0.393919	0.900591	0.288885	0.853188	1.000000
```


### Principle Component Analysis

- very common approach for feature extraction

- Goald is to construct a new set of dimensions (attributes) that better captures the variability of the data
