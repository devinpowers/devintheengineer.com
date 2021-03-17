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

|      	|     ADJOE 	|     ADJDE 	|  BARTHAG 	|     EFG_O 	|     EFG_D 	|       TOR 	|      TORD 	|       ORB 	|       DRB 	|       FTR 	|      FTRD 	|     2P_O 	|      2P_D 	|      3P_O 	|      3P_D 	|     ADJ_T 	|      WAB 	|      SEED 	|
|-----:	|----------:	|----------:	|---------:	|----------:	|----------:	|----------:	|----------:	|----------:	|----------:	|----------:	|----------:	|---------:	|----------:	|----------:	|----------:	|----------:	|---------:	|----------:	|
|    0 	|  1.790975 	| -0.344966 	| 0.927239 	|  0.025708 	|  0.070145 	| -1.158243 	| -0.292501 	|  2.254545 	|  0.528910 	| -0.733603 	| -0.380176 	| 0.768122 	| -0.746034 	| -1.410947 	|  1.345417 	|  1.118666 	| 1.406516 	| -1.622565 	|
|    1 	|  2.720675 	| -0.602885 	| 1.070661 	|  0.830086 	| -0.097678 	| -2.962418 	| -1.354130 	|  0.204552 	| -1.641418 	|  0.068093 	| -1.793344 	| 1.060508 	| -0.711749 	|  0.125053 	|  1.962839 	| -2.671675 	| 1.962761 	| -1.622565 	|
|    2 	|  0.364366 	| -1.237763 	| 0.828677 	|  0.501022 	| -0.097678 	| -2.000191 	|  0.282548 	| -1.368698 	| -1.228022 	| -1.062504 	| -0.450834 	| 1.028021 	|  0.008250 	| -0.400421 	| -0.079404 	| -0.654235 	| 1.056287 	| -1.189701 	|
|    3 	|  0.492601 	| -2.269438 	| 1.031488 	|  0.354772 	| -2.069599 	|  0.224958 	|  1.742288 	| -0.915792 	|  0.081064 	| -0.610266 	|  0.715030 	| 0.410762 	| -1.671747 	|  0.125053 	| -1.741695 	| -0.165159 	| 1.076889 	| -1.189701 	|
|    4 	|  0.909363 	| -2.051199 	| 1.051706 	|  1.488214 	| -2.866759 	| -0.677129 	| -0.779081 	| -0.296027 	| -0.780177 	|  0.643670 	| -0.998437 	| 1.547818 	| -2.323175 	|  0.812210 	| -2.074154 	|  1.057532 	| 1.221100 	| -1.622565 	|
|  ... 	|       ... 	|       ... 	|      ... 	|       ... 	|       ... 	|       ... 	|       ... 	|       ... 	|       ... 	|       ... 	|       ... 	|      ... 	|       ... 	|       ... 	|       ... 	|       ... 	|      ... 	|       ... 	|
| 1752 	| -0.148572 	| -0.384646 	| 0.364295 	| -0.413044 	| -0.433324 	|  1.127046 	| -1.575303 	|  0.633620 	| -0.401231 	| -0.795272 	| -0.874785 	| 0.313300 	| -0.368892 	| -1.330105 	| -0.364368 	|  0.690725 	| 0.026203 	| -0.323972 	|
| 1753 	|  0.925392 	| -0.007688 	| 0.642924 	| -0.486169 	|  0.825349 	|  0.345236 	|  0.547956 	|  1.301060 	|  0.804507 	|  0.253100 	|  0.096769 	| 0.443249 	|  0.899677 	| -1.734315 	|  0.158066 	|  0.965830 	| 1.138694 	| -1.189701 	|
| 1754 	|  1.710828 	| -0.285447 	| 0.900072 	|  1.012899 	|  0.070145 	| -0.917686 	| -0.380970 	|  0.085367 	|  0.597809 	| -0.528040 	|  0.414732 	| 1.255432 	| -0.711749 	|  0.205895 	|  0.965465 	|  0.232216 	| 1.674337 	| -1.406133 	|
| 1755 	|  0.845246 	| -0.424326 	| 0.742119 	|  0.976337 	| -1.314395 	| -0.135877 	| -1.663772 	|  0.204552 	| -0.849076 	| -0.301921 	| -0.786462 	| 0.898072 	| -0.814606 	|  0.650526 	| -1.456731 	|  0.048812 	| 0.067406 	|  0.541757 	|
| 1756 	|  0.813187 	| -0.344966 	| 0.713055 	|  1.634464 	| -0.349413 	| -0.737269 	| -0.646377 	|  0.419086 	| -1.848115 	| -0.774716 	| -0.609815 	| 2.165078 	| -0.917463 	|  0.246316 	|  0.775489 	|  0.751859 	| 0.644253 	| -0.973269 	|

320 rows × 18 columns


**Random Forest Classifier**

```python
from sklearn.ensemble import RandomForestClassifier, RandomForestRegressor

randTree = RandomForestRegressor(min_samples_split=20, random_state=5);
randTree.fit(X, y)
```

Output:

**RandomForestRegressor(min_samples_split=20, random_state=5)**




### Now that we have our **Model** we can import a file from 2018 and use that as a test to see how accurate our model is!!


Lets start again by importing data from 2018 College Basketball Season

```python
test_data_2018 = pd.read_csv("cbb18.csv")
```

Then lets *clean* the data like we did above


