---
title: 'Big Data Analysis Day 8: Predictive Modeling '

date: 2021-3-4

---

**What is Predictive Modeling/Analytics?**

Predictive Modeling/Analytics involves manipulations on data from exisiting data sets with the goal of **identifying some new trends or patterns**, in which are used to *predict* future outcomes and trends.

**What's the difference between Predictive Modeling/Analytics and Machine Learning?**

- Predictive Modeling is the mathematical approach for which we use *statistics* and *past trends* for "future predictions". While Machine Learning uses various ML models to solve complex problems.

**Why is Predictive Analysis Important?**

Well we use historical data to predict future outcomes, thus it improves decision making and helps increase profit rates of business/engineering (KPIs).

Predictive Analysis can be used in many fields (domains) including:

- Online Retail
- Engineering
- Eduction
- Predicting Weather Forecasting
- Social Media Analysis


**What are the Steps to Perform Predictive Analysis?**

1. Define Problem Statement
2. Collect Data
3. Clean Data
4. Data Analysis
5. Build a Predictive Model
6. Validate the Model
7. Deployment of the Model
8. Monitor the Model


**Predictive Modeling**

* The task of predicting the value of a target variable (y) as a function of the predictor variables (X)

    **y = f(X)**


| Task           	| Target Variable              	| Example Applications                                                                        	|
|----------------	|------------------------------	|---------------------------------------------------------------------------------------------	|
| **Regression**    | Quantitative (ratio/interval) | Stock Market Prediction, revenue/sales Forecast, Temperature Prediction, Calorie Prediction 	|
| **Classification**| Qualitative (nominal)        	| Disease Prediction, Image Classification, Twitter Mood Prediction                           	|





**Terminology for Predicitve Modeling**

* **Training Set**: is the set used for *model building*, in which contains a set of labeled examples, including the target variablue values are known

* **Test Set**: is used to predict the target values of the unknown data or it's used to evaluate the performance of the model (if its for evaluation, the target values of test examples must be known)

* **Predictive Model**: An *abstract* representation of the relationship between the predictor and the target variables





**Predictive Modeling Techniques**

**Single Models**

- Decison Tree Methods
- Support Vector Machine/Regression
- Artifical Neural Network


**Ensemble Models**

- Boosting, Random Forest, Bagging


Lets work with a **Decision Tree Classifier**

A Classification Technique is a systematic approach to build a Classification models from an input of data!

A decision tree classifier is organized a series of test questions and conditions in a tree structure.


In a decision tree, the root and internal nodes contain attribute test conditions to “separate” records that have different characteristics, all the terminal node assigned a class label yes or no.

**How do we Build a Decision Tree?**

Building an optimal decision tee is key in decision tree classifiers, there are many efficient algorithms that use Greedy approach/strategy. Greedy Algorithms is an algorithm paradigm that builds up a solution piece-by-piece, which makes locally optimum decisions about what attributes to use for dividing the data.

Examples of different Greedy Algorithms:

1.	Hunts
2.	ID3
3.	C4.5
4.	CART
5.	SPRINT

All 5 of those algorithms are used in Greedy decision tree induction.


**How do we determine the best Attribute test Condition?**

We have to split the “Nodes”. We can do a two-way split or a multi-way split. A two-way split is easy for when there are binary attributes (Yes or No). If there is a Nominal (many names) attributes which could have many values, a test condition can be expressed into a multiway split. For continuous attributes (example of money $0- 1,000,000), we could split into comparison tests ($0-100,000, $100,001-500,000, $500,001-1,000,000) (< & >). Since there are many ways to specify the test conditions from a given training set, we need a measurement to determine the best way to split the records.


