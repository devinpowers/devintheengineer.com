---
layout: archive
permalink: /Big_Data/big_data/day_11
title: "Anomaly Detection"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

### What is Anomaly Detection?

* Finding a subset of instances whose characteristics are different than the remainder of the data
* Think Outliers in Data!!


**Example Applications**

* Detecting fraud purchases on credit cards

### Challenges in Anomaly Detection

* Like finding a needle in a haystack
* Number of anomalies are usually unknown
* Method is unsupervised

### Python Example

```python
import pandas as pd

data = pd.read_csv('Synthetic_control_sample.csv',header=None)
data.head()

```

Output:

|   	|           	|       1 	|       2 	|       3 	|       4 	|        5 	|         6 	|        7 	|        8 	|       9 	| ... 	|       50 	|       51 	|        52 	|       53 	|       54 	|     55 	|      56 	|      57 	|        58 	|        59 	|
|--:	|----------:	|--------:	|--------:	|--------:	|--------:	|---------:	|----------:	|---------:	|---------:	|--------:	|----:	|---------:	|---------:	|----------:	|---------:	|---------:	|-------:	|--------:	|--------:	|----------:	|----------:	|
| 0 	|  0.448130 	| 0.30272 	| 0.39039 	| 1.55520 	| 1.36110 	|  1.00610 	|  0.636930 	| -0.51374 	| -0.69051 	| -1.5134 	| ... 	| -0.89196 	| -0.73934 	|  0.821470 	|  1.13340 	|  0.52480 	| 1.5382 	| 1.05790 	| 0.10072 	| -0.079991 	| -0.734820 	|
| 1 	|  0.324930 	| 0.92102 	| 0.67606 	| 1.56710 	| 0.62195 	|  0.23225 	|  0.699970 	| -0.29080 	| -1.06150 	| -1.1291 	| ... 	| -0.89692 	| -1.61170 	|  0.049964 	| -0.20141 	|  0.96575 	| 1.5515 	| 1.34120 	| 0.54099 	|  0.488130 	|  0.075192 	|
| 2 	|  0.065106 	| 0.27966 	| 1.60660 	| 0.90703 	| 0.31790 	| -0.38201 	| -0.071902 	| -1.69230 	| -1.05300 	| -1.0928 	| ... 	| -0.85534 	| -1.61720 	| -0.786690 	| -0.44217 	|  0.61959 	| 1.4380 	| 1.21310 	| 1.20440 	|  0.411550 	| -0.733190 	|
| 3 	| -0.197290 	| 0.86487 	| 0.91300 	| 1.10690 	| 1.13040 	|  0.22366 	| -0.070158 	| -0.91154 	| -1.32590 	| -1.3727 	| ... 	| -1.51920 	| -1.82530 	| -0.541960 	| -0.64238 	|  0.20283 	| 1.1598 	| 1.76730 	| 1.27050 	|  0.200010 	| -0.351930 	|
| 4 	| -0.295140 	| 0.27611 	| 1.36790 	| 1.12880 	| 0.68236 	|  0.27383 	| -0.083935 	| -0.64006 	| -1.38620 	| -1.1307 	| ... 	| -1.03950 	| -1.28350 	| -1.317100 	| -1.13480 	| -0.46492 	| 0.5699 	| 0.95651 	| 0.87453 	|  0.811540 	| -0.451390 	|


Lets graph our data above:

```python
import matplotlib.pyplot as plt
%matplotlib inline

plt.figure().add_subplot(2,2,1)
plt.plot(data.ix[5].T)
plt.figure().add_subplot(2,2,1)
plt.plot(data.ix[10].T)
plt.figure().add_subplot(2,2,1)
plt.plot(data.ix[45].T)
plt.figure().add_subplot(2,2,1)
plt.plot(data.ix[50].T)
```

Output:

![insert image](/images/big_data/day14/graphs.png)
