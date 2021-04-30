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

    ["Insert Equation for User-Based Nearest Neighbor]


#### Similarity Measure

* Numerical measure of **how alike two data instances are**, the higher they're the more alike the instances are

**Examples of Similarity Measures include:**

* Jaccard Similarity
* Cosine Similarity
* Correlation Similarity
* Gaussian RBF Similarity

##### Jaccard Similarity

##### Cosine Similarity

##### Correlation Similarity

##### Gaussian RBF Similarity




### Matrix Factorization

