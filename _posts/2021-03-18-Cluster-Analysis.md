---
title: 'Cluster Analysis'

date: 2021-3-18

header:

  image: "/images/big_data/clustering/james_harden.png"

toc: true
toc_label: "Table of Contents" 
---

## Introduction of Cluster Analysis

**What is Clustering?**

* Clustering is **partitioning** (dividing up) the population of data points into groups that are more similar to other data points in the same group

* Helps identify two qualities of data:

1. Meaningfulness
2. Usefulness


**Why Clustering over Classification?**

* Clustering can adapt to changes made and helps *single out* useful features that differentiate different groups


### Examples of using Clustering

| Data          	| Attribute Set (x)                    	| Clustering Task                        	    |
|---------------	|--------------------------------------	|----------------------------------------	    |
| Customer      	| Demographic and Location Information 	| Group together similar customers       	    |
| Word Document 	| Words                                	| Group Documents based on similar words 	    |
| Ads               | Number of different Ads               | Group together similar people and target them |
|Fantasy Football   | Performance Data                      | Group together similar players to compare     |


### Clustering Methods

* Partitioning Method

- K-Means all all its variants (Fuzzy k-means aka similar words)
- Support Vector Clustering

* Model-Based Method

* Heirarchial Method


## K-Means Clustering

- Unsuprervised Machine Learning Technique

- One of the more popular "clustering" algorithms, K-Means stores centroids that it uses to define clusters. A point is considered to be in a particular cluster if its close to that cluster's centroid than any other centroid.

## K-Means Algorithm

Steps: (**Pseudocode**)

1. Specify the number of k clusters to assign.
2. Randomly pick number of k centroids.
3. Repeat
4.      Expectation: Assign each point to its closet centroids.
5.      Maximization: Compute the new centroid (mean) of each cluster.
6. Until The centroid positions do not change.

Note: The quality of the cluster assignment is determined by computing the **sum of the squared error (SSE)** after the centroids converge.


!['Insert Image'](/images/big_data/clustering/kmeans1.jpg)
!['Insert Image'](/images/big_data/clustering/kmeans2.jpg)
!['Insert Image'](/images/big_data/clustering/kmeans3.jpg)
!['Insert Image'](/images/big_data/clustering/kmeans4.jpg)
!['Insert Image'](/images/big_data/clustering/kmeans5.jpg)
!['Insert Image'](/images/big_data/clustering/kmeans6.jpg)
!['Insert Image'](/images/big_data/clustering/kmeans7.jpg)



### Example of K-Means Algorithm in Python

[sklearn](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html)

Import Libraries

```python
from sklearn.cluster import KMeans
import pandas as pd

from matplotlib import pyplot as plt
%matplotlib inline
```


1. Load the input data

- Using NBA data with player age and salary! (note some salaries are not correct )

```python
data = pd.read_csv("salary_nba.csv")
data
```

Output:

|    	|                 Name 	| Age 	|   Salary 	|
|---:	|---------------------:	|----:	|---------:	|
|  0 	|         Lebron James 	|  36 	| 40000000 	|
|  1 	|          Steph Curry 	|  31 	| 41000000 	|
|  2 	|         Kevin Durant 	|  33 	| 39000000 	|
|  3 	|           Chris Paul 	|  35 	| 41500000 	|
|  4 	|        Anthony Davis 	|  28 	| 33000000 	|
|  5 	|      Dennis Schroder 	|  27 	| 15500000 	|
|  6 	|                  KCP 	|  28 	| 12000000 	|
|  7 	|     Montrezl Harrell 	|  27 	| 16000000 	|
|  8 	|          Alex Caruso 	|  25 	| 14750000 	|
|  9 	|           Kyle Kuzma 	|  27 	| 12960000 	|
| 10 	|      Markieff Morris 	|  25 	|  2300000 	|
| 11 	|     Alfonzo Mckinnie 	|  28 	| 13000000 	|
| 12 	|  Talen Horton-Tucker 	|  20 	|  1500000 	|
| 13 	| Kostas Antetokounmpo 	|  23 	|  1000000 	|
| 14 	|       Devontae Cacok 	|  24 	|  1000000 	|
| 15 	|         Damian Jones 	|  21 	|   785000 	|


Lets plot the Age and Salary

