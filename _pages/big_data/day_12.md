---
permalink: /Big_Data/big_data/day_12
title: "Collaborative Filtering"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"

toc: true
toc_label: "Table of Contents" 

  
---
## Questions to Answer:

### What is a Recommender System?

### What is Collaborative Filtering?

### What are the Collaborative Filtering Techniques?


## Recommender System

* Automated systems that *make recommendations* based on the preference of users

* Examples:
  * Amazon or any other online store always makes recommendations of products to buy
  * Netflix or Spotify


### Collaborative Filtering

* is the tech behind *most* recommender systems, which is the *process of filtering information* by soliciting judgements from others to overcome the information overload problem.

![insert image](/images/big_data/collaborative/Collaborative_filtering.gif)


### Collaborative Filtering Techniques

* Collaborative Filtering Techniques are used to predict how well a user will like an item that he/she has not rated given a set of historical preference judgements for a community of users.

#### Nearest Neighbor


* For Nearest Neighbor we need to define the **similarity measure** and **neighborhood size**

  **User-Based Nearest Neighbor** (we've seen this many times before!)

    * The process is given a user *u*, generate a prediction for an item *i* by using the ratings for *i* from users in *u's* neighborhood
    * Where Neighbor is equal to users with similar interests

    ["Insert Equation for User-Based Nearest Neighbor]

  **Item-Based Nearest Neighbour**

    * Given a user *u*, generate a prediction for an item *i* by using a weighted sum of the users *u's* rating for items that are most similar to i.

    ["Insert Equation for Item-Based Nearest Neighbor]


#### Similarity Measure

* Numerical measure of **how alike two data instances are**, the higher they're the more alike the instances are

**Examples of Similarity Measures include:**

* Jaccard Similarity
* Cosine Similarity
* Correlation Similarity
* Gaussian RBF Similarity

##### Jaccard Similarity
["Insert more Notes Here"]
##### Cosine Similarity
["Insert more Notes Here"]
##### Correlation Similarity
["Insert more Notes Here"]
##### Gaussian RBF Similarity
["Insert more Notes Here"]


### Python Example of User-Based Similarity

```python
import pandas as pd

data = pd.read_csv('ratings.csv',header='infer')
data
```

Output:

|   	| Mission Impossible 	| Over the Hedge 	| Back to the Future 	| Harry Potter 	|
|--:	|-------------------:	|---------------:	|-------------------:	|-------------:	|
| 0 	|                  5 	|              3 	|                  4 	|          NaN 	|
| 1 	|                  5 	|              4 	|                  5 	|          5.0 	|
| 2 	|                  2 	|              2 	|                  4 	|          5.0 	|
| 3 	|                  3 	|              1 	|                  1 	|          2.0 	|

Using from the **sklearn** libary!

```python
from sklearn.metrics import pairwise
import pandas as pd
import numpy as np

X = data.to_numpy()
user_similarity = pairwise.rbf_kernel(X[:,:3],gamma=0.2)
usim = pd.DataFrame(user_similarity)
usim
```

Output:

|   	|        0 	|        1 	|        2 	|        3 	|
|--:	|---------:	|---------:	|---------:	|----------	|
| 0 	| 1.000000 	| 0.670320 	| 0.135335 	| 0.033373 	|
| 1 	| 0.670320 	| 1.000000 	| 0.060810 	| 0.003028 	|
| 2 	| 0.135335 	| 0.060810 	| 1.000000 	| 0.110803 	|
| 3 	| 0.033373 	| 0.003028 	| 0.110803 	| 1.000000 	|

```python
avg_ratings = data.mean(axis=1)      # average ratings for each user
avg_ratings
```

Output:

0    4.00
1    4.75
2    3.25
3    1.75
dtype: float64

```python
import numpy as np

ratings = (data['Harry Potter'][1:] - avg_ratings[1:])*usim[0].iloc[1:]
predicted = avg_ratings[0] + (ratings.sum()*1.0/usim[0].iloc[1:].sum())
predicted
```
Output:

**4.4919499466890604**

### Python Example of Item-Based Similarity

```python
item_similarity = pairwise.rbf_kernel(X[1:,:].T,gamma=0.2)
isim = pd.DataFrame(item_similarity)
isim
```

Output:

|   	|        0 	|        1 	|        2 	|        3 	|
|--:	|---------:	|---------:	|---------:	|----------	|
| 0 	| 1.000000 	| 0.367879 	| 0.201897 	| 0.135335 	|
| 1 	| 0.367879 	| 1.000000 	| 0.367879 	| 0.110803 	|
| 2 	| 0.201897 	| 0.367879 	| 1.000000 	| 0.670320 	|
| 3 	| 0.135335 	| 0.110803 	| 0.670320 	| 1.000000 	|



## Another Technique: Matrix Factorization


