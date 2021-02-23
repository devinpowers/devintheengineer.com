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
data.head()   

```

