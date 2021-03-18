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

- Unsuprervised Machine Learning Techniue

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


### Example of K-Means Algorithm in Python

[sklearn](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html)


```python
from sklearn import cluster
```

**Steps**

1. Import Pandas and Load the input data

```python
import pandas as pd

data = pd.read_csv('ratings.csv',header=None)
data
```

Output:

The Columns are movie titles and the indexes are user reviews  

|   	| Jaws 	| Star Wars 	| James Bond 	| It 	|
|--:	|-----:	|----------:	|-----------:	|---:	|
| 0 	|    5 	|         5 	|          2 	|  1 	|
| 1 	|    4 	|         5 	|          3 	|  2 	|
| 2 	|    4 	|         4 	|          4 	|  3 	|
| 3 	|    2 	|         2 	|          4 	|  5 	|
| 4 	|    1 	|         2 	|          3 	|  4 	|
| 5 	|    2 	|         1 	|          5 	|  5 	|


2. Create Cluster Object

```python
k_means = cluster.KMeans(n_clusters=2)
```

3. Apply K-Means Clustering to the Data

```python
k_means.fit(data) 
values = k_means.cluster_centers_
pd.DataFrame(values)
```
Ouput:

|   	    |     Jaws 	| Star Wars 	| James Bond 	|       It 	|
|---------: |---------:	|----------:	|-----------:	|---------:	|
| Cluster 1	| 4.333333 	|  4.666667 	|        3.0 	| 2.000000 	|
| Cluster 2	| 1.666667 	|  1.666667 	|        4.0 	| 4.666667 	|


4. Obtain the Centroids and Cluster Labels

```python
labels = k_means.labels_
pd.DataFrame(labels)
```

Output:

|   	| 0 	|
|--:	|--:	|
| 0 	| 1 	|
| 1 	| 1 	|
| 2 	| 1 	|
| 3 	| 0 	|
| 4 	| 0 	|
| 5 	| 0 	|


**Now lets import another csv file**

```python
testdata = pd.read_csv('ratings2.csv',header=None)
testdata
```

Applying cluster to new data points

```python
predicted = k_means.predict(testdata)
pd.DataFrame(predicted)
```

Output:

|   	| 0 	|
|--:	|--:	|
| 0 	| 0 	|
| 1 	| 1 	|
| 2 	| 0 	|
| 3 	| 1 	|
| 4 	| 0 	|




### Errors with K-Means


* K-Means Clustering was designed to minimize the sum of square error (SSE)
* SSE measures the sum-of-squared distance between every data point **x** to their cluster centroid **c**

* SSE can be used to determine the number of clusters

### Limitations of K-Means

**When are there problems with K-Means Clustering?**

* When clusters are of differing Sizes, Densities, and Non-Globular Shapes
* When there are outliers in the Data



## Cluster Validity

### Issues in Cluster Validation


### Python Examples of Cluster Validation


## Hierarchical Clustering


### Python Examples