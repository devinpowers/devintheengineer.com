---
title: 'Cluster Analysis'

date: 2021-3-18


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





### Limitations of K-Means

**When are there problems with K-Means Clustering?**

* When clusters are of differing Sizes, Densities, and Non-Globular Shapes
* When there are outliers in the Data


## More Examples using Clustering (another NBA Example)

Lets look at the Top 50 NBA Scorers!!






## Cluster Validity

### Issues in Cluster Validation


### Python Examples of Cluster Validation


## Hierarchical Clustering


### Python Examples