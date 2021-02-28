---
title: 'Big Data Analysis Day 6: Data Preprocessing '

date: 2021-2-28

---

#### How do we **Transform raw data** into a more useful representation ?

- Data Cleaning
    * Noise, Outliers, Duplicate Data, Missing Values
- Aggregation
- Sampling
- Feature Extraction
- Discretization


#### Sampling

What is Sampling?

- Sampling is a technique use for **data reduction**
- There is different Types of Sampling

    * Simple Random Sampling
    * Stratified Sampling
    * Sampling without Replacement
    * Sample with Replacement



Python Examples:

```python
import pandas as p
data = p.read_csv('diabetes.csv', header= 0)
data[:5]
```
Output:
```python
	preg	plas	pres	skin	insu	mass	pedi	age	class
0	6	    148	    72	    35	    0	    33.6	0.627	50	tested_positive
1	1	    85  	66	    29  	0	    26.6	0.351	31	tested_negative
2	8	    183	    64	    0	    0	    23.3	0.672	32	tested_positive
3	1	    89	    66	    23	    94	    28.1	0.167	21	tested_negative
4	0	    137	    40	    35	    168	    43.1	2.288	33	tested_positive
```

Now we will use the **DataFrame.sample()** in Pandas, the sample method returns a **random sample** of items from our dataframe

**Parameters**

n = int -> Number of items from axis to return

frac = float -> Fraction of axis items to return

Other Parameters in the link below

[Pandas Documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sample.html)

```python
sample = data.sample(n = 5)
sample
```

Output:

```python

preg	plas	pres	skin	insu	mass	pedi	age	class
351	4	137	84	0	0	31.2	0.252	30	tested_negative
466	0	74	52	10	36	27.8	0.269	22	tested_negative
528	0	117	66	31	188	30.8	0.493	22	tested_negative
683	4	125	80	0	0	32.3	0.536	27	tested_positive
3	1	89	66	23	94	28.1	0.167	21	tested_negative
```