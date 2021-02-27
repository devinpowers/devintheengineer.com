---
title: 'Big Data Analysis Day 5: Data Quality and Pandas Library '

date: 2021-2-25

---



Working with **Raw** data

**What are some Data Quality Issues that we might encounter?**

- Noise
- Outliers
- Duplicate Data
- Missing Values

Lets dive into each one...

**Noise**

Noise refers to the incorrect/modified values of data, some data is very stable and possesses little variabilty, while other data swings wildly and unpredictably from one value to another

How do we deal with Noise?

Dealing with noise depends on the type of data, for time series low pass filters are often used, for document data we can use software or lookup dictionary

**Outliers**

Are data objects with charactersitics that are considerbly different than most of the other data objects in the data set!


**Duplicate Data**

- Where data set may include data objects that are duplicates (common problem when merging data from multiple sources)

How do we handle Duplicate Data?



**Missing Values**

Why is there missing values?
- Information/data wasn't collected
- Attributes may not apply to all cases

How do we handle missing values?

- We could remove data objects with missing values
- Ignore the missing values during analysis


One of the best Python libraries with Data Analysis is **Pandas** as we already know

The Pandas Library has two main data structures

1. Series: a one-dimensional array-like object
2. DataFrame: spreadsheet-like data structure containing a collection of ordered columns



**Series**





**DataFrame**