```python
plt.scatter(df.Age,df['Salary'])

plt.xlabel('Age')
plt.ylabel('Salary')
```

Output:

!['Insert Image'](/images/big_data/clustering/nba_graph1.png)

```python
km = KMeans(n_clusters=3)
y_predicted = km.fit_predict(df[['Age','Salary']])
y_predicted
```

Output:

```python
array([0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 1, 2, 2, 2, 2], dtype=int32)
```


```python
df['cluster']=y_predicted
df.head()
```

Output:

|   	|          Name 	| Age 	|   Salary 	| cluster 	|
|--:	|--------------:	|----:	|---------:	|--------:	|
| 0 	|  Lebron James 	|  36 	| 40000000 	|       0 	|
| 1 	|   Steph Curry 	|  31 	| 41000000 	|       0 	|
| 2 	|  Kevin Durant 	|  33 	| 39000000 	|       0 	|
| 3 	|    Chris Paul 	|  35 	| 41500000 	|       0 	|
| 4 	| Anthony Davis 	|  28 	| 33000000 	|       0 	|



```python
km.cluster_centers_
```


```python
df1 = df[df.cluster==0]
df2 = df[df.cluster==1]
df3 = df[df.cluster==2]
plt.scatter(df1.Age,df1['Salary'],color='blue')
plt.scatter(df2.Age,df2['Salary'],color='orange')
plt.scatter(df3.Age,df3['Salary'],color='green')
plt.scatter(km.cluster_centers_[:,0],km.cluster_centers_[:,1],color='purple',marker='*',label='centroid')
plt.xlabel('Age')
plt.ylabel('Salary')
plt.legend()
```

Output:

!['Insert Image'](/images/big_data/clustering/nba_graph2.png)



### Errors with K-Means


* K-Means Clustering was designed to minimize the sum of square error (SSE)
* SSE measures the sum-of-squared distance between every data point **x** to their cluster centroid **c**

* SSE can be used to determine the number of clusters


Lets use the Sum of Squared Error (SEE) to plot an **Elbow Plot**


```python
sse = []
k_range = range(1,10)
for k in k_range:
    km = KMeans(n_clusters=k)
    km.fit(df[['Age','Salary']])
    sse.append(km.inertia_)
```

```python
plt.xlabel('K')
plt.ylabel('Sum of squared error')
plt.plot(k_range,sse)
```

Output:

!['Insert Image'](/images/big_data/clustering/elbow_plot.png)




## More Examples using Clustering (another NBA Example)

Lets look at the Top 50 NBA Scorers!!

<a href="/Files/Data_Series/clustering/top_50_NBA.csv" class="btn btn--success">NBA File Download</a>

```python
data = pd.read_csv('top_50_NBA.csv')
```

```python
kmeans = KMeans(n_clusters = 4, random_state = 98)

x = np.column_stack((data['PTS'], data['USG%']))

kmeans.fit(x)

y_kmeans = kmeans.predict(x)
```

```python
for i, j in zip(df_counting['Player'], y_kmeans):
    print(i, j)
```
Output:

```python
James Harden 2
Paul George 1
Giannis Antetokounmpo 1
Joel Embiid 1
Stephen Curry 1
Kawhi Leonard 1
Devin Booker 1
Kevin Durant 1
Damian Lillard 1
Bradley Beal 1
Kemba Walker 1
Blake Griffin 1
Karl-Anthony Towns 1
Kyrie Irving 1
Donovan Mitchell 1
Zach LaVine 1
Russell Westbrook 1
Klay Thompson 3
Julius Randle 3
LaMarcus Aldridge 3
Jrue Holiday 3
DeMar DeRozan 3
Luka Doncic 3
Mike Conley 3
DAngelo Russell 3
CJ McCollum 3
Nikola Vucevic 3
Buddy Hield 3
Nikola Jokic 3
Tobias Harris 0
Lou Williams 3
Danilo Gallinari 0
John Collins 0
Trae Young 3
Jimmy Butler 0
Kyle Kuzma 0
Khris Middleton 0
Jamal Murray 0
Andrew Wiggins 0
J.J. Redick 0
Tim Hardaway 0
Bojan Bogdanovic 0
Andre Drummond 0
DeAaron Fox 0
Ben Simmons 0
Pascal Siakam 0
Spencer Dinwiddie 0
Jordan Clarkson 3
Collin Sexton 0
Clint Capela 0
```


