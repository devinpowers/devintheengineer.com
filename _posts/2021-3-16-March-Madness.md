---
title: 'March Madness Prediction '

date: 2021-3-16

---

Lets predict who will win in the tournament....


![insert image](/images/big_data/msu.jpg)


I found some datasets of NCAA from kaggle -->


```python
import matplotlib.pyplot as plt
import matplotlib
import pandas as pd
import numpy as np 
```

Lets open the data set


```python
data = pd.read_csv('cbb.csv',header="infer")
```

```python
data.head()
```

Output:


|   	|           TEAM 	| CONF 	|  G 	|  W 	| ADJOE 	| ADJDE 	| BARTHAG 	| EFG_O 	| EFG_D 	|  TOR 	| FTRD 	| 2P_O 	| 2P_D 	| 3P_O 	| 3P_D 	| ADJ_T 	|  WAB 	| POSTSEASON 	| SEED 	| YEAR 	|
|--:	|---------------:	|-----:	|---:	|---:	|------:	|------:	|--------:	|------:	|------:	|-----:	|-----:	|-----:	|-----:	|-----:	|-----:	|------:	|-----:	|-----------:	|-----:	|-----:	|
| 0 	| North Carolina 	|  ACC 	| 40 	| 33 	| 123.3 	|  94.9 	|  0.9531 	|  52.6 	|  48.1 	| 15.4 	| 30.4 	| 53.9 	| 44.6 	| 32.7 	| 36.2 	|  71.7 	|  8.6 	|        2ND 	|  1.0 	| 2016 	|
| 1 	|      Wisconsin 	|  B10 	| 40 	| 36 	| 129.1 	|  93.6 	|  0.9758 	|  54.8 	|  47.7 	| 12.4 	| 22.4 	| 54.8 	| 44.7 	| 36.5 	| 37.5 	|  59.3 	| 11.3 	|        2ND 	|  1.0 	| 2015 	|
| 2 	|       Michigan 	|  B10 	| 40 	| 33 	| 114.4 	|  90.4 	|  0.9375 	|  53.9 	|  47.7 	| 14.0 	| 30.0 	| 54.7 	| 46.8 	| 35.2 	| 33.2 	|  65.9 	|  6.9 	|        2ND 	|  3.0 	| 2018 	|
| 3 	|     Texas Tech 	|  B12 	| 38 	| 31 	| 115.2 	|  85.2 	|  0.9696 	|  53.5 	|  43.0 	| 17.7 	| 36.6 	| 52.8 	| 41.9 	| 36.5 	| 29.7 	|  67.5 	|  7.0 	|        2ND 	|  3.0 	| 2019 	|
| 4 	|        Gonzaga 	|  WCC 	| 39 	| 37 	| 117.8 	|  86.3 	|  0.9728 	|  56.6 	|  41.1 	| 16.2 	| 26.9 	| 56.3 	| 40.0 	| 38.2 	| 29.0 	|  71.5 	|  7.7 	|        2ND 	|  1.0 	| 2017 	|





Lets drop all the teams that didn't make the tournement.
In the POSTSEASON Column teams that didnt make the tournemnt are left with a ??? marks so we can use dropna() to remove those rows.

```python
data = data.dropna()
```
Theres also teams that lost their "play-in game" lets drop them as well

The tournemnt is 64 games and 68 with the play in games, In the CSV file teams with the POSTSEASON = R68 didn't win their play-in games. So we can single those rows out!! Lets update our data below:

```python
data = data[data["POSTSEASON"] != 'R68']
data

```

Now we can update the rows in Postseason to reflect the number of games each team won during the tournemnt in the year.

From the CSV file:
    
- Champions = 6 games won (Won the tournment)
- 2ND = 5 games won (lost in the championship game)
- F4 = 4 Final Four
- E8 = 3 Elite Eight
- S16 = 2 Sweet Sixteen
- R32 = 1 Round of 32
- R64 =  0 Round of 64 the first round

We can use .replace and a dictionary to map/update the values to reflect the number of games won!!


```python
data = data.replace({
    
    'Champions': 6,
    '2ND': 5,
    'F4': 4,
    'E8': 3,
    'S16': 2,
    'R32': 1,
    'R64': 0
})
```

Sweet, now lets save that column as our predictor
```python
y = data["POSTSEASON"]
y
```

Now the question is... What columns should we keep and what columns should we remove??

- The number of games won in the regular reason will be different during our 2020-21 season since some teams werent able to play everyone, so I dont care about Games Played (record) and number of wins.

**Lets Drop these:**

**We can only take Numeric Values as well**
- TEAM = Team Name (Can Drop)
- CONF = Conference (Can Drop)
- G = Games Played (Can Drop)
- W = Number of Wins (Can Drop)
- YEAR = Year (Can drop)


**Lets use these:**
- ADJOE = Adjusted Offensive Efficiency
- ADJDE = Adjusted Defensive Efficiency
- BARTHAG = Power Ranking (Chance of beating average D1 Team)
- EFG% = Effective Field Goal
- EFGD% = Effective Field Goal Defensively
- TOR = Turnover rate
- TORD = Turnover rate defensively
- ORB = Offensive Rebounding
- DRB = Defensive Rebounding
- FTR = Free throw rate
- FTRD = Free throw rate defensively
- 2P_O = 2-point %
- 2P_D = 2-point % defensively
- 3P_O = 3-point %
- 3P_D = 3-point % defensively
- WAB = Wins above Bubble
- ADJ_T = Adjusted Tempo
- SEED = Seed in the tournment


Lets drop those columns:

```python
data = data.drop(columns = ["POSTSEASON", "TEAM","CONF","YEAR","G","W"])
```

Now lets normalize our data

In general, learning algorithms benefit from standardization of the data set.

Standardization of datasets is a common requirement for many machine learning estimators implemented in scikit-learn; they might behave badly if the individual features do not more or less look like standard normally distributed data: Gaussian with zero mean and unit variance.

In practice we often ignore the shape of the distribution and just transform the data to center it by removing the mean value of each feature, then scale it by dividing non-constant features by their standard deviation.

```python
data = ( data - data.mean())/data.std()

X = data

X
```

**Random Forest Classifier**

```python
from sklearn.ensemble import RandomForestClassifier, RandomForestRegressor

randTree = RandomForestRegressor(min_samples_split=20, random_state=5);
randTree.fit(X, y)
```


Now that we have our **Model** we can import a file from 2018 and use that as a test to see how accurate our model is!!

