---
layout: archive
permalink: /Big_Data/big_data/day_11
title: "Anomaly Detection"
author_profile: true


toc: true
toc_label: "Table of Contents" 

header:
  image: "/images/chicagotwo.jpeg"
  
---

### What is Anomaly Detection?

* Finding a subset of instances whose characteristics are different than the remainder of the data
* Think Outliers in Data!!


**Example Applications**

* Detecting fraud purchases on credit cards
* Detecting deforestation using remote sensing data
* Smart Homes/Building
  * Water or electrical theft detection
  * Pip burst detection

### Challenges in Anomaly Detection

* Like finding a needle in a haystack
* Number of anomalies are usually unknown
* Method is unsupervised

### Python Example of Distance-Based Approach

* Compute the distance between every pair of data points
* Anomaly score of a data point is given by its distance to the k-th nearest neighbor
    * The larger distance, the more anomalous is the data point


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
plt.plot(data.iloc[5].T)
plt.figure().add_subplot(2,2,1)
plt.plot(data.iloc[10].T)
plt.figure().add_subplot(2,2,1)
plt.plot(data.iloc[45].T)
plt.figure().add_subplot(2,2,1)
plt.plot(data.iloc[50].T)
```

Output:

![insert image](/images/big_data/day14/graphs.png)


```python
plt.figure().add_subplot(2,1,1)
plt.plot(data.iloc[:49].T)
plt.figure().add_subplot(2,1,2)
plt.plot(data.iloc[50:55].T)
```

Output:

![insert image](/images/big_data/day14/graphs2.png)


```python
from scipy.spatial import distance

Y = distance.pdist(data.to_numpy(), 'correlation')
Y = distance.squareform(Y)
Y
```

Output:

```python
array([[ 0.        ,  0.20237268,  1.16745543, ...,  1.07495438,
         1.02072118,  1.11979732],
       [ 0.20237268,  0.        ,  0.9807679 , ...,  1.09614197,
         1.01776417,  1.01390679],
       [ 1.16745543,  0.9807679 ,  0.        , ...,  0.94071103,
         0.97634081,  0.95014835],
       ..., 
       [ 1.07495438,  1.09614197,  0.94071103, ...,  0.        ,
         0.23309714,  0.29398105],
       [ 1.02072118,  1.01776417,  0.97634081, ...,  0.23309714,
         0.        ,  0.19070761],
       [ 1.11979732,  1.01390679,  0.95014835, ...,  0.29398105,
         0.19070761,  0.        ]])
```


```python
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

knn = 6
index = np.argsort(Y, axis=1)    # sort each row by increasing distance
index = index[:,knn]             
knnDist = Y[np.arange(len(index)),index]  # identify the k-th smallest distance
plt.hist(knnDist)
```

![insert image](/images/big_data/day14/graph3.png)


### Identify the Outliers

```python
outlier = np.flipud(np.argsort(knnDist))
sort_dist = np.flipud(np.sort(knnDist))
p = pd.DataFrame(np.column_stack((outlier,sort_dist)),columns=['index','score'])
p.head()
```

Output:

|   	| index 	|    score 	|
|--:	|------:	|---------:	|
| 0 	|  50.0 	| 0.955814 	|
| 1 	|  53.0 	| 0.945165 	|
| 2 	|  54.0 	| 0.927089 	|
| 3 	|  51.0 	| 0.902902 	|
| 4 	|  52.0 	| 0.888707 	|


### Distance-based Outlier Detection (using scikit-learn)


```python
from sklearn.neighbors import NearestNeighbors
import numpy as np
from scipy.spatial import distance

knn = 6
nbrs = NearestNeighbors(n_neighbors=knn+1, metric=distance.correlation).fit(data.to_numpy())
distances, indices = nbrs.kneighbors(data.to_numpy())
plt.hist(distances[:,knn])
```

![insert image](/images/big_data/day14/graph4.png)


```python
outlier = np.flipud(np.argsort(distances[:,knn]))
sort_dist = np.flipud(np.sort(distances[:,knn]))

p = pd.DataFrame(np.column_stack((outlier,sort_dist)),columns=['index','score'])
p.head()
```

Output:

|   	| index 	|    score 	|
|--:	|------:	|---------:	|
| 0 	|  50.0 	| 0.955814 	|
| 1 	|  53.0 	| 0.945165 	|
| 2 	|  54.0 	| 0.927089 	|
| 3 	|  51.0 	| 0.902902 	|
| 4 	|  52.0 	| 0.888707 	|


### Isolation Forest

```python
import numpy as np
X = np.array([0.1,0.8,0.84,0.87,0.89,0.92,0.95])
plt.plot(X,np.ones(len(X)),'ro')
plt.xlim(-0.1,1.1)
plt.ylim([0.95,1.5])
```

![insert image](/images/big_data/day14/graph5.png)


```python
from sklearn.ensemble import IsolationForest

clf = IsolationForest(n_estimators=100, max_samples=30, contamination=0.1)
clf.fit(data.to_numpy())
score = clf.predict(data.to_numpy())
score
```

Output:

```python
array([ 1,  1,  1,  1,  1,  1, -1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,
        1,  1,  1,  1,  1,  1,  1,  1,  1,  1, -1,  1,  1,  1,  1,  1,  1,
        1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1, -1,
        1, -1, -1, -1])
```


### Excercise

#### Applying Anomaly Detection Algorithms to a Dataset


Load the dataset into a pandas DataFrame object

**Note:** the last column (6) corresponds to the true class of each data point (0: normal, 1: anomaly)

```python

import pandas as pd

data = pd.read_csv('mammography.csv', header = None)
data.head()

```

Output:

|   	|       0 	|       1 	|       2 	|       3 	|       4 	|       5 	| 6 	|
|--:	|--------:	|--------:	|--------:	|--------:	|--------:	|--------:	|--:	|
| 0 	| -0.5378 	| -0.3640 	|  5.3141 	| -0.2190 	|  0.2685 	|  1.1080 	| 0 	|
| 1 	| -0.7844 	| -0.4702 	| -0.5916 	| -0.8596 	| -0.3779 	| -0.9457 	| 0 	|
| 2 	| -0.7844 	| -0.4702 	| -0.5916 	| -0.8596 	| -0.3779 	| -0.9457 	| 0 	|
| 3 	|  0.3804 	| -0.0278 	| -0.4113 	|  0.7261 	|  3.5478 	|  1.2421 	| 0 	|
| 4 	| -0.7844 	| -0.4702 	| -0.5916 	| -0.8596 	| -0.3779 	| -0.9457 	| 0 	|


Draw a scatter plot based on the 4th and 5th column in the DataFrame.

```python
import matplotlib
%matplotlib inline

data.plot.scatter(x=3,y=4,c=6,colormap='cool')
```

Output:

![insert image](/images/big_data/day14/exercise1.png)


Extract the last column of the dataframe and store it in a pandas Series object named *classes*. Remove the last column from the dataframe. Count the number of data points that belong to each class. You should also display the size of the remaining dataframe to prove that you have removed the last column.

```python
classes = data[6]
data = data.drop(6,1)
print('Size of data:', data.shape)
print('Class distribution:')

print(classes.value_counts())
```

Output:

```python
Size of data: (200, 6)
Class distribution:
0    195
1      5
Name: 6, dtype: int64
```

### Anomaly Detection using Mahalanobis Distance 