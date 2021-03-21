---
title: 'Cluster Analysis'

date: 2021-3-18

header:

  image: "/images/big_data/clustering/cluster_points.png"

toc: true
toc_label: "Table of Contents" 
---

## Introduction of Cluster Analysis

**What is Clustering?**

* Clustering is **partitioning** (dividing up) the population of data points into groups that are more similar to other data points in the same group

* Helps identify two qualities of data:

1. Meaningfulness
2. Usefulness
3. u

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

cluster_1 = []
cluster_2 = []
cluster_3 = []
cluster_4 = []

# add Cluster to each desinated cluster list above
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
cluster_1 = np.vstack(cluster_1)
cluster_2 = np.vstack(cluster_2)
cluster_3 = np.vstack(cluster_3)
cluster_4 = np.vstack(cluster_4)

ax.scatter(cluster_1[:, 0], cluster_1[:, 1], label = "Cluster 1 (Bottom Top 50)")
ax.scatter(cluster_2[:, 0], cluster_2[:, 1], label = "Cluster 2 (Top Scorers in NBA)")
ax.scatter(cluster_3[:, 0], cluster_3[:, 1], label = "Cluster 3 (James Freaking Harden)")
ax.scatter(cluster_4[:, 0], cluster_4[:, 1], label = "Cluster 4 (Middle Top 50 Scorers) ")



centers = kmeans.cluster_centers_

ax.scatter(centers[:, 0], centers[:, 1], c = 'black', s = 200, alpha = .5, label = 'Cluster Center')

ax.legend(loc ='best', prop = {'size': 8})

ax.set_xlabel('Points Per Game')
ax.set_ylabel('Usage (%)')

points_usage_clustered.suptitle("Clustered Points and Usage")


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
* Are the clusters real or are they nothing more than accidental groupings of the data


We need some sort of *statistical framework* to interpet a measure fir 

### Python Examples of Cluster Validation

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


* Hierachical Clustering produces nested clusters organized as a tree!


### Python Examples of Hierarchical Clustering

```python
import pandas as pd

data = pd.read_csv('animals.csv',header='infer')
names = data['Name']
Y = data['Class']
X = data.drop(['Name','Class'],axis=1)
data[:10]
```
Output:

|   	|          Name 	| warmBlooded 	| coldBlooded 	| GiveBirth 	| LayEggs 	| CanSwim 	| CanFly 	| HasLegs 	| HasScales 	|     Class 	|
|--:	|--------------:	|------------:	|------------:	|----------:	|--------:	|--------:	|-------:	|--------:	|----------:	|----------:	|
| 0 	|         human 	|           1 	|           0 	|         1 	|       0 	|       0 	|      0 	|       1 	|         0 	|    mammal 	|
| 1 	|        python 	|           0 	|           1 	|         0 	|       1 	|       0 	|      0 	|       0 	|         1 	|   reptile 	|
| 2 	|        salmon 	|           0 	|           1 	|         0 	|       1 	|       1 	|      0 	|       0 	|         1 	|      fish 	|
| 3 	|         whale 	|           1 	|           0 	|         1 	|       0 	|       1 	|      0 	|       0 	|         0 	|    mammal 	|
| 4 	|          frog 	|           0 	|           1 	|         0 	|       1 	|       1 	|      0 	|       1 	|         0 	| amphibian 	|
| 5 	| komodo dragon 	|           0 	|           1 	|         0 	|       1 	|       0 	|      0 	|       1 	|         1 	|   reptile 	|
| 6 	|           bat 	|           1 	|           0 	|         1 	|       0 	|       0 	|      1 	|       1 	|         0 	|    mammal 	|
| 7 	|        pigeon 	|           1 	|           0 	|         0 	|       1 	|       0 	|      1 	|       1 	|         0 	|      bird 	|
| 8 	|           cat 	|           1 	|           0 	|         1 	|       0 	|       0 	|      0 	|       1 	|         0 	|    mammal 	|
| 9 	| leopard shark 	|           0 	|           1 	|         1 	|       0 	|       1 	|      0 	|       0 	|         1 	|      fish 	|



```python
from scipy.cluster import hierarchy
import matplotlib.pyplot as plt
%matplotlib inline
from pandas import Series
import numpy as np

Z = hierarchy.linkage(X.to_numpy(), 'complete')
dn = hierarchy.dendrogram(Z,labels=names.tolist(),orientation='right')

```

Output:

!['Insert Image'](/images/big_data/clustering/hierarchy.png)



```python
Z = hierarchy.linkage(X.to_numpy(), 'complete')
threshold = 1.1
labels = hierarchy.fcluster(Z, threshold)
labels
```

Output:

```python
array([1, 4, 5, 2, 3, 4, 1, 1, 1, 2, 6, 1, 1, 5, 3, 6], dtype=int32)
```

**Rand Score**

```python
metrics.adjusted_rand_score(Y,labels)
```

Output:

Rand Score: **0.4411764705882353**

```python
Z = hierarchy.linkage(X.to_numpy(), 'complete')
threshold = 1.0
labels = hierarchy.fcluster(Z, threshold)
labels
```

Output:

```python
array([1, 5, 6, 3, 4, 5, 1, 2, 1, 3, 7, 2, 1, 6, 4, 7], dtype=int32)
```

```python
metrics.adjusted_rand_score(Y,labels)
```

Output:

Rand Score: **0.6180555555555556**