Graph the **Clustered** **Points** and **Usage**

```python
points_usage_clustered, ax = plt.subplots()

# List of the 4 Clusters

cluster_1 = []
cluster_2 = []
cluster_3 = []
cluster_4 = []

# Add Cluster to each desinated cluster list above
for i in range(len(y_kmeans)):
    if(y_kmeans[i] == 0):
        cluster_1.append(x[i])
    elif(y_kmeans[i] == 1):
        cluster_2.append(x[i])
    elif(y_kmeans[i] == 2):
        cluster_3.append(x[i])
    elif(y_kmeans[i] == 3):
        cluster_4.append(x[i])
        
# vstack stacks things refer to numpy doc --> https://numpy.org/doc/stable/reference/generated/numpy.vstack.html

#vstacks is an array so array([[21.5, 25.6],[points, usage(%)],..])

cluster_1 = np.vstack(cluster_1)
cluster_2 = np.vstack(cluster_2)
cluster_3 = np.vstack(cluster_3)
cluster_4 = np.vstack(cluster_4)


# ax.scatter(x,y, label = 'name of what were plotting', s = size )
ax.scatter(cluster_1[:, 0], cluster_1[:, 1], label = "Cluster 1 (Bottom Top 50)")
ax.scatter(cluster_2[:, 0], cluster_2[:, 1], label = "Cluster 2 (Top Scorers in NBA)")
ax.scatter(cluster_3[:, 0], cluster_3[:, 1], label = "Cluster 3 (James Freaking Harden)")
ax.scatter(cluster_4[:, 0], cluster_4[:, 1], label = "Cluster 4 (Middle Top 50 Scorers) ")

## Heres the centroids! array([[20.56666667, 27.84666667], [x,y],..]) 
centers = kmeans.cluster_centers_

## Now we can plot the centroids (4 of them)
ax.scatter(centers[:, 0], centers[:, 1], c = 'black', s = 200, alpha = .5, label = 'Cluster Center')

# lets plot the Legend, which will include the labels for each of our 4 clusters above
ax.legend(loc ='best', prop = {'size': 8})

## Labeling the x-axis and y-axis
ax.set_xlabel('Points Per Game')
ax.set_ylabel('Usage (%)')

## Naming our Scattered Plot!!!!
points_usage_clustered.suptitle("Clustered Points and Usage")

plt.show()
```

Output:

!['Insert Image'](/images/big_data/clustering/cluster_points.png)



## Limitations of K-Means

**When are there problems with K-Means Clustering?**

* When clusters are of differing Sizes, Densities, and Non-Globular Shapes
* When there are outliers in the Data (James Harden in the example above)



## Cluster Validity

* Cluster Validitation is used to *measure/evaluate* how good our model is!
    - Accuracy, True Positive Rate

**How does one evalute the "goodness" of the resulting Clusters?**



### Issues in Cluster Validation

Typical Questions to answer:

* How many Clusters are there in  the data?
* Are the clusters real or are they nothing more than "accidental" groupings of the data


We need some sort of *statistical framework* to interpet a measure for Cluster Validity


### Rand Index 

**What is the Rand Index? (External Measure)**

* Rand Index or Rand Measure in *statistics* (data clustering), is a measure of the similarity between two *two clustering*.



