---
title: 'March Madness Prediction '

date: 2021-3-16

header:

  image: "/images/magic.jpeg"

---

Lets predict who will win in the tournament....


![insert image](/images/big_data/msu.jpg)

kidding.....maybe



I found a College Basketball Dataset 2013 - 2021 seasons on Kaggle

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




#### Now the question is... What columns should we keep and what columns should we remove??

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



Lets drop those columns:

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




### Now lets normalize our data

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


### Now that we have our **Model** we can import a file from 2018 and use that as a test to see how accurate our model is!!


Lets start again by importing data from 2018 College Basketball Season

**Note:** We removed **Year** from column_names since it's not a column in the CSV file

```python
column_names = ["Team", "Conference", "Games Played","Games Won",
          "Adjusted Offensive Efficiency", "Adjusted Defensive Efficiency",
          "Power Ranking", "Effective Field Goal %","Effective Field Goal % (D)",
          "Turnover %", "Turnover % (D)", "Offensive Rebounds", "Defensive Rebounds",
          "Free Throw Rate", "Free Throw Rate (D)", "2-PT%", "2-PT% (D)",
          "3-PT%", "3-PT (D)", "Adjusted Tempo", "Wins above Bubble", "Postseason","Seed in Tournament"]

test_data_2018 = pd.read_csv("cbb18.csv", header = None, names = column_names, skiprows = 1)
```

Then lets *clean* the data like we did above!!


```python
# Lets Drop the teams that didn't make the tournment in 2018 and who ever didnt get into the round of 64

test_data_2018 = test_data_2018.dropna()

test_data_2018 = test_data_2018[test_data_2018["Postseason"] != 'R68']
 
## Lets replace the POSTSEASON with the number of wins

test_data_2018 = test_data_2018.replace({
    
    'Champions': 6,
    '2ND': 5,
    'F4': 4,
    'E8': 3,
    'S16': 2,
    'R32': 1,
    'R64': 0
})

# Lets grab the teams that made the Tournment
team_names = test_data_2018.get("Team")

labels = test_data_2018.get("Postseason")
# Lets drop the Columns like we did above to the dataset
test_data_2018 = test_data_2018.drop(columns = ["Postseason", "Team","Conference","Games Played","Games Won"])

# Lets finally standardize the data! 

test_data_2018 = (test_data_2018 - test_data_2018.mean())/test_data_2018.std()

test_data_2018
```

Output:

