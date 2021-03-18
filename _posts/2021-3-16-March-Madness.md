---
title: 'March Madness Prediction '

date: 2021-3-16

tags:
    - Machine Learning

header:

  image: "/images/magic.jpeg"

toc: true
toc_label: "Table of Contents" 
---

Lets predict who will th 2021 NCCA Basketball Tournament


![insert image](/images/big_data/March/msu.jpg)

kidding.....maybe..i wish



I found a College Basketball Dataset (2013 - 2021 seasons on Kaggle) for their annual challenge.

[Link to College Basketball Dataset](https://www.kaggle.com/andrewsundberg/college-basketball-dataset)



```python
import matplotlib.pyplot as plt
import matplotlib
import pandas as pd
import numpy as np 
```

Lets open the data set


```python

column_names = ["Team", "Conference", "Games Played","Games Won",
          "Adjusted Offensive Efficiency", "Adjusted Defensive Efficiency",
          "Power Ranking", "Effective Field Goal %","Effective Field Goal % (D)",
          "Turnover %", "Turnover % (D)", "Offensive Rebounds", "Defensive Rebounds",
          "Free Throw Rate", "Free Throw Rate (D)", "2-PT%", "2-PT% (D)",
          "3-PT%", "3-PT (D)", "Adjusted Tempo", "Wins above Bubble", "Postseason","Seed in Tournament", "Year"]

data = pd.read_csv("cbb.csv", header = None, names = column_names, skiprows = 1)
data
```

```python
data.head()
```

Output:


|   	|           Team 	| Conference 	| Games Played 	| Games Won 	| Adjusted Offensive Efficiency 	| Adjusted Defensive Efficiency 	| Power Ranking 	| Effective Field Goal % 	| Effective Field Goal % (D) 	| Turnover % 	| ... 	| Free Throw Rate (D) 	| 2-PT% 	| 2-PT% (D) 	| 3-PT% 	| 3-PT (D) 	| Adjusted Tempo 	| Wins above Bubble 	| Postseason 	| Seed in Tournament 	| Year 	|
|--:	|---------------:	|-----------:	|-------------:	|-----------:	|------------------------------:	|------------------------------:	|--------------:	|-----------------------:	|---------------------------:	|-----------:	|----:	|--------------------:	|------:	|----------:	|------:	|---------:	|---------------:	|------------------:	|-----------:	|-------------------:	|-----:	|
| 0 	| North Carolina 	|        ACC 	|           40 	|         33 	|                         123.3 	|                          94.9 	|        0.9531 	|                   52.6 	|                       48.1 	|       15.4 	| ... 	|                30.4 	|  53.9 	|      44.6 	|  32.7 	|     36.2 	|           71.7 	|               8.6 	|        2ND 	|                1.0 	| 2016 	|
| 1 	|      Wisconsin 	|        B10 	|           40 	|         36 	|                         129.1 	|                          93.6 	|        0.9758 	|                   54.8 	|                       47.7 	|       12.4 	| ... 	|                22.4 	|  54.8 	|      44.7 	|  36.5 	|     37.5 	|           59.3 	|              11.3 	|        2ND 	|                1.0 	| 2015 	|
| 2 	|       Michigan 	|        B10 	|           40 	|         33 	|                         114.4 	|                          90.4 	|        0.9375 	|                   53.9 	|                       47.7 	|       14.0 	| ... 	|                30.0 	|  54.7 	|      46.8 	|  35.2 	|     33.2 	|           65.9 	|               6.9 	|        2ND 	|                3.0 	| 2018 	|
| 3 	|     Texas Tech 	|        B12 	|           38 	|         31 	|                         115.2 	|                          85.2 	|        0.9696 	|                   53.5 	|                       43.0 	|       17.7 	| ... 	|                36.6 	|  52.8 	|      41.9 	|  36.5 	|     29.7 	|           67.5 	|               7.0 	|        2ND 	|                3.0 	| 2019 	|
| 4 	|        Gonzaga 	|        WCC 	|           39 	|         37 	|                         117.8 	|                          86.3 	|        0.9728 	|                   56.6 	|                       41.1 	|       16.2 	| ... 	|                26.9 	|  56.3 	|      40.0 	|  38.2 	|     29.0 	|           71.5 	|               7.7 	|        2ND 	|                1.0 	| 2017 	|




## Cleaning the Data

Lets **drop all the teams that didn't make the tournement.**

In the **Postseason** Column teams that didnt make the tournemnt are read as a ??? marks (meaning missing) in the csv so we can use **dropna()** to remove those empty/missing rows.

```python
data = data.dropna()
```
Theres also teams that lost their "play-in game" lets drop them as well

The tournemnt is 64 games and 68 with the play in games, In the CSV file teams with the Postseason = R68 didn't win their play-in games. So we can single those rows out!! Lets update our data below:

```python
data = data[data["Postseason"] != 'R68']
data

```

Output:

|      	|               Team 	| Conference 	| Games Played 	| Games Won 	| Adjusted Offensive Efficiency 	| Adjusted Defensive Efficiency 	| Power Ranking 	| Effective Field Goal % 	| Effective Field Goal % (D) 	| Turnover % 	| ... 	| Free Throw Rate (D) 	| 2-PT% 	| 2-PT% (D) 	| 3-PT% 	| 3-PT (D) 	| Adjusted Tempo 	| Wins above Bubble 	| Postseason 	| Seed in Tournament 	| Year 	|
|-----:	|-------------------:	|-----------:	|-------------:	|----------:	|------------------------------:	|------------------------------:	|--------------:	|-----------------------:	|---------------------------:	|-----------:	|----:	|--------------------:	|------:	|----------:	|------:	|---------:	|---------------:	|------------------:	|-----------:	|-------------------:	|-----:	|
|    0 	|     North Carolina 	|        ACC 	|           40 	|        33 	|                         123.3 	|                          94.9 	|        0.9531 	|                   52.6 	|                       48.1 	|       15.4 	| ... 	|                30.4 	|  53.9 	|      44.6 	|  32.7 	|     36.2 	|           71.7 	|               8.6 	|        2ND 	|                1.0 	| 2016 	|
|    1 	|          Wisconsin 	|        B10 	|           40 	|        36 	|                         129.1 	|                          93.6 	|        0.9758 	|                   54.8 	|                       47.7 	|       12.4 	| ... 	|                22.4 	|  54.8 	|      44.7 	|  36.5 	|     37.5 	|           59.3 	|              11.3 	|        2ND 	|                1.0 	| 2015 	|
|    2 	|           Michigan 	|        B10 	|           40 	|        33 	|                         114.4 	|                          90.4 	|        0.9375 	|                   53.9 	|                       47.7 	|       14.0 	| ... 	|                30.0 	|  54.7 	|      46.8 	|  35.2 	|     33.2 	|           65.9 	|               6.9 	|        2ND 	|                3.0 	| 2018 	|
|    3 	|         Texas Tech 	|        B12 	|           38 	|        31 	|                         115.2 	|                          85.2 	|        0.9696 	|                   53.5 	|                       43.0 	|       17.7 	| ... 	|                36.6 	|  52.8 	|      41.9 	|  36.5 	|     29.7 	|           67.5 	|               7.0 	|        2ND 	|                3.0 	| 2019 	|
|    4 	|            Gonzaga 	|        WCC 	|           39 	|        37 	|                         117.8 	|                          86.3 	|        0.9728 	|                   56.6 	|                       41.1 	|       16.2 	| ... 	|                26.9 	|  56.3 	|      40.0 	|  38.2 	|     29.0 	|           71.5 	|               7.7 	|        2ND 	|                1.0 	| 2017 	|
|  ... 	|                ... 	|        ... 	|          ... 	|       ... 	|                           ... 	|                           ... 	|           ... 	|                    ... 	|                        ... 	|        ... 	| ... 	|                 ... 	|   ... 	|       ... 	|   ... 	|      ... 	|            ... 	|               ... 	|        ... 	|                ... 	|  ... 	|
| 2450 	|       Michigan St. 	|        B10 	|           35 	|        26 	|                         111.4 	|                          87.8 	|        0.9392 	|                   50.6 	|                       44.5 	|       20.8 	| ... 	|                32.4 	|  50.4 	|      44.3 	|  34.1 	|     30.1 	|           64.4 	|               6.7 	|        S16 	|                3.0 	| 2013 	|
| 2451 	|            Arizona 	|        P12 	|           35 	|        27 	|                         114.4 	|                          92.2 	|        0.9229 	|                   52.5 	|                       46.6 	|       19.5 	| ... 	|                32.9 	|  50.6 	|      43.4 	|  37.1 	|     35.8 	|           66.8 	|               4.6 	|        S16 	|                6.0 	| 2013 	|
| 2452 	|             Oregon 	|        P12 	|           37 	|        28 	|                         104.8 	|                          88.6 	|        0.8728 	|                   49.3 	|                       46.4 	|       21.4 	| ... 	|                33.3 	|  49.1 	|      44.9 	|  33.3 	|     33.4 	|           69.2 	|               2.9 	|        S16 	|               12.0 	| 2013 	|
| 2453 	|           La Salle 	|        A10 	|           34 	|        24 	|                         112.0 	|                          96.2 	|        0.8516 	|                   51.9 	|                       49.3 	|       17.1 	| ... 	|                28.5 	|  49.3 	|      50.6 	|  37.7 	|     30.2 	|           66.0 	|               0.3 	|        S16 	|               13.0 	| 2013 	|
| 2454 	| Florida Gulf Coast 	|       ASun 	|           35 	|        24 	|                         103.4 	|                          96.3 	|        0.6952 	|                   51.6 	|                       46.9 	|       21.0 	| ... 	|                32.7 	|  52.3 	|      46.9 	|  33.4 	|     31.3 	|           69.1 	|              -4.0 	|        S16 	|               15.0 	| 2013 	|

448 rows × 24 columns




Now we can update the rows in Postseason to reflect the number of games each team won during the tournemnt in the year, the number of games won will be our **Predictor** (y)!


From the CSV file rows in the Column **Postseason**
    
- Champions = 6 (Won the tournment)
- 2ND = 5 (lost in the championship game)
- F4 = 4 (Final Four)
- E8 = 3 (Elite Eight)
- S16 = 2 (Sweet Sixteen)
- R32 = 1 (Round of 32)
- R64 =  0 (Round of 64 the first round)

We can use .replace() and a dictionary to *map/update* the values to reflect the number of games won in each row!!


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

data
```

Output:

|      	|               Team 	| Conference 	| Games Played 	| Games Wons 	| Adjusted Offensive Efficiency 	| Adjusted Defensive Efficiency 	| Power Ranking 	| Effective Field Goal % 	| Effective Field Goal % (D) 	| Turnover % 	| ... 	| Free Throw Rate (D) 	| 2-PT% 	| 2-PT% (D) 	| 3-PT% 	| 3-PT (D) 	| Adjusted Tempo 	| Wins above Bubble 	| Postseason 	| Seed in Tournament 	| Year 	|
|-----:	|-------------------:	|-----------:	|-------------:	|-----------:	|------------------------------:	|------------------------------:	|--------------:	|-----------------------:	|---------------------------:	|-----------:	|----:	|--------------------:	|------:	|----------:	|------:	|---------:	|---------------:	|------------------:	|-----------:	|-------------------:	|-----:	|
|    0 	|     North Carolina 	|        ACC 	|           40 	|         33 	|                         123.3 	|                          94.9 	|        0.9531 	|                   52.6 	|                       48.1 	|       15.4 	| ... 	|                30.4 	|  53.9 	|      44.6 	|  32.7 	|     36.2 	|           71.7 	|               8.6 	|          5 	|                1.0 	| 2016 	|
|    1 	|          Wisconsin 	|        B10 	|           40 	|         36 	|                         129.1 	|                          93.6 	|        0.9758 	|                   54.8 	|                       47.7 	|       12.4 	| ... 	|                22.4 	|  54.8 	|      44.7 	|  36.5 	|     37.5 	|           59.3 	|              11.3 	|          5 	|                1.0 	| 2015 	|
|    2 	|           Michigan 	|        B10 	|           40 	|         33 	|                         114.4 	|                          90.4 	|        0.9375 	|                   53.9 	|                       47.7 	|       14.0 	| ... 	|                30.0 	|  54.7 	|      46.8 	|  35.2 	|     33.2 	|           65.9 	|               6.9 	|          5 	|                3.0 	| 2018 	|
|    3 	|         Texas Tech 	|        B12 	|           38 	|         31 	|                         115.2 	|                          85.2 	|        0.9696 	|                   53.5 	|                       43.0 	|       17.7 	| ... 	|                36.6 	|  52.8 	|      41.9 	|  36.5 	|     29.7 	|           67.5 	|               7.0 	|          5 	|                3.0 	| 2019 	|
|    4 	|            Gonzaga 	|        WCC 	|           39 	|         37 	|                         117.8 	|                          86.3 	|        0.9728 	|                   56.6 	|                       41.1 	|       16.2 	| ... 	|                26.9 	|  56.3 	|      40.0 	|  38.2 	|     29.0 	|           71.5 	|               7.7 	|          5 	|                1.0 	| 2017 	|
|  ... 	|                ... 	|        ... 	|          ... 	|        ... 	|                           ... 	|                           ... 	|           ... 	|                    ... 	|                        ... 	|        ... 	| ... 	|                 ... 	|   ... 	|       ... 	|   ... 	|      ... 	|            ... 	|               ... 	|        ... 	|                ... 	|  ... 	|
| 2450 	|       Michigan St. 	|        B10 	|           35 	|         26 	|                         111.4 	|                          87.8 	|        0.9392 	|                   50.6 	|                       44.5 	|       20.8 	| ... 	|                32.4 	|  50.4 	|      44.3 	|  34.1 	|     30.1 	|           64.4 	|               6.7 	|          2 	|                3.0 	| 2013 	|
| 2451 	|            Arizona 	|        P12 	|           35 	|         27 	|                         114.4 	|                          92.2 	|        0.9229 	|                   52.5 	|                       46.6 	|       19.5 	| ... 	|                32.9 	|  50.6 	|      43.4 	|  37.1 	|     35.8 	|           66.8 	|               4.6 	|          2 	|                6.0 	| 2013 	|
| 2452 	|             Oregon 	|        P12 	|           37 	|         28 	|                         104.8 	|                          88.6 	|        0.8728 	|                   49.3 	|                       46.4 	|       21.4 	| ... 	|                33.3 	|  49.1 	|      44.9 	|  33.3 	|     33.4 	|           69.2 	|               2.9 	|          2 	|               12.0 	| 2013 	|
| 2453 	|           La Salle 	|        A10 	|           34 	|         24 	|                         112.0 	|                          96.2 	|        0.8516 	|                   51.9 	|                       49.3 	|       17.1 	| ... 	|                28.5 	|  49.3 	|      50.6 	|  37.7 	|     30.2 	|           66.0 	|               0.3 	|          2 	|               13.0 	| 2013 	|
| 2454 	| Florida Gulf Coast 	|       ASun 	|           35 	|         24 	|                         103.4 	|                          96.3 	|        0.6952 	|                   51.6 	|                       46.9 	|       21.0 	| ... 	|                32.7 	|  52.3 	|      46.9 	|  33.4 	|     31.3 	|           69.1 	|              -4.0 	|          2 	|               15.0 	| 2013 	|


448 rows × 24 columns



Sweet, now lets save that column as our **Predictor (y)**

```python
y = data["Postseason"]
y
```

Output:

| Index                                       	| Postseason (Number of Wins) 	|
|---------------------------------------------	|-----------------------------	|
| 0                                           	| 5                           	|
| 1                                           	| 5                           	|
| 2                                           	| 5                           	|
| 3                                           	| 5                           	|
| 4                                           	| 5                           	|
| ..                                          	|                             	|
| 2450                                        	| 2                           	|
| 2451                                        	| 2                           	|
| 2452                                        	| 2                           	|
| 2453                                        	| 2                           	|
| 2454                                        	| 2                           	|
| Name: Postseason, Length: 448, dtype: int64 	|                             	|




## Selecting the Feature Columns

**Now the question is... What columns should we keep and what columns should we remove??**

- The number of games won in the regular reason will be different during our 2020-21 season since some teams werent able to play everyone, so I dont care about Games Played (record) and number of wins.

**Lets Drop these:**

**We can only take Numeric Values as well**

- Team : Not Numeric Value (Can Drop)
- Conference : Not Numeric Value (Can Drop)
- Games Played : (Can Drop)
- Games Won : (Can Drop)
- Year : (Can drop)


**Lets use these:**

Note that the (D) stands for Defensively

- Adjusted Offensive Efficiency
- Adjusted Defensive Efficiency
- Power Ranking : Odds of Beating a average D1 Team
- Effective Field Goal %
- Effective Field Goal % (D)
- Turnover %
- Turnover % (D)
- Offensive Rebounds
- Defensive Rebounds
- Free Throw Rate
- Free Throw Rate (D)
- 2-PT%
- 2-PT% (D)
- 3-PT%
- 3-PT (D)
- Adjusted Tempo
- Wins above Bubble
- Postseason
- Seed in Tournament



Lets **drop** those columns:

```python
data = data.drop(columns = ["Postseason", "Team","Conference","Year","Games Played","Games Won"])
data.head()
```

Output:

|   	| Adjusted Offensive Efficiency 	| Adjusted Defensive Efficiency 	| Power Ranking 	| Effective Field Goal % 	| Effective Field Goal % (D) 	| Turnover % 	| Turnover % (D) 	| Offensive Rebounds 	| Defensive Rebounds 	| Free Throw Rate 	| Free Throw Rate (D) 	| 2-PT% 	| 2-PT% (D) 	| 3-PT% 	| 3-PT (D) 	| Adjusted Tempo 	| Wins above Bubble 	| Seed in Tournament 	|
|--:	|------------------------------:	|------------------------------:	|--------------:	|-----------------------:	|---------------------------:	|-----------:	|---------------:	|-------------------:	|-------------------:	|----------------:	|--------------------:	|------:	|----------:	|------:	|---------:	|---------------:	|------------------:	|-------------------:	|
| 0 	|                         123.3 	|                          94.9 	|        0.9531 	|                   52.6 	|                       48.1 	|       15.4 	|           18.2 	|               40.7 	|               30.0 	|            32.3 	|                30.4 	|  53.9 	|      44.6 	|  32.7 	|     36.2 	|           71.7 	|               8.6 	|                1.0 	|
| 1 	|                         129.1 	|                          93.6 	|        0.9758 	|                   54.8 	|                       47.7 	|       12.4 	|           15.8 	|               32.1 	|               23.7 	|            36.2 	|                22.4 	|  54.8 	|      44.7 	|  36.5 	|     37.5 	|           59.3 	|              11.3 	|                1.0 	|
| 2 	|                         114.4 	|                          90.4 	|        0.9375 	|                   53.9 	|                       47.7 	|       14.0 	|           19.5 	|               25.5 	|               24.9 	|            30.7 	|                30.0 	|  54.7 	|      46.8 	|  35.2 	|     33.2 	|           65.9 	|               6.9 	|                3.0 	|
| 3 	|                         115.2 	|                          85.2 	|        0.9696 	|                   53.5 	|                       43.0 	|       17.7 	|           22.8 	|               27.4 	|               28.7 	|            32.9 	|                36.6 	|  52.8 	|      41.9 	|  36.5 	|     29.7 	|           67.5 	|               7.0 	|                3.0 	|
| 4 	|                         117.8 	|                          86.3 	|        0.9728 	|                   56.6 	|                       41.1 	|       16.2 	|           17.1 	|               30.0 	|               26.2 	|            39.0 	|                26.9 	|  56.3 	|      40.0 	|  38.2 	|     29.0 	|           71.5 	|               7.7 	|                1.0 	|




### Normalizing the Data

In general, learning algorithms benefit from standardization of the data set.

Standardization of datasets is a common requirement for many machine learning estimators implemented in scikit-learn; they might behave badly if the individual features do not more or less look like standard normally distributed data: Gaussian with zero mean and unit variance.

In practice we often ignore the shape of the distribution and just transform the data to center it by removing the mean value of each feature, then scale it by dividing non-constant features by their standard deviation.

```python
data = ( data - data.mean())/data.std()

X = data

X
```

Output:

|      	| Adjusted Offensive Efficiency 	| Adjusted Defensive Efficiency 	| Power Ranking 	| Effective Field Goal % 	| Effective Field Goal % (D) 	| Turnover % 	| Turnover % (D) 	| Offensive Rebounds 	| Defensive Rebounds 	| Free Throw Rate 	| Free Throw Rate (D) 	|     2-PT% 	| 2-PT% (D) 	|     3-PT% 	|  3-PT (D) 	| Adjusted Tempo 	| Wins above Bubble 	| Seed in Tournament 	|
|-----:	|------------------------------:	|------------------------------:	|--------------:	|-----------------------:	|---------------------------:	|-----------:	|---------------:	|-------------------:	|-------------------:	|----------------:	|--------------------:	|----------:	|----------:	|----------:	|----------:	|---------------:	|------------------:	|-------------------:	|
|    0 	|                      1.852712 	|                     -0.267905 	|      0.933216 	|               0.166623 	|                   0.210833 	|  -1.150197 	|      -0.353803 	|           2.097437 	|           0.366500 	|       -0.878417 	|           -0.499655 	|  0.910415 	| -0.629216 	| -1.279282 	|  1.461359 	|       1.292709 	|          1.432846 	|          -1.624281 	|
|    1 	|                      2.784428 	|                     -0.522727 	|      1.079968 	|               0.961125 	|                   0.044102 	|  -2.808673 	|      -1.365528 	|           0.067238 	|          -1.815799 	|       -0.154639 	|           -1.868845 	|  1.208926 	| -0.594961 	|  0.216083 	|  2.091614 	|      -2.540566 	|          2.000168 	|          -1.624281 	|
|    2 	|                      0.423009 	|                     -1.149982 	|      0.832365 	|               0.636102 	|                   0.044102 	|  -1.924153 	|       0.194215 	|          -1.490822 	|          -1.400123 	|       -1.175351 	|           -0.568114 	|  1.175758 	|  0.124406 	| -0.295489 	|  0.006926 	|      -0.500274 	|          1.075643 	|          -1.191268 	|
|    3 	|                      0.551521 	|                     -2.169272 	|      1.039886 	|               0.491647 	|                  -1.914991 	|   0.121301 	|       1.585337 	|          -1.042290 	|          -0.083816 	|       -0.767066 	|            0.561467 	|  0.545568 	| -1.554117 	|  0.216083 	| -1.689913 	|      -0.005658 	|          1.096655 	|          -1.191268 	|
|    4 	|                      0.969187 	|                     -1.953653 	|      1.060573 	|               1.611173 	|                  -2.706964 	|  -0.707937 	|      -0.817510 	|          -0.428509 	|          -0.949807 	|        0.364995 	|           -1.098675 	|  1.706445 	| -2.204972 	|  0.885062 	| -2.029281 	|       1.230882 	|          1.243738 	|          -1.624281 	|
|  ... 	|                           ... 	|                           ... 	|           ... 	|                    ... 	|                        ... 	|        ... 	|            ... 	|                ... 	|                ... 	|             ... 	|                 ... 	|       ... 	|       ... 	|       ... 	|       ... 	|            ... 	|               ... 	|                ... 	|
| 2450 	|                     -0.058914 	|                     -1.659627 	|      0.843355 	|              -0.555652 	|                  -1.289748 	|   1.835059 	|       0.067749 	|           1.011516 	|          -0.464852 	|       -0.080406 	|           -0.157357 	| -0.250462 	| -0.731983 	| -0.728358 	| -1.495989 	|      -0.963977 	|          1.033619 	|          -1.191268 	|
| 2451 	|                      0.423009 	|                     -0.797151 	|      0.737979 	|               0.130509 	|                  -0.414409 	|   1.116386 	|       0.320681 	|           0.751840 	|          -0.776609 	|        0.068061 	|           -0.071783 	| -0.184126 	| -1.040283 	|  0.452193 	|  1.267435 	|      -0.222053 	|          0.592368 	|          -0.541749 	|
| 2452 	|                     -1.119143 	|                     -1.502813 	|      0.414091 	|              -1.025131 	|                  -0.497775 	|   2.166754 	|       1.248095 	|           0.940695 	|          -0.603411 	|        0.253645 	|           -0.003324 	| -0.681645 	| -0.526450 	| -1.043171 	|  0.103888 	|       0.519871 	|          0.235165 	|           0.757289 	|
| 2453 	|                      0.037471 	|                     -0.013082 	|      0.277037 	|              -0.086173 	|                   0.711027 	|  -0.210394 	|       0.953009 	|          -0.664578 	|           1.821366 	|       -1.064000 	|           -0.824837 	| -0.615309 	|  1.426117 	|  0.688303 	| -1.447508 	|      -0.469361 	|         -0.311146 	|           0.973795 	|
| 2454 	|                     -1.344040 	|                      0.006519 	|     -0.734062 	|              -0.194514 	|                  -0.289361 	|   1.945624 	|       1.290250 	|           0.161666 	|           1.336411 	|       -0.340223 	|           -0.106013 	|  0.379728 	|  0.158661 	| -1.003820 	| -0.914215 	|       0.488958 	|         -1.214659 	|           1.406808 	|

448 rows × 18 columns


## Random Forest Classifier

- One way to use predictive modeling is using **Random Forest Classifier**


```python
from sklearn.ensemble import RandomForestClassifier, RandomForestRegressor

randTree = RandomForestRegressor(min_samples_split=20, random_state=5);
randTree.fit(X, y)
```

Output:

```python
RandomForestRegressor(min_samples_split=20, random_state=5)
```

Now **randTree** is our trained model that we can input data (features X) and predict the number of wins that each team will win!


## Testing our Model 


Now that we have our **Model** we can import a file from 2018 and use that as a test to see how accurate our model is!!


Lets start again by importing data from 2019 College Basketball Season

**Note:** We removed **Year** from column_names since it's not a column in the CSV file

```python
column_names = ["Team", "Conference", "Games Played","Games Won",
          "Adjusted Offensive Efficiency", "Adjusted Defensive Efficiency",
          "Power Ranking", "Effective Field Goal %","Effective Field Goal % (D)",
          "Turnover %", "Turnover % (D)", "Offensive Rebounds", "Defensive Rebounds",
          "Free Throw Rate", "Free Throw Rate (D)", "2-PT%", "2-PT% (D)",
          "3-PT%", "3-PT (D)", "Adjusted Tempo", "Wins above Bubble","Seed in Tournament"]


test_data_2019 = pd.read_csv("cbb19.csv", header = None, names = column_names, skiprows = 1)
test_data_2019
```

Output:

|     	|                   Team 	| Conference 	| Games Played 	| Games Won 	| Adjusted Offensive Efficiency 	| Adjusted Defensive Efficiency 	| Power Ranking 	| Effective Field Goal % 	| Effective Field Goal % (D) 	| Turnover % 	| ... 	| Free Throw Rate 	| Free Throw Rate (D) 	| 2-PT% 	| 2-PT% (D) 	| 3-PT% 	| 3-PT (D) 	| Adjusted Tempo 	| Wins above Bubble 	| Postseason 	| Seed in Tournament 	|
|----:	|-----------------------:	|-----------:	|-------------:	|----------:	|------------------------------:	|------------------------------:	|--------------:	|-----------------------:	|---------------------------:	|-----------:	|----:	|----------------:	|--------------------:	|------:	|----------:	|------:	|---------:	|---------------:	|------------------:	|-----------:	|-------------------:	|
|   0 	|                Gonzaga 	|        WCC 	|           37 	|        33 	|                         123.4 	|                          89.9 	|        0.9744 	|                   59.0 	|                       44.2 	|       14.9 	| ... 	|            35.3 	|                25.9 	|  61.4 	|      43.4 	|  36.3 	|     30.4 	|           72.0 	|               7.0 	|         E8 	|                1.0 	|
|   1 	|               Virginia 	|        ACC 	|           38 	|        35 	|                         123.0 	|                          89.9 	|        0.9736 	|                   55.2 	|                       44.7 	|       14.7 	| ... 	|            29.1 	|                26.3 	|  52.5 	|      45.7 	|  39.5 	|     28.9 	|           60.7 	|              11.1 	|  Champions 	|                1.0 	|
|   2 	|                   Duke 	|        ACC 	|           38 	|        32 	|                         118.9 	|                          89.2 	|        0.9646 	|                   53.6 	|                       45.0 	|       17.5 	| ... 	|            33.2 	|                24.0 	|  58.0 	|      45.0 	|  30.8 	|     29.9 	|           73.6 	|              11.2 	|         E8 	|                1.0 	|
|   3 	|         North Carolina 	|        ACC 	|           36 	|        29 	|                         120.1 	|                          91.4 	|        0.9582 	|                   52.9 	|                       48.9 	|       17.2 	| ... 	|            30.2 	|                28.4 	|  52.1 	|      47.9 	|  36.2 	|     33.5 	|           76.0 	|              10.0 	|        S16 	|                1.0 	|
|   4 	|               Michigan 	|        B10 	|           37 	|        30 	|                         114.6 	|                          85.6 	|        0.9665 	|                   51.6 	|                       44.1 	|       13.9 	| ... 	|            27.5 	|                24.1 	|  51.8 	|      44.3 	|  34.2 	|     29.1 	|           65.9 	|               9.2 	|        S16 	|                2.0 	|
| ... 	|                    ... 	|        ... 	|          ... 	|       ... 	|                           ... 	|                           ... 	|           ... 	|                    ... 	|                        ... 	|        ... 	| ... 	|             ... 	|                 ... 	|   ... 	|       ... 	|   ... 	|      ... 	|            ... 	|               ... 	|        ... 	|                ... 	|
| 348 	|             Alcorn St. 	|       SWAC 	|           27 	|        10 	|                          89.0 	|                         112.6 	|        0.0628 	|                   45.7 	|                       52.7 	|       24.1 	| ... 	|            30.5 	|                36.5 	|  45.0 	|      55.3 	|  31.3 	|     32.1 	|           67.1 	|             -16.7 	|        NaN 	|                NaN 	|
| 349 	|          New Hampshire 	|         AE 	|           27 	|         5 	|                          83.7 	|                         106.1 	|        0.0613 	|                   44.0 	|                       51.5 	|       18.4 	| ... 	|            21.9 	|                38.0 	|  39.4 	|      52.1 	|  32.6 	|     33.6 	|           67.1 	|             -20.2 	|        NaN 	|                NaN 	|
| 350 	|            Chicago St. 	|        WAC 	|           30 	|         3 	|                          88.5 	|                         117.3 	|        0.0380 	|                   44.2 	|                       57.8 	|       22.5 	| ... 	|            33.1 	|                33.9 	|  43.5 	|      57.9 	|  30.7 	|     38.5 	|           71.9 	|             -20.9 	|        NaN 	|                NaN 	|
| 351 	|           Delaware St. 	|       MEAC 	|           29 	|         6 	|                          84.3 	|                         112.2 	|        0.0358 	|                   40.0 	|                       52.4 	|       19.0 	| ... 	|            25.5 	|                39.2 	|  37.7 	|      52.6 	|  29.0 	|     34.7 	|           71.6 	|             -21.7 	|        NaN 	|                NaN 	|
| 352 	| Maryland Eastern Shore 	|       MEAC 	|           30 	|         7 	|                          85.7 	|                         114.4 	|        0.0346 	|                   43.5 	|                       54.4 	|       20.7 	| ... 	|            28.3 	|                36.6 	|  44.5 	|      53.2 	|  27.9 	|     37.3 	|           64.5 	|             -19.9 	|        NaN 	|                NaN 	|




Then lets *clean* the data like we did above!!


```python
# Lets Drop the teams that didn't make the tournment in 2018 and who ever didnt get into the round of 64

test_data_2019 = test_data_2019.dropna()

test_data_2019 = test_data_2019[test_data_2019["Postseason"] != 'R68']
 
## Lets replace the POSTSEASON with the number of wins

test_data_2019 = test_data_2019.replace({
    
    'Champions': 6,
    '2ND': 5,
    'F4': 4,
    'E8': 3,
    'S16': 2,
    'R32': 1,
    'R64': 0
})



# Lets grab the teams that made the Tournment
team_names = test_data_2019.get("Team")

actual_outcomes = test_data_2019.get("Postseason")

# Lets drop the Columns like we did above to the dataset
test_data_2019 = test_data_2019.drop(columns = ["Postseason", "Team","Conference","Games Played","Games Won"])

# Lets finally standardize the data! 

test_data_2019 = (test_data_2019 - test_data_2019.mean())/test_data_2019.std()

test_data_2019
```

Output:

|     	| Adjusted Offensive Efficiency 	| Adjusted Defensive Efficiency 	| Power Ranking 	| Effective Field Goal % 	| Effective Field Goal % (D) 	| Turnover % 	| Turnover % (D) 	| Offensive Rebounds 	| Defensive Rebounds 	| Free Throw Rate 	| Free Throw Rate (D) 	|     2-PT% 	| 2-PT% (D) 	|     3-PT% 	|  3-PT (D) 	| Adjusted Tempo 	| Wins above Bubble 	| Seed in Tournament 	|
|----:	|------------------------------:	|------------------------------:	|--------------:	|-----------------------:	|---------------------------:	|-----------:	|---------------:	|-------------------:	|-------------------:	|----------------:	|--------------------:	|----------:	|----------:	|----------:	|----------:	|---------------:	|------------------:	|-------------------:	|
|   0 	|                      2.042572 	|                     -1.132484 	|      1.073843 	|               2.460166 	|                  -1.566239 	|  -1.786817 	|       0.010948 	|           0.338659 	|          -0.258338 	|        0.390565 	|           -1.264927 	|  3.016431 	| -1.347685 	|  0.262195 	| -1.161525 	|       1.304614 	|          0.951017 	|          -1.614218 	|
|   1 	|                      1.972384 	|                     -1.132484 	|      1.068618 	|               0.941607 	|                  -1.361502 	|  -1.929228 	|      -0.645904 	|           0.058170 	|          -0.736583 	|       -1.103902 	|           -1.164796 	|  0.040748 	| -0.543228 	|  1.656936 	| -1.875394 	|      -2.729147 	|          1.772165 	|          -1.614218 	|
|   2 	|                      1.252960 	|                     -1.260798 	|      1.009833 	|               0.302213 	|                  -1.238660 	|   0.064530 	|       0.186108 	|           1.384121 	|           0.663992 	|       -0.115625 	|           -1.740545 	|  1.879653 	| -0.788062 	| -2.135016 	| -1.399481 	|       1.875766 	|          1.792193 	|          -1.614218 	|
|   3 	|                      1.463523 	|                     -0.857526 	|      0.968031 	|               0.022479 	|                   0.358290 	|  -0.149087 	|      -0.295583 	|           1.307624 	|          -1.624753 	|       -0.838755 	|           -0.639113 	| -0.092990 	|  0.226254 	|  0.218609 	|  0.313805 	|       2.732493 	|          1.551857 	|          -1.614218 	|
|   4 	|                      0.498442 	|                     -1.920698 	|      1.022243 	|              -0.497028 	|                  -1.607186 	|  -2.498873 	|      -0.426954 	|          -1.395277 	|          -0.941545 	|       -1.489571 	|           -1.715513 	| -0.193294 	| -1.032897 	| -0.653104 	| -1.780211 	|      -0.872903 	|          1.391633 	|          -1.398989 	|
| ... 	|                           ... 	|                           ... 	|           ... 	|                    ... 	|                        ... 	|        ... 	|            ... 	|                ... 	|                ... 	|             ... 	|                 ... 	|       ... 	|       ... 	|       ... 	|       ... 	|            ... 	|               ... 	|                ... 	|
|  61 	|                     -1.905487 	|                      0.847215 	|     -1.982937 	|              -0.377142 	|                   0.726817 	|  -0.077881 	|       1.893923 	|          -0.808798 	|           0.322389 	|        0.077209 	|            1.839111 	| -0.962291 	|  0.890806 	|  0.872394 	|  0.218622 	|      -0.444539 	|         -0.971671 	|           1.398989 	|
|  62 	|                     -1.010593 	|                      1.928718 	|     -2.121406 	|               0.781758 	|                   1.013449 	|  -0.220292 	|      -0.339373 	|          -1.981755 	|           1.278879 	|        1.113695 	|           -0.839373 	|  0.408529 	|  1.100664 	|  0.872394 	|  0.408988 	|       0.126613 	|         -1.452343 	|           1.614218 	|
|  63 	|                     -0.905312 	|                      2.368651 	|     -2.436881 	|               0.262251 	|                   2.282819 	|  -1.217172 	|      -2.003398 	|          -2.415239 	|          -0.565781 	|       -0.356669 	|           -1.114731 	| -0.092990 	|  1.870145 	|  0.436537 	|  1.979500 	|      -0.658721 	|         -2.173351 	|           1.614218 	|
|  64 	|                     -1.150969 	|                      2.331990 	|     -2.649158 	|               0.062441 	|                   1.750502 	|  -0.077881 	|      -0.208003 	|          -1.293281 	|           1.073917 	|        0.752130 	|           -0.614080 	|  0.274791 	|  1.065688 	| -0.260833 	|  1.789134 	|       1.268917 	|         -2.533854 	|           1.614218 	|
|  66 	|                     -1.273797 	|                      2.606948 	|     -3.008395 	|               0.541986 	|                   1.627660 	|   1.631054 	|       0.536429 	|          -0.171322 	|           1.927926 	|        0.486983 	|           -0.388787 	| -0.460771 	|  1.415452 	|  1.918449 	|  1.170448 	|      -0.123266 	|         -2.313546 	|           1.614218 	|

64 rows × 18 columns


Now that we have everything formated, we can **test our data on the train model** that we build to test for accuracy!

```python
outcomes = randTree.predict(test_data_2019)
outcomes
```

```python
array([1.07743918, 1.13519988, 2.65392151, 1.41487909, 2.47988569,
       2.94260759, 1.10666421, 2.99517953, 1.47717599, 1.21751297,
       1.3863434 , 2.40559993, 0.87402628, 0.78681459, 1.36926636,
       2.35571116, 0.8465855 , 1.00924984, 2.56186303, 3.01548967,
       1.3497019 , 0.67274804, 2.4168949 , 0.97998758, 0.30464533,
       0.76005142, 0.3474276 , 0.70917375, 0.25876418, 2.25906946,
       1.4213046 , 1.08078719, 0.5007893 , 0.41390343, 2.62928611,
       0.53216457, 0.88700573, 0.03977468, 2.55307896, 0.77592342,
       0.86255786, 0.21795734, 0.38352635, 0.77422673, 1.01526413,
       0.77083375, 0.21385657, 2.55357066, 0.26152267, 0.37922084,
       0.08835621, 0.20948635, 2.53386749, 0.31673781, 0.52333739,
       0.04270588, 0.40829133, 2.66266546, 0.18301588, 0.15924488,
       0.10103648, 0.22302584, 0.04448503, 0.07210633, 0.27154693,
       0.10517421, 0.22233011, 0.05810671])
```


**Lets look at the MSE and R Squared Values**

**R Squared**: is the proportion of the variance in the dependent variable that is predictable from the independent variable(s).

- Range from 0 to 1, closer to 1 is the best! ( 1 being Perfect)

**MSE**: Means Squared Error! (lower number the better)


The **sklearn** library has MSE and R Squared metrics build in, lets first import them!


```python
from sklearn.metrics import mean_squared_error, r2_score
```

```python
print('Mean squared error:', mean_squared_error(actual_outcomes, outcomes)) 
print('Coefficient of determination:', r2_score(actual_outcomes, outcomes))
```

Output:

```python
Mean squared error: 0.3880797220485247
Coefficient of determination: 0.783995849774323
```

Are trained model looks pretty solid when testing the 2019 NCAA Data on it!



## Running Model on 2021 Data

Lets now run our trained model on the 2021 Data to predict the number of wins for each team!!

We have to Change a few columns in the 2021 dataset!

```python
column_names = ["Team", "Conference", "Games Played","Games Won",
          "Adjusted Offensive Efficiency", "Adjusted Defensive Efficiency",
          "Power Ranking", "Effective Field Goal %","Effective Field Goal % (D)",
          "Turnover %", "Turnover % (D)", "Offensive Rebounds", "Defensive Rebounds",
          "Free Throw Rate", "Free Throw Rate (D)", "2-PT%", "2-PT% (D)",
          "3-PT%", "3-PT (D)", "Adjusted Tempo", "Wins above Bubble", "Seed in Tournament"]

data_2021 = pd.read_csv("cbb21.csv", header = None, names = column_names, skiprows = 1)
data_2021
```
Output:

|   	|     Team 	| Conference 	| Games Played 	| Games Won 	| Adjusted Offensive Efficiency 	| Adjusted Defensive Efficiency 	| Power Ranking 	| Effective Field Goal % 	| Effective Field Goal % (D) 	| Turnover % 	| ... 	| Defensive Rebounds 	| Free Throw Rate 	| Free Throw Rate (D) 	| 2-PT% 	| 2-PT% (D) 	| 3-PT% 	| 3-PT (D) 	| Adjusted Tempo 	| Wins above Bubble 	| Seed in Tournament 	|
|--:	|---------:	|-----------:	|-------------:	|----------:	|------------------------------:	|------------------------------:	|--------------:	|-----------------------:	|---------------------------:	|-----------:	|----:	|-------------------:	|----------------:	|--------------------:	|------:	|----------:	|------:	|---------:	|---------------:	|------------------:	|-------------------:	|
| 0 	| Michigan 	|        B10 	|           24 	|        20 	|                         118.1 	|                          91.1 	|        0.9521 	|                   54.9 	|                       44.9 	|       16.3 	| ... 	|               24.8 	|            28.9 	|                24.5 	|  53.3 	|      42.3 	|  38.7 	|     33.5 	|           66.9 	|               7.2 	|                1.0 	|
| 1 	|   Baylor 	|        B12 	|           24 	|        22 	|                         123.2 	|                          94.5 	|        0.9548 	|                   57.5 	|                       49.1 	|       17.6 	| ... 	|               30.9 	|            27.0 	|                31.7 	|  54.1 	|      48.1 	|  41.8 	|     34.0 	|           68.8 	|               6.6 	|                1.0 	|
| 2 	| Illinois 	|        B10 	|           29 	|        23 	|                         117.7 	|                          90.4 	|        0.9539 	|                   55.6 	|                       46.6 	|       18.2 	| ... 	|               22.2 	|            39.2 	|                30.5 	|  55.3 	|      45.4 	|  37.6 	|     32.7 	|           70.7 	|               8.9 	|                1.0 	|
| 3 	|  Gonzaga 	|        WCC 	|           26 	|        26 	|                         125.4 	|                          89.8 	|        0.9791 	|                   61.0 	|                       47.5 	|       16.1 	| ... 	|               23.4 	|            36.7 	|                25.9 	|  64.0 	|      46.8 	|  36.5 	|     32.5 	|           74.6 	|               8.5 	|                1.0 	|
| 4 	|     Iowa 	|        B10 	|           29 	|        21 	|                         123.5 	|                          95.7 	|        0.9491 	|                   54.6 	|                       48.3 	|       13.3 	| ... 	|               28.6 	|            32.0 	|                22.6 	|  52.4 	|      45.8 	|  38.6 	|     34.8 	|           70.0 	|               5.6 	|                2.0 	|



Now we can Clean and Adjust the data!

```python

# Drop teams that didn't make the tournament
data_2021 = data_2021.dropna()

#Grab Team names

team_names = data_2021.get("Team")

# Lets drop the Columns like we did above to the dataset

data_2021 = data_2021.drop(columns = ["Team","Conference","Games Played","Games Won"])

# Lets finally standardize the data! 

data_2021 = (data_2021 - data_2021.mean())/data_2021.std()

data_2021.head()

```

Output:

|   	| Adjusted Offensive Efficiency 	| Adjusted Defensive Efficiency 	| Power Ranking 	| Effective Field Goal % 	| Effective Field Goal % (D) 	| Turnover % 	| Turnover % (D) 	| Offensive Rebounds 	| Defensive Rebounds 	| Free Throw Rate 	| Free Throw Rate (D) 	|    2-PT% 	| 2-PT% (D) 	|    3-PT% 	| 3-PT (D) 	| Adjusted Tempo 	| Wins above Bubble 	| Seed in Tournament 	|   	|   	|   	|
|--:	|------------------------------:	|------------------------------:	|--------------:	|-----------------------:	|---------------------------:	|-----------:	|---------------:	|-------------------:	|-------------------:	|----------------:	|--------------------:	|---------:	|----------:	|---------:	|---------:	|---------------:	|------------------:	|-------------------:	|---	|---	|---	|
| 0 	|                      1.254529 	|                     -0.974462 	|      0.932161 	|               0.994790 	|                  -1.565422 	|  -0.665798 	|      -1.700853 	|          -0.208926 	|          -0.735535 	|       -0.676980 	|           -1.116763 	| 0.508850 	| -2.126998 	| 1.395668 	| 0.642816 	|      -0.302966 	|          1.712498 	|          -1.658834 	|   	|   	|   	|
| 1 	|                      2.040990 	|                     -0.204484 	|      0.948353 	|               1.944973 	|                   0.797604 	|  -0.067054 	|       2.207902 	|           1.853376 	|           1.237944 	|       -1.128067 	|            0.244709 	| 0.757337 	|  0.360808 	| 2.669843 	| 0.907414 	|       0.347254 	|          1.544582 	|          -1.658834 	|   	|   	|   	|
| 2 	|                      1.192845 	|                     -1.132987 	|      0.942956 	|               1.250609 	|                  -0.608959 	|   0.209289 	|      -1.289405 	|           0.707653 	|          -1.576689 	|        1.768387 	|            0.017797 	| 1.130067 	| -0.797309 	| 0.943542 	| 0.219460 	|       0.997474 	|          2.188261 	|          -1.658834 	|   	|   	|   	|
| 3 	|                      2.380248 	|                     -1.268865 	|      1.094084 	|               3.224066 	|                  -0.102596 	|  -0.757912 	|       0.438676 	|           0.045679 	|          -1.188464 	|        1.174851 	|           -0.852032 	| 3.832363 	| -0.196804 	| 0.491416 	| 0.113621 	|       2.332137 	|          2.076317 	|          -1.658834 	|   	|   	|   	|
| 4 	|                      2.087253 	|                      0.067273 	|      0.914169 	|               0.885154 	|                   0.347504 	|  -2.047515 	|      -1.207115 	|           0.122061 	|           0.493845 	|        0.059004 	|           -1.476040 	| 0.229302 	| -0.625736 	| 1.354566 	| 1.330770 	|       0.757919 	|          1.264722 	|          -1.446003 	|   	|   	|   	|



Now we can use our trained model to make Predictions (number of wins for each team)

```python
outcomes = randTree.predict(data_2021)
outcomes
```

```python
array([2.90137755, 3.25091381, 2.86165301, 4.76819429, 3.18066861,
       2.36148922, 3.09853133, 2.06465737, 1.92141687, 1.39338319,
       0.8818488 , 1.83575132, 2.52558497, 1.0863441 , 1.73735455,
       0.83906491, 1.74379691, 1.33183751, 1.12418422, 1.20195583,
       1.03637919, 1.4480753 , 1.11063843, 1.49674965, 0.64235945,
       1.30626018, 0.74411647, 0.47462401, 0.52989933, 0.79758753,
       1.2647636 , 1.4425606 , 0.63045054, 0.70913249, 2.06620984,
       0.86648306, 0.60994555, 0.61427192, 2.18634874, 0.52689784,
       0.33416316, 0.25236245, 1.0838805 , 0.79748643, 0.82304538,
       0.40971093, 1.07154771, 0.14501442, 0.28730544, 0.31200205,
       0.2381309 , 0.43729915, 0.18642513, 0.29956863, 0.46401838,
       0.10031835, 0.32652622, 0.08293184, 0.11272476, 0.1299452 ,
       0.15566156, 0.07748426, 0.08898297, 0.09433593, 0.16023765,
       0.05697938, 0.02390829, 0.09276995])

```

Convert Team names to a Frame

```python
team_names = team_names.to_numpy()
```

Lets print out the **Projected Wins** for each team!


```python
for i in range(len(team_names)):
    print(team_names[i], outcomes[i])
```


### Projected Number of Wins for 2021 Tourny

**Projected Number of Wins in Tourny for Teams**

```python
Michigan 2.901377551068698
Baylor 3.2509138093289214
Illinois 2.8616530060354
Gonzaga 4.768194292284091
Iowa 3.1806686060196636
Ohio St. 2.3614892221216515
Houston 3.098531328889728
Alabama 2.0646573670639774
West Virginia 1.9214168657035833
Texas 1.3933831859470671
Kansas 0.8818487965279312
Arkansas 1.83575131694493
Florida St. 2.5255849661183216
Virginia 1.08634409745
Purdue 1.737354550600605
Oklahoma St. 0.8390649078411792
Villanova 1.7437969052107938
Tennessee 1.3318375107722848
Creighton 1.1241842230904682
Colorado 1.2019558332965143
Texas Tech 1.036379192388832
BYU 1.4480752958728775
USC 1.1106384309237298
San Diego St. 1.4967496522059323
Florida 0.6423594519586673
Connecticut 1.3062601784053558
Clemson 0.7441164652698969
Oregon 0.47462400545930694
Oklahoma 0.5298993343723692
North Carolina 0.7975875291664838
LSU 1.2647635969699733
Loyola Chicago 1.4425605963594352
St. Bonaventure 0.6304505421114232
Missouri 0.709132494142787
Wisconsin 2.066209844623407
Georgia Tech 0.8664830586357855
Rutgers 0.6099455505034019
Virginia Tech 0.6142719174309312
Maryland 2.186348739514017
VCU 0.5268978448812078
Michigan St. 0.33416316257893075
Wichita St. 0.252362451365367
Syracuse 1.0838804985591546
UCLA 0.7974864348475628
Utah St. 0.8230453823210917
Drake 0.40971093402267866
Georgetown 1.0715477143484449
Oregon St. 0.14501442395206512
UC Santa Barbara 0.2873054411083263
Winthrop 0.31200205260351155
Ohio 0.23813090226222985
North Texas 0.4372991516463077
UNC Greensboro 0.18642513089080598
Liberty 0.29956862571123394
Colgate 0.4640183849244288
Eastern Washington 0.10031835221526803
Abilene Christian 0.3265262248702281
Morehead St. 0.0829318449854731
Iona 0.11272475691949374
Oral Roberts 0.12994520485084304
Grand Canyon 0.15566156131186967
Cleveland St. 0.07748425598062622
Drexel 0.08898296549941286
Mount St. Marys 0.09433592975651799
Hartford 0.16023764568764565
Norfolk St. 0.056979379782011355
Texas Southern 0.023908293460925042
Appalachian St. 0.09276995322684975
```



#### Important Features


**What are the important Features?**


```python
Importances = randTree.feature_importances_
print('Features | Coefficients:')
print('-------------------------------')
for i in range(len(Importances)):
    print(data_2021.columns[i], ":", Importances[i])
```

Output:

```python
Features | Coefficients:
-------------------------------
Adjusted Offensive Efficiency : 0.01929179106662344
Adjusted Defensive Efficiency : 0.012166986101116231
Power Ranking : 0.673670498282482
Effective Field Goal % : 0.016918569685206462
Effective Field Goal % (D) : 0.008659203235951584
Turnover % : 0.016029947205072663
Turnover % (D) : 0.011657031108119028
Offensive Rebounds : 0.04872405222299242
Defensive Rebounds : 0.03678456545563587
Free Throw Rate : 0.0287558387075352
Free Throw Rate (D) : 0.01523000282671945
2-PT% : 0.01392243965528682
2-PT% (D) : 0.013467855281397186
3-PT% : 0.014077173558140924
3-PT (D) : 0.016480450413741625
Adjusted Tempo : 0.015892583071390052
Wins above Bubble : 0.018270456403570653
Seed in Tournament : 0.020000555719018376
```

We can see above that some important Features (stats) are **Power Ranking**, **Rebounding (both offensive and defensive**, **Free Throws**



From here I am just going to look at the matchups on the NCAA Bracket and pick the winners of each game based on the the **Projected wins**, so whoever has the **Higher Projected wins** will advance in each matchup.


### Bracket Filled Out

![insert image](/images/big_data/March/ncaa_bracket_filled.jpg)


**Some notably upsets include:**

**West**
* Missouri over Oklahoma in the 1st round
* USC over Kansas in the 2nd round
* VCU over Oregon in the 1st round
* Creighton over Virgina (returning champions) in the 2nd round

**East**

* Maryland over Uconn in the first round
* Maryland over Alabama in the 2nd round
* BYU over Texas in the 2nd round
* Maryland making it to the Elite 8

**South**

* Wisconsin over UNC (not really suprising)
* Villanova over Purdue in the 2nd round

**Midwest**

* Tennessee over OSU in the 2nd round
* Houston over Illinois in the Elite 8 to make it to the Final 4


### Final Four Projections

* Gonzaga over Michigan

* Baylor over Houston

### Championship

* Gonzaga over Baylor for the Title!


**And the Winner of the 2021 NCAA Division 1 Basketball is...**

# Gonzaga!!!

![insert image](/images/big_data/March/adam.jpeg)

THE GOAT **ADAM MORRISON**