[Heres the wiki link ](https://en.wikipedia.org/wiki/Rand_index)



### Python Examples of Cluster Validation (using the Rand Index)

<a href="/Files/Data_Series/clustering/diabetes.csv" class="btn btn--success">Diabetes File Download</a>

```python
import pandas as pd

data = pd.read_csv('diabetes.csv',header='infer')
data.head()
```

Output:

|   	| preg 	| plas 	| pres 	| skin 	| insu 	| mass 	|  pedi 	| age 	|           class 	|
|--:	|-----:	|-----:	|-----:	|-----:	|-----:	|-----:	|------:	|----:	|----------------:	|
| 0 	|    6 	|  148 	|   72 	|   35 	|    0 	| 33.6 	| 0.627 	|  50 	| tested_positive 	|
| 1 	|    1 	|   85 	|   66 	|   29 	|    0 	| 26.6 	| 0.351 	|  31 	| tested_negative 	|
| 2 	|    8 	|  183 	|   64 	|    0 	|    0 	| 23.3 	| 0.672 	|  32 	| tested_positive 	|
| 3 	|    1 	|   89 	|   66 	|   23 	|   94 	| 28.1 	| 0.167 	|  21 	| tested_negative 	|
| 4 	|    0 	|  137 	|   40 	|   35 	|  168 	| 43.1 	| 2.288 	|  33 	| tested_positive 	|


```python
Y = (data['class'] == 'tested_positive')*1
X = data.drop('class',axis=1)
```

```python
from sklearn import cluster, metrics

k_means = cluster.KMeans(n_clusters = 2)
k_means.fit(X)
metrics.confusion_matrix(Y,k_means.labels_)
```
Output:

```python
array([[421,  79],
       [182,  86]])
```

```python
metrics.adjusted_rand_score(Y,k_means.labels_)
```

Output:

Adjusted Rand Index: **0.07438695547529094**



## Hierarchical Clustering


* Hierachical Clustering produces *nested clusters* organized as a tree!
* It has the advantage of not having a *pre-defined* number of clusters, but it doesn't work well when we have huge amounts of data!



### Python Examples of Hierarchical Clustering

```python
import pandas as pd

data = pd.read_csv('animals.csv')
names = data['Name']
Y = data['Class']
X = data.drop(['Name','Class'],axis=1)
data
```
Output:

|    	|          Name 	| warmBlooded 	| coldBlooded 	| GiveBirth 	| LayEggs 	| CanSwim 	| CanFly 	| HasLegs 	| HasScales 	|     Class 	|
|---:	|--------------:	|------------:	|------------:	|----------:	|--------:	|--------:	|-------:	|--------:	|----------:	|----------:	|
|  0 	|         human 	|           1 	|           0 	|         1 	|       0 	|       0 	|      0 	|       1 	|         0 	|    mammal 	|
|  1 	|        python 	|           0 	|           1 	|         0 	|       1 	|       0 	|      0 	|       0 	|         1 	|   reptile 	|
|  2 	|        salmon 	|           0 	|           1 	|         0 	|       1 	|       1 	|      0 	|       0 	|         1 	|      fish 	|
|  3 	|         whale 	|           1 	|           0 	|         1 	|       0 	|       1 	|      0 	|       0 	|         0 	|    mammal 	|
|  4 	|          frog 	|           0 	|           1 	|         0 	|       1 	|       1 	|      0 	|       1 	|         0 	| amphibian 	|
|  5 	| komodo dragon 	|           0 	|           1 	|         0 	|       1 	|       0 	|      0 	|       1 	|         1 	|   reptile 	|
|  6 	|           bat 	|           1 	|           0 	|         1 	|       0 	|       0 	|      1 	|       1 	|         0 	|    mammal 	|
|  7 	|        pigeon 	|           1 	|           0 	|         0 	|       1 	|       0 	|      1 	|       1 	|         0 	|      bird 	|
|  8 	|           cat 	|           1 	|           0 	|         1 	|       0 	|       0 	|      0 	|       1 	|         0 	|    mammal 	|
|  9 	| leopard shark 	|           0 	|           1 	|         1 	|       0 	|       1 	|      0 	|       0 	|         1 	|      fish 	|
| 10 	|        turtle 	|           0 	|           1 	|         0 	|       1 	|       1 	|      0 	|       1 	|         1 	|   reptile 	|
| 11 	|       penguin 	|           1 	|           0 	|         0 	|       1 	|       1 	|      0 	|       1 	|         0 	|      bird 	|
| 12 	|     porcupine 	|           1 	|           0 	|         1 	|       0 	|       0 	|      0 	|       1 	|         0 	|    mammal 	|
| 13 	|           eel 	|           0 	|           1 	|         0 	|       1 	|       1 	|      0 	|       0 	|         1 	|      fish 	|
| 14 	|    salamander 	|           0 	|           1 	|         0 	|       1 	|       1 	|      0 	|       1 	|         0 	| amphibian 	|
| 15 	|     alligator 	|           0 	|           1 	|         0 	|       1 	|       1 	|      0 	|       1 	|         1 	|   reptile 	|



Import these *Libraries*

```python
import numpy as np

X.to_numpy()
X
```

Output:

```python
array([[1, 0, 1, 0, 0, 0, 1, 0],
       [0, 1, 0, 1, 0, 0, 0, 1],
       [0, 1, 0, 1, 1, 0, 0, 1],
       [1, 0, 1, 0, 1, 0, 0, 0],
       [0, 1, 0, 1, 1, 0, 1, 0],
       [0, 1, 0, 1, 0, 0, 1, 1],
       [1, 0, 1, 0, 0, 1, 1, 0],
       [1, 0, 0, 1, 0, 1, 1, 0],
       [1, 0, 1, 0, 0, 0, 1, 0],
       [0, 1, 1, 0, 1, 0, 0, 1],
       [0, 1, 0, 1, 1, 0, 1, 1],
       [1, 0, 0, 1, 1, 0, 1, 0],
       [1, 0, 1, 0, 0, 0, 1, 0],
       [0, 1, 0, 1, 1, 0, 0, 1],
       [0, 1, 0, 1, 1, 0, 1, 0],
       [0, 1, 0, 1, 1, 0, 1, 1]])

```
Turns our table into a Matrix!! (**to_numpy()** function)



[Link to Scipy Documentation](https://docs.scipy.org/doc/scipy/reference/generated/scipy.cluster.hierarchy.linkage.html)


scipy.cluster.hierarchy.linkage( y, Method , Metric, optimal_ordering)

**y**: May be either a *1-D condensed distance matrix* or a *2-D array of observation vectors*
**Method**:  Used to compute the distance d(s,t) between the 2 clusters s and t

* method = 'single'
* method = 'complete'
* method = 'average'
* method = 'ward'
* method = 'weighted'
* method = 'centroid'
* method = 'median'

**Metric**: The distance metric to use in the case that y is a collection of observation vectors; ignored otherwise.
**optimal_ordering**: If True, the linkage matrix will be reordered so that the distance between successive leaves is minimal

Note that method, metric and optimal_ordering are all **optional**

**Returns:**

* a hierarchical clustering encoded as a linkage matrix.


**How about hierarchy.dendrogram ?**

[Link to Hierarchy Dendrogram](https://docs.scipy.org/doc/scipy/reference/generated/scipy.cluster.hierarchy.dendrogram.html)

**Parameters**:

* **Z**: The linkage matrix encoding the hierarchical clustering to render as a dendrogram
* **Orientation**: The direction to plot the dendrogram, which can be any of the following strings:

    * top, bottom, left, right
* **labels**: text


```python
from scipy.cluster import hierarchy
import matplotlib.pyplot as plt

%matplotlib inline
from pandas import Series
import numpy as np

Z = hierarchy.linkage(X.to_numpy(), 'complete')

dn = hierarchy.dendrogram(Z,labels=names.tolist(),orientation='left')

```

Output:

!['Insert Image'](/images/big_data/clustering/hierarchy.png)


Lets check to see the number of Clusters given the threshold (t = 1.1)

```python
Z = hierarchy.linkage(X.to_numpy(), 'complete')
labels = hierarchy.fcluster(Z, t = 1.1)
labels
```

Output:

```python
array([1, 4, 5, 2, 3, 4, 1, 1, 1, 2, 6, 1, 1, 5, 3, 6], dtype=int32)
```

**Rand Score**

What is Y again?

```python
Y
```

Output:

```python
0        mammal
1       reptile
2          fish
3        mammal
4     amphibian
5       reptile
6        mammal
7          bird
8        mammal
9          fish
10      reptile
11         bird
12       mammal
13         fish
14    amphibian
15      reptile
Name: Class, dtype: object
```

**Adjusted Rand Score**

adjusted_rand_score(labels_true, labels_predicted)


```python
metrics.adjusted_rand_score(Y,labels)
```

Output:

Rand Score: **0.4411764705882353**

**Adjusting the Threshold to (t=1)**

```python
Z = hierarchy.linkage(X.to_numpy(), 'complete')
labels = hierarchy.fcluster(Z, t=1)
labels
```

Output:

```python
array([1, 5, 6, 3, 4, 5, 1, 2, 1, 3, 7, 2, 1, 6, 4, 7], dtype=int32)
```
**Adjusted Rand Score**

```python
metrics.adjusted_rand_score(Y,labels)
```

Output:

Rand Score: **0.6180555555555556**




## More examples of Clustering....

```python
import pandas as pd

data = pd.read_csv('traffic.csv')
data.head()
```

|   	|      date 	| 0:00 	| 0:05 	| 0:10 	| 0:15 	| 0:20 	| 0:25 	| 0:30 	| 0:35 	| 0:40 	| ... 	| 23:15 	| 23:20 	| 23:25 	| 23:30 	| 23:35 	| 23:40 	| 23:45 	| 23:50 	| 23:55 	|     class 	|
|--:	|----------:	|-----:	|-----:	|-----:	|-----:	|-----:	|-----:	|-----:	|-----:	|-----:	|----:	|------:	|------:	|------:	|------:	|------:	|------:	|------:	|------:	|------:	|----------:	|
| 0 	| 4/10/2005 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	| ... 	|   NaN 	|   NaN 	|   NaN 	|   NaN 	|   NaN 	|   NaN 	|   NaN 	|   NaN 	|   NaN 	|      none 	|
| 1 	| 4/11/2005 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	| ... 	|  12.0 	|   6.0 	|   8.0 	|  11.0 	|   7.0 	|   2.0 	|   3.0 	|   6.0 	|   8.0 	|      none 	|
| 2 	| 4/12/2005 	|  3.0 	|  8.0 	| 10.0 	|  6.0 	|  1.0 	|  4.0 	|  9.0 	|  4.0 	|  6.0 	| ... 	|   4.0 	|  10.0 	|   2.0 	|   6.0 	|   5.0 	|   4.0 	|   5.0 	|   6.0 	|   7.0 	| afternoon 	|
| 3 	| 4/13/2005 	|  6.0 	|  5.0 	|  4.0 	|  4.0 	|  4.0 	|  4.0 	|  4.0 	|  2.0 	| 12.0 	| ... 	|   7.0 	|  15.0 	|  10.0 	|   4.0 	|  10.0 	|   6.0 	|  10.0 	|   6.0 	|  16.0 	|   evening 	|
| 4 	| 4/14/2005 	|  7.0 	|  3.0 	|  6.0 	| 11.0 	|  8.0 	|  6.0 	|  6.0 	| 10.0 	|  4.0 	| ... 	|   5.0 	|   9.0 	|   4.0 	|   4.0 	|   6.0 	|   9.0 	|   5.0 	|  16.0 	|   8.0 	|      none 	|


5 rows × 290 columns


Lets clean up this data!!

```python

X = data.dropt('data', axis = 1 )
y = data['class']
y = y.map({'none': 0, 'afternoon': 1, 'evening': 2})

X = X.drop('class',axis=1)
X.head()
```

|   	| 0:00 	| 0:05 	| 0:10 	| 0:15 	| 0:20 	| 0:25 	| 0:30 	| 0:35 	| 0:40 	| 0:45 	| ... 	| 23:10 	| 23:15 	| 23:20 	| 23:25 	| 23:30 	| 23:35 	| 23:40 	| 23:45 	| 23:50 	| 23:55 	|
|--:	|-----:	|-----:	|-----:	|-----:	|-----:	|-----:	|-----:	|-----:	|-----:	|-----:	|----:	|------:	|------:	|------:	|------:	|------:	|------:	|------:	|------:	|------:	|------:	|
| 0 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	| ... 	|   NaN 	|   NaN 	|   NaN 	|   NaN 	|   NaN 	|   NaN 	|   NaN 	|   NaN 	|   NaN 	|   NaN 	|
| 1 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	|  NaN 	| ... 	|  12.0 	|  12.0 	|   6.0 	|   8.0 	|  11.0 	|   7.0 	|   2.0 	|   3.0 	|   6.0 	|   8.0 	|
| 2 	|  3.0 	|  8.0 	| 10.0 	|  6.0 	|  1.0 	|  4.0 	|  9.0 	|  4.0 	|  6.0 	| 13.0 	| ... 	|  10.0 	|   4.0 	|  10.0 	|   2.0 	|   6.0 	|   5.0 	|   4.0 	|   5.0 	|   6.0 	|   7.0 	|
| 3 	|  6.0 	|  5.0 	|  4.0 	|  4.0 	|  4.0 	|  4.0 	|  4.0 	|  2.0 	| 12.0 	|  2.0 	| ... 	|   7.0 	|   7.0 	|  15.0 	|  10.0 	|   4.0 	|  10.0 	|   6.0 	|  10.0 	|   6.0 	|  16.0 	|
| 4 	|  7.0 	|  3.0 	|  6.0 	| 11.0 	|  8.0 	|  6.0 	|  6.0 	| 10.0 	|  4.0 	|  7.0 	| ... 	|  12.0 	|   5.0 	|   9.0 	|   4.0 	|   4.0 	|   6.0 	|   9.0 	|   5.0 	|  16.0 	|   8.0 	|



Lets replace any *empty (missing values)* with the mean value

```python
mean_value = X.mean()
X = X.fillna(mean_value)
X.head()
```

Output:

|   	|     0:00 	|     0:05 	|      0:10 	|      0:15 	|     0:20 	|     0:25 	|     0:30 	|      0:35 	|     0:40 	|      0:45 	| 23:10 	|     23:15 	|           	|     23:20 	|     23:25 	|     23:30 	|     23:35 	|     23:40 	|     23:45 	|     23:50 	|     23:55 	|
|--:	|---------:	|---------:	|----------:	|----------:	|---------:	|---------:	|---------:	|----------:	|---------:	|----------:	|------:	|----------:	|----------:	|----------:	|----------:	|----------:	|----------:	|----------:	|----------:	|----------:	|----------:	|
| 0 	| 8.472727 	| 7.969697 	|  7.343558 	|  7.208589 	| 7.006135 	| 6.411043 	| 6.349693 	|  6.705521 	|  5.98773 	|  5.460123 	|   ... 	| 14.763636 	| 14.042424 	| 13.551515 	| 12.151515 	| 11.684848 	| 10.345455 	| 10.575758 	|  9.321212 	|  9.351515 	|  8.884848 	|
| 1 	| 8.472727 	| 7.969697 	|  7.343558 	|  7.208589 	| 7.006135 	| 6.411043 	| 6.349693 	|  6.705521 	|  5.98773 	|  5.460123 	|   ... 	| 12.000000 	| 12.000000 	|  6.000000 	|  8.000000 	| 11.000000 	|  7.000000 	|  2.000000 	|  3.000000 	|  6.000000 	|  8.000000 	|
| 2 	| 3.000000 	| 8.000000 	| 10.000000 	|  6.000000 	| 1.000000 	| 4.000000 	| 9.000000 	|  4.000000 	|  6.00000 	| 13.000000 	|   ... 	| 10.000000 	|  4.000000 	| 10.000000 	|  2.000000 	|  6.000000 	|  5.000000 	|  4.000000 	|  5.000000 	|  6.000000 	|  7.000000 	|
| 3 	| 6.000000 	| 5.000000 	|  4.000000 	|  4.000000 	| 4.000000 	| 4.000000 	| 4.000000 	|  2.000000 	| 12.00000 	|  2.000000 	|   ... 	|  7.000000 	|  7.000000 	| 15.000000 	| 10.000000 	|  4.000000 	| 10.000000 	|  6.000000 	| 10.000000 	|  6.000000 	| 16.000000 	|
| 4 	| 7.000000 	| 3.000000 	|  6.000000 	| 11.000000 	| 8.000000 	| 6.000000 	| 6.000000 	| 10.000000 	|  4.00000 	|  7.000000 	|   ... 	| 12.000000 	|  5.000000 	|  9.000000 	|  4.000000 	|  4.000000 	|  6.000000 	|  9.000000 	|  5.000000 	| 16.000000 	|  8.000000 	|



Clustering now

```python
from sklearn import cluster

k_means = cluster.KMeans(n_clusters=3)
k_means.fit(X) 
values = k_means.cluster_centers_
labels = k_means.labels_

```

Confusion Matrix

```python
from sklearn import metrics

metrics.confusion_matrix(y, k_means.labels_)
```

Output:

```python
array([[ 0, 71, 23],
       [ 0,  4, 19],
       [36, 13,  9]])
```


Lets find the Rand Score

```python
metrics.adjusted_rand_score(y,k_means.labels_)
```

Output:

```python
0.3557396125157386
```

Lets plot 

```python
import matplotlib.pyplot as plt
%matplotlib inline

plt.plot(k_means.cluster_centers_.T)
plt.legend(['Cluster 0','Cluster 1','Cluster 2'])
```

Output:

!['Insert Image'](/images/big_data/clustering/time_cluster.png)