```python
# Lets Drop the teams that didn't make the tournment in 2018 and who ever didnt get into the round of 64

test_data_2018 = test_data_2018.dropna()

test_data_2018 = test_data_2018[test_data_2018["POSTSEASON"] != 'R68']
 
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
team_names = test_data_2018.get("TEAM")

labels = test_data_2018.get("POSTSEASON")
# Lets drop the Columns like we did above to the dataset
test_data_2018 = test_data_2018.drop(columns = ["POSTSEASON","TEAM","CONF","G","W"])


# Lets finally standardize the data! 

test_data_2018 = (test_data_2018 - test_data_2018.mean())/test_data_2018.std()


test_data_2018
```

Output:

|     	|     ADJOE 	|     ADJDE 	|   BARTHAG 	|     EFG_O 	|     EFG_D 	|       TOR 	|      TORD 	|       ORB 	|       DRB 	|       FTR 	|      FTRD 	|      2P_O 	|      2P_D 	|      3P_O 	|      3P_D 	|     ADJ_T 	|       WAB 	|      SEED 	|
|----:	|----------:	|----------:	|----------:	|----------:	|----------:	|----------:	|----------:	|----------:	|----------:	|----------:	|----------:	|----------:	|----------:	|----------:	|----------:	|----------:	|----------:	|----------:	|
|   0 	|  2.579463 	| -0.761656 	|  1.152933 	|  2.430809 	| -0.082145 	| -1.263596 	| -0.245655 	| -0.109757 	| -0.212295 	| -1.025966 	| -0.965148 	|  2.222601 	|  0.568321 	|  1.587796 	| -1.074600 	|  0.020946 	|  2.092867 	| -1.614218 	|
|   1 	|  0.337820 	| -2.427031 	|  1.075074 	| -0.241975 	| -2.107888 	| -1.860864 	|  1.002849 	| -0.726767 	| -0.744418 	| -2.031728 	| -1.054851 	| -0.786654 	| -1.735150 	|  0.795617 	| -1.437116 	| -3.106958 	|  2.253664 	| -1.614218 	|
|   2 	|  1.588592 	| -1.031717 	|  1.061294 	|  1.015805 	| -1.095017 	|  0.229575 	| -0.661823 	|  2.073512 	|  0.816476 	|  0.041372 	| -1.754534 	|  1.208245 	| -0.769178 	|  0.311508 	| -0.919236 	|  0.467789 	|  1.174030 	| -1.398989 	|
|   3 	|  1.734786 	| -0.401575 	|  0.986881 	|  1.723307 	| -0.805625 	| -0.785781 	| -0.476859 	| -0.489456 	|  0.106979 	|  0.246630 	| -1.413662 	|  0.565820 	| -0.732025 	|  2.423986 	| -0.297781 	| -0.288407 	|  1.403739 	| -1.398989 	|
|   4 	| -0.149494 	| -2.201980 	|  0.940717 	| -0.831560 	| -2.590208 	| -0.069059 	|  1.326536 	|  2.002318 	|  0.177929 	|  0.328733 	| -0.947207 	| -0.752842 	| -2.255288 	| -0.524681 	| -1.488904 	| -1.147722 	|  1.013233 	| -1.398989 	|
| ... 	|       ... 	|       ... 	|       ... 	|       ... 	|       ... 	|       ... 	|       ... 	|       ... 	|       ... 	|       ... 	|       ... 	|       ... 	|       ... 	|       ... 	|       ... 	|       ... 	|       ... 	|       ... 	|
| 153 	| -0.604320 	|  2.276528 	| -1.873209 	|  0.229692 	|  1.847134 	| -0.666328 	|  0.031791 	| -1.320047 	|  1.100275 	| -0.861760 	| -0.624276 	| -0.313288 	|  1.571445 	|  0.795617 	|  1.048706 	|  0.674025 	| -2.018929 	|  1.398989 	|
| 163 	| -1.692654 	|  1.061254 	| -2.128143 	| -0.438504 	|  1.413046 	|  0.050395 	|  0.910368 	| -0.987810 	|  0.213403 	| -0.861760 	| -0.229583 	| -1.462891 	|  1.311376 	|  0.751607 	|  0.634402 	| -0.082172 	| -1.467627 	|  1.614218 	|
| 171 	| -1.773873 	|  1.128770 	| -2.268013 	| -0.674338 	| -0.226841 	|  2.140834 	| -0.245655 	| -0.964079 	|  0.426253 	|  2.299204 	|  0.559802 	| -0.144229 	| -0.917789 	| -1.184830 	|  1.359434 	|  0.399044 	| -1.605453 	|  1.398989 	|
| 182 	| -1.822604 	|  1.196285 	| -2.406504 	| -1.578368 	|  0.689567 	|  0.946297 	|  0.679163 	|  0.459792 	|  0.106979 	| -0.656503 	| -0.068118 	| -1.801009 	|  0.531168 	| -0.656711 	|  0.427251 	| -1.835173 	| -1.835162 	|  1.614218 	|
| 258 	| -1.367778 	|  3.356771 	| -3.528905 	| -1.106700 	|  1.220118 	|  0.050395 	| -1.170473 	| -0.370800 	|  1.703347 	|  1.745009 	| -0.157821 	| -1.327643 	|  0.716932 	| -0.260621 	|  1.463010 	|  1.052123 	| -2.845883 	|  1.614218 	|

64 rows × 18 columns


Now that we have everything formated, we can test our data on the train model that we build to test for accuracy!

```python
outcomes = randTree.predict(test_data_2018)
```

Lets look at the MSE and r^2

```python
from sklearn.metrics import mean_squared_error, r2_score
```

```python
#from sci learn metrics
print('Mean squared error: %.2f'
      %mean_squared_error(labels, outcomes)) 
# The coefficient of determination: 1 is perfect prediction
print('Coefficient of determination: %.2f'
      % r2_score(labels, outcomes))

```

Output:

**Mean squared error: 1.13**
**Coefficient of determination: 0.37**