|     	| Adjusted Offensive Efficiency 	| Adjusted Defensive Efficiency 	| Power Ranking 	| Effective Field Goal % 	| Effective Field Goal % (D) 	| Turnover % 	| Turnover % (D) 	| Offensive Rebounds 	| Defensive Rebounds 	| Free Throw Rate 	| Free Throw Rate (D) 	|     2-PT% 	| 2-PT% (D) 	|     3-PT% 	|  3-PT (D) 	| Adjusted Tempo 	| Wins above Bubble 	| Seed in Tournament 	|
|----:	|------------------------------:	|------------------------------:	|--------------:	|-----------------------:	|---------------------------:	|-----------:	|---------------:	|-------------------:	|-------------------:	|----------------:	|--------------------:	|----------:	|----------:	|----------:	|----------:	|---------------:	|------------------:	|-------------------:	|
|   0 	|                      2.579463 	|                     -0.761656 	|      1.152933 	|               2.430809 	|                  -0.082145 	|  -1.263596 	|      -0.245655 	|          -0.109757 	|          -0.212295 	|       -1.025966 	|           -0.965148 	|  2.222601 	|  0.568321 	|  1.587796 	| -1.074600 	|       0.020946 	|          2.092867 	|          -1.614218 	|
|   1 	|                      0.337820 	|                     -2.427031 	|      1.075074 	|              -0.241975 	|                  -2.107888 	|  -1.860864 	|       1.002849 	|          -0.726767 	|          -0.744418 	|       -2.031728 	|           -1.054851 	| -0.786654 	| -1.735150 	|  0.795617 	| -1.437116 	|      -3.106958 	|          2.253664 	|          -1.614218 	|
|   2 	|                      1.588592 	|                     -1.031717 	|      1.061294 	|               1.015805 	|                  -1.095017 	|   0.229575 	|      -0.661823 	|           2.073512 	|           0.816476 	|        0.041372 	|           -1.754534 	|  1.208245 	| -0.769178 	|  0.311508 	| -0.919236 	|       0.467789 	|          1.174030 	|          -1.398989 	|
|   3 	|                      1.734786 	|                     -0.401575 	|      0.986881 	|               1.723307 	|                  -0.805625 	|  -0.785781 	|      -0.476859 	|          -0.489456 	|           0.106979 	|        0.246630 	|           -1.413662 	|  0.565820 	| -0.732025 	|  2.423986 	| -0.297781 	|      -0.288407 	|          1.403739 	|          -1.398989 	|
|   4 	|                     -0.149494 	|                     -2.201980 	|      0.940717 	|              -0.831560 	|                  -2.590208 	|  -0.069059 	|       1.326536 	|           2.002318 	|           0.177929 	|        0.328733 	|           -0.947207 	| -0.752842 	| -2.255288 	| -0.524681 	| -1.488904 	|      -1.147722 	|          1.013233 	|          -1.398989 	|
| ... 	|                           ... 	|                           ... 	|           ... 	|                    ... 	|                        ... 	|        ... 	|            ... 	|                ... 	|                ... 	|             ... 	|                 ... 	|       ... 	|       ... 	|       ... 	|       ... 	|            ... 	|               ... 	|                ... 	|
| 153 	|                     -0.604320 	|                      2.276528 	|     -1.873209 	|               0.229692 	|                   1.847134 	|  -0.666328 	|       0.031791 	|          -1.320047 	|           1.100275 	|       -0.861760 	|           -0.624276 	| -0.313288 	|  1.571445 	|  0.795617 	|  1.048706 	|       0.674025 	|         -2.018929 	|           1.398989 	|
| 163 	|                     -1.692654 	|                      1.061254 	|     -2.128143 	|              -0.438504 	|                   1.413046 	|   0.050395 	|       0.910368 	|          -0.987810 	|           0.213403 	|       -0.861760 	|           -0.229583 	| -1.462891 	|  1.311376 	|  0.751607 	|  0.634402 	|      -0.082172 	|         -1.467627 	|           1.614218 	|
| 171 	|                     -1.773873 	|                      1.128770 	|     -2.268013 	|              -0.674338 	|                  -0.226841 	|   2.140834 	|      -0.245655 	|          -0.964079 	|           0.426253 	|        2.299204 	|            0.559802 	| -0.144229 	| -0.917789 	| -1.184830 	|  1.359434 	|       0.399044 	|         -1.605453 	|           1.398989 	|
| 182 	|                     -1.822604 	|                      1.196285 	|     -2.406504 	|              -1.578368 	|                   0.689567 	|   0.946297 	|       0.679163 	|           0.459792 	|           0.106979 	|       -0.656503 	|           -0.068118 	| -1.801009 	|  0.531168 	| -0.656711 	|  0.427251 	|      -1.835173 	|         -1.835162 	|           1.614218 	|
| 258 	|                     -1.367778 	|                      3.356771 	|     -3.528905 	|              -1.106700 	|                   1.220118 	|   0.050395 	|      -1.170473 	|          -0.370800 	|           1.703347 	|        1.745009 	|           -0.157821 	| -1.327643 	|  0.716932 	| -0.260621 	|  1.463010 	|       1.052123 	|         -2.845883 	|           1.614218 	|

64 rows × 18 columns


Now that we have everything formated, we can **test our data on the train model** that we build to test for accuracy!

```python
outcomes = randTree.predict(test_data_2018)
outcomes
```

```python
array([4.79374106, 4.50706001, 4.63436916, 2.92119834, 2.44943964,
       2.92408205, 2.53887016, 1.85535918, 1.97381219, 1.7675324 ,
       1.9517013 , 2.0826024 , 1.69939146, 1.50933805, 1.64787509,
       1.8062911 , 1.48300696, 1.41080189, 1.34507522, 1.30606804,
       0.84765406, 0.92654377, 0.56113908, 0.77383816, 0.62359858,
       0.71972569, 0.59706735, 0.65653557, 0.84654274, 0.27220807,
       0.48551756, 0.85555839, 0.79078947, 0.5566213 , 0.75432677,
       0.68419701, 0.49255355, 0.58879836, 1.12082712, 0.64836982,
       0.87441541, 0.4570832 , 0.24411728, 0.24689467, 0.3344182 ,
       0.22142439, 0.31518034, 0.11686592, 0.20606556, 0.25557758,
       0.05800339, 0.18187103, 0.29142277, 0.04124938, 0.26513749,
       0.33923594, 0.01466802, 0.11317538, 0.18958856, 0.04887212,
       0.09793627, 0.048189  , 0.14309469, 0.03703799])
```


#### Lets look at the MSE and R Squared Values

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
Mean squared error: 1.2053217759220127
Coefficient of determination: 0.3291210770245191
```
Wow those numbers blow

## Decision Tree Test

```python
from sklearn.model_selection import train_test_split
X_train, X_test, Y_train, Y_test = train_test_split(X, y, test_size=0.8, random_state=1)
```

Our Model was trained

```python
from sklearn import tree

clf = tree.DecisionTreeClassifier(max_depth = 15)
clf = clf.fit(X_train, Y_train)
Y_pred = clf.predict(X_test)
```

```python
from sklearn.metrics import accuracy_score

accuracy_score(Y_test, Y_pred)
```

Output:

```python
0.362116991643454
```



## Lets now run our trained model on the 2021 Data to predict the number of wins for each team!!
