---
title: 'Big Data Analysis Day 8: Predictive Modeling '

date: 2021-3-4

---

**What is Predictive Modeling/Analytics?**

Predictive Modeling/Analytics involves manipulations on data from exisiting data sets with the goal of **identifying some new trends or patterns**, in which are used to *predict* future outcomes and trends.

**What's the difference between Predictive Modeling/Analytics and Machine Learning?**

- Predictive Modeling is the **mathematical approach** for which we use **statistics** and **past trends** for "future predictions". While Machine Learning uses various ML models to solve complex problems.

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
5. **Build a Predictive Model**
6. Validate the Model
7. Deployment of the Model
8. Monitor the Model


**Predictive Modeling**

* The task of predicting the value of a target variable (y) as a function of the predictor variables (X)

* Problem of learning a mapping function from inputs to outputs called function approximation

    **y = f(X)**


| Task           	| Target Variable              	| Example Applications                                                                        	|
|----------------	|------------------------------	|---------------------------------------------------------------------------------------------	|
| **Regression**    | Quantitative (ratio/interval) | Stock Market Prediction, revenue/sales Forecast, Temperature Prediction, Calorie Prediction 	|
| **Classification**| Qualitative (nominal)        	| Disease Prediction, Image Classification, Twitter Mood Prediction                           	|



# Classification vs Regression

## Regression

**Regression** is the process of finding a model or function for distinguishing the data into *continuous real values* instead of using classes


**Method of Calculation:** Measurement of root mean square error

**Examples of Regression** Regression Tree (random forest) , Linear Regression


Let's see how **Linear Regression** works


```python
%matplotlib inline
import numpy as np
import matplotlib.pyplot as plt

seed = 1            # seed for random number generation 
numInstances = 200  # number of data instances
np.random.seed(seed)
X = np.random.rand(numInstances,1).reshape(-1,1)
y_true = 2*X + 1 
y = y_true + np.random.normal(size=numInstances).reshape(-1,1)

plt.scatter(X, y,  color='black')
plt.plot(X, y_true, color='blue', linewidth=3)
plt.title('True function: y = 2X + 1')
plt.xlabel('X')
plt.ylabel('y')
```

Output:

![insert image](/images/big_data/predictive_modeling/regression_plot_new.png)


## Classification
**Classification** is the task of *classifying*  things into sub-categories. Definition: Classification is the task of learning a **Target function f** that maps each attribute set **x** to one of the predefined class labels *y*.

![insert image](/images/big_data/predictive_modeling/classification.jpg)

It has **two types:**

1. Binary Classification: Categorizes given data into two distinct classes

2. Multiclass Classification: The number of classes is more than 2

Involves prediction of Discrete Values (individually seperate and distinct)

**Method of Calculation:** Measuring Accuracy 

**Examples of Classification:** Decision Tree, Logestic Regression


## Predictive Modeling

**Terminology for Predicitve Modeling**

* **Training Set**: is the set used for *model building*, in which contains a set of labeled examples, including the target variablue values are known

* **Test Set**: is used to predict the target values of the unknown data or it's used to evaluate the performance of the model (if its for evaluation, the target values of test examples must be known)

* **Predictive Model**: An *abstract* representation of the relationship between the predictor and the target variables

![insert image](/images/big_data/predictive_modeling/training_set.jpg)


**Predictive Modeling Techniques**

**Single Models**

- Decison Tree Methods (examples below!!!)
- Support Vector Machine/Regression
- Artifical Neural Network


**Ensemble Models**

- Boosting, Random Forest, Bagging


Lets work with a **Decision Tree Classifier**

A Classification Technique is a systematic approach to build a Classification models from an input of data!

A decision tree classifier is organized a series of test questions and conditions in a tree structure.


In a decision tree, the root and internal nodes contain attribute test conditions to “separate” records that have different characteristics, all the terminal node assigned a class label yes or no.

**How do we Build a Decision Tree?**

- It's called/referred to as *decision tree induction*

Building an optimal decision tee is key in decision tree classifiers, there are many efficient algorithms that use Greedy approach/strategy. Greedy Algorithms is an algorithm paradigm that builds up a solution piece-by-piece, which makes locally optimum decisions about what attributes to use for dividing the data.

Examples of different Greedy Algorithms:

1.	Hunts
2.	ID3
3.	C4.5
4.	CART
5.	SPRINT

All 5 of those algorithms are used in Greedy decision tree induction.


**How do we Determine the Best Attribute test Condition?**

We have to split the “Nodes”. We can do a two-way split or a multi-way split. A two-way split is easy for when there are binary attributes (Yes or No). If there is a Nominal (many names) attributes which could have many values, a test condition can be expressed into a multiway split. For continuous attributes (example of money $0- 1,000,000), we could split into comparison tests ($0-100,000, $100,001-500,000, $500,001-1,000,000) (< & >). Since there are many ways to specify the test conditions from a given training set, we need a measurement to determine the best way to split the records.

The goal of the best test condition is whether it leads to a homogenous distribution of the nodes, which is the purity of child nodes before and after splitting. The larger the degree of purity, the better the class distribution.


**Measurement of impurity can be determined by:**

1.	Gina Index (used in our example below)
2.	Entropy
3.	Misclassification Error



## Decision Tree Example Notes: 

![insert image](/images/big_data/predictive_modeling/tree1.jpg)
![insert image](/images/big_data/predictive_modeling/tree2.jpg)
![insert image](/images/big_data/predictive_modeling/tree3.jpg)
![insert image](/images/big_data/predictive_modeling/tree4.jpg)
![insert image](/images/big_data/predictive_modeling/tree5.jpg)
![insert image](/images/big_data/predictive_modeling/tree6.jpg)
![insert image](/images/big_data/predictive_modeling/tree7.jpg)
![insert image](/images/big_data/predictive_modeling/tree8.jpg)
![insert image](/images/big_data/predictive_modeling/tree9.jpg)
![insert image](/images/big_data/predictive_modeling/tree10.jpg)


### Example of a Decision Tree Classification

- using sklearn in Python

* Using a *NBA Draft Combine Information* file to predict if the player will be drafted based on picking a few different categories.

Heres the csv file -> [file](/Files/Data_Series/predictive/nba.csv)

**Steps**

**Step 1**: Load the data

```python
import pandas as p

data = p.read_csv('nba_draft_combine_all_years.csv', header = 0)
data
```

Output
|     	|                Player 	| Year 	| Drafted 	| Height (No Shoes) 	| Height (With Shoes) 	| Wingspan 	| Standing reach 	| Vertical (Max) 	| Vertical (Max Reach) 	| Vertical (No Step) 	| Vertical (No Step Reach) 	| Weight 	| Body Fat 	| Hand (Length) 	| Hand (Width) 	| Bench 	| Agility 	| Sprint 	|
|----:	|----------------------:	|-----:	|--------:	|------------------:	|--------------------:	|---------:	|---------------:	|---------------:	|---------------------:	|-------------------:	|-------------------------:	|-------:	|---------:	|--------------:	|-------------:	|------:	|--------:	|-------:	|
|   0 	|         Blake Griffin 	| 2009 	|     Yes 	|             80.50 	|               82.00 	|    83.25 	|          105.0 	|           35.5 	|                140.5 	|               32.0 	|                    137.0 	|  248.0 	|      8.2 	|           NaN 	|          NaN 	|  22.0 	|   10.95 	|   3.28 	|
|   1 	|     Terrence Williams 	| 2009 	|     Yes 	|             77.00 	|               78.25 	|    81.00 	|          103.5 	|           37.0 	|                140.5 	|               30.5 	|                    134.0 	|  213.0 	|      5.1 	|           NaN 	|          NaN 	|   9.0 	|   11.15 	|   3.18 	|
|   2 	|      Gerald Henderson 	| 2009 	|     Yes 	|             76.00 	|               77.00 	|    82.25 	|          102.5 	|           35.0 	|                137.5 	|               31.5 	|                    134.0 	|  215.0 	|      4.4 	|           NaN 	|          NaN 	|   8.0 	|   11.17 	|   3.14 	|
|   3 	|      Tyler Hansbrough 	| 2009 	|     Yes 	|             80.25 	|               81.50 	|    83.50 	|          106.0 	|           34.0 	|                140.0 	|               27.5 	|                    133.5 	|  234.0 	|      8.5 	|           NaN 	|          NaN 	|  18.0 	|   11.12 	|   3.27 	|
|   4 	|            Earl Clark 	| 2009 	|     Yes 	|             80.50 	|               82.25 	|    86.50 	|          109.5 	|           33.0 	|                142.5 	|               28.5 	|                    138.0 	|  228.0 	|      5.2 	|           NaN 	|          NaN 	|   5.0 	|   11.17 	|   3.35 	|
| ... 	|                   ... 	|  ... 	|     ... 	|               ... 	|                 ... 	|      ... 	|            ... 	|            ... 	|                  ... 	|                ... 	|                      ... 	|    ... 	|      ... 	|           ... 	|          ... 	|   ... 	|     ... 	|    ... 	|
| 512 	|             Peter Jok 	| 2017 	|      No 	|             76.25 	|               77.75 	|    80.00 	|          102.0 	|           31.0 	|                133.0 	|               26.5 	|                    128.5 	|  202.0 	|     11.0 	|          8.25 	|         9.50 	|   NaN 	|   11.34 	|   3.41 	|
| 513 	|          Rawle Alkins 	| 2017 	|      No 	|             74.50 	|               75.75 	|    80.75 	|           99.0 	|           40.5 	|                139.5 	|               31.5 	|                    130.5 	|  223.0 	|     11.0 	|          8.75 	|        10.00 	|   NaN 	|   11.99 	|   3.30 	|
| 514 	| Sviatoslav Mykhailiuk 	| 2017 	|      No 	|             78.50 	|               79.50 	|    77.00 	|          100.0 	|           33.0 	|                133.0 	|               27.0 	|                    127.0 	|  220.0 	|     11.4 	|          8.00 	|         9.25 	|   NaN 	|   12.40 	|   3.53 	|
| 515 	|          Thomas Welsh 	| 2017 	|      No 	|             83.50 	|               84.50 	|    84.00 	|          109.5 	|            NaN 	|                  NaN 	|                NaN 	|                      NaN 	|  254.0 	|     10.9 	|          9.00 	|        10.50 	|   NaN 	|     NaN 	|    NaN 	|
| 516 	|          V.J. Beachem 	| 2017 	|      No 	|             78.25 	|               80.00 	|    82.25 	|          104.5 	|           37.0 	|                141.5 	|               30.0 	|                    134.5 	|  193.0 	|      6.8 	|          8.50 	|         9.00 	|   NaN 	|   11.18 	|   3.26 	|


**Step 2** Lets clean this data because there are missing values, here are the columns were intrested in using!

```python
feature_columns = ["Height (No Shoes)", "Wingspan", "Standing reach","Vertical (Max)", "Weight", "Agility", "Sprint"] 
update_data = data[feature_columns]
update_data
```

Output:

|     	| Height (No Shoes) 	| Wingspan 	| Standing reach 	| Vertical (Max) 	| Weight 	| Agility 	| Sprint 	|
|----:	|------------------:	|---------:	|---------------:	|---------------:	|-------:	|--------:	|-------:	|
|   0 	|             80.50 	|    83.25 	|          105.0 	|           35.5 	|  248.0 	|   10.95 	|   3.28 	|
|   1 	|             77.00 	|    81.00 	|          103.5 	|           37.0 	|  213.0 	|   11.15 	|   3.18 	|
|   2 	|             76.00 	|    82.25 	|          102.5 	|           35.0 	|  215.0 	|   11.17 	|   3.14 	|
|   3 	|             80.25 	|    83.50 	|          106.0 	|           34.0 	|  234.0 	|   11.12 	|   3.27 	|
|   4 	|             80.50 	|    86.50 	|          109.5 	|           33.0 	|  228.0 	|   11.17 	|   3.35 	|
| ... 	|               ... 	|      ... 	|            ... 	|            ... 	|    ... 	|     ... 	|    ... 	|
| 512 	|             76.25 	|    80.00 	|          102.0 	|           31.0 	|  202.0 	|   11.34 	|   3.41 	|
| 513 	|             74.50 	|    80.75 	|           99.0 	|           40.5 	|  223.0 	|   11.99 	|   3.30 	|
| 514 	|             78.50 	|    77.00 	|          100.0 	|           33.0 	|  220.0 	|   12.40 	|   3.53 	|
| 515 	|             83.50 	|    84.00 	|          109.5 	|            NaN 	|  254.0 	|     NaN 	|    NaN 	|
| 516 	|             78.25 	|    82.25 	|          104.5 	|           37.0 	|  193.0 	|   11.18 	|   3.26 	|


Now lets check for missing values!!!

```python
update_data.describe()
```

|       	| Height (No Shoes) 	|   Wingspan 	| Standing reach 	| Vertical (Max) 	|     Weight 	|    Agility 	|     Sprint 	|
|------:	|------------------:	|-----------:	|---------------:	|---------------:	|-----------:	|-----------:	|-----------:	|
| count 	|        517.000000 	| 517.000000 	|     517.000000 	|     450.000000 	| 516.000000 	| 444.000000 	| 446.000000 	|
|  mean 	|         77.609284 	|  82.497292 	|     103.275629 	|      35.136667 	| 214.833333 	|  11.330248 	|   3.299664 	|
|   std 	|          3.287633 	|   3.943068 	|       4.897515 	|       3.561688 	|  24.683537 	|   0.563144 	|   0.128422 	|
|   min 	|         68.250000 	|  70.000000 	|      88.500000 	|      25.000000 	| 149.000000 	|  10.070000 	|   3.010000 	|
|   25% 	|         75.250000 	|  79.750000 	|     100.000000 	|      32.500000 	| 196.000000 	|  10.940000 	|   3.200000 	|
|   50% 	|         77.750000 	|  82.500000 	|     103.500000 	|      35.000000 	| 213.500000 	|  11.255000 	|   3.280000 	|
|   75% 	|         80.000000 	|  85.500000 	|     107.000000 	|      37.500000 	| 232.000000 	|  11.660000 	|   3.380000 	|
|   max 	|         85.250000 	|  92.500000 	|     115.000000 	|      44.500000 	| 303.000000 	|  13.440000 	|   3.810000 	|



We can see the count for the total players is 517, and in different columns like Vertical, Weight, Agility, and Sprint here is missing data. Ill just insert the **Median** value for the missing values.

```python
## Vertical Max

update_data['Vertical (Max)'] = update_data['Vertical (Max)'].fillna(update_data['Vertical (Max)'].median())

## Weight

update_data['Weight'] = update_data['Weight'].fillna(update_data['Weight'].median())

## Agility

update_data['Agility'] = update_data['Agility'].fillna(update_data['Agility'].median())


## Sprint

update_data['Sprint'] = update_data['Sprint'].fillna(update_data['Sprint'].median())

```

Now all the Columns are filled in, no more missing data!

```python
update_data
```

Output:

|     	| Height (No Shoes) 	| Wingspan 	| Standing reach 	| Vertical (Max) 	| Weight 	| Agility 	| Sprint 	|
|----:	|------------------:	|---------:	|---------------:	|---------------:	|-------:	|--------:	|-------:	|
|   0 	|             80.50 	|    83.25 	|          105.0 	|           35.5 	|  248.0 	|  10.950 	|   3.28 	|
|   1 	|             77.00 	|    81.00 	|          103.5 	|           37.0 	|  213.0 	|  11.150 	|   3.18 	|
|   2 	|             76.00 	|    82.25 	|          102.5 	|           35.0 	|  215.0 	|  11.170 	|   3.14 	|
|   3 	|             80.25 	|    83.50 	|          106.0 	|           34.0 	|  234.0 	|  11.120 	|   3.27 	|
|   4 	|             80.50 	|    86.50 	|          109.5 	|           33.0 	|  228.0 	|  11.170 	|   3.35 	|
| ... 	|               ... 	|      ... 	|            ... 	|            ... 	|    ... 	|     ... 	|    ... 	|
| 512 	|             76.25 	|    80.00 	|          102.0 	|           31.0 	|  202.0 	|  11.340 	|   3.41 	|
| 513 	|             74.50 	|    80.75 	|           99.0 	|           40.5 	|  223.0 	|  11.990 	|   3.30 	|
| 514 	|             78.50 	|    77.00 	|          100.0 	|           33.0 	|  220.0 	|  12.400 	|   3.53 	|
| 515 	|             83.50 	|    84.00 	|          109.5 	|           35.0 	|  254.0 	|  11.255 	|   3.28 	|
| 516 	|             78.25 	|    82.25 	|          104.5 	|           37.0 	|  193.0 	|  11.180 	|   3.26 	|



**Step 3**: Extract the predictor (X) and the Target (y) variables

```python
X = update_data
y = data["Drafted"]

```

Now that we have the data split.

**Step 3**: Divide the data into training and test sets


```python
from sklearn.tree import DecisionTreeClassifier 
from sklearn.model_selection import train_test_split
from sklearn import metrics 
```

```python
 X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=1) 
 ```

 Note: test_size 0.3 means that 70% training and 30% test

 Lets look at X_train,X_test, y_train, and y_test

 ```python
 X_train
 ```

 Output:

|     	| Height (No Shoes) 	| Wingspan 	| Standing reach 	| Vertical (Max) 	| Weight 	| Agility 	| Sprint 	|
|----:	|------------------:	|---------:	|---------------:	|---------------:	|-------:	|--------:	|-------:	|
|  13 	|             79.75 	|    81.25 	|          106.5 	|           32.5 	|  211.0 	|  11.150 	|   3.28 	|
|  61 	|             76.75 	|    80.50 	|          104.0 	|           35.5 	|  208.0 	|  11.860 	|   3.19 	|
| 453 	|             75.25 	|    81.75 	|           97.5 	|           35.5 	|  212.0 	|  10.770 	|   3.45 	|
|  39 	|             71.25 	|    74.00 	|           95.0 	|           33.0 	|  175.0 	|  10.870 	|   3.10 	|
| 373 	|             76.50 	|    80.25 	|          100.5 	|           34.5 	|  209.0 	|  11.255 	|   3.27 	|
| ... 	|               ... 	|      ... 	|            ... 	|            ... 	|    ... 	|     ... 	|    ... 	|
| 129 	|             76.00 	|    81.75 	|          101.5 	|           35.5 	|  198.0 	|  11.200 	|   3.09 	|
| 144 	|             78.50 	|    85.25 	|          106.5 	|           30.5 	|  242.0 	|  12.430 	|   3.46 	|
|  72 	|             75.75 	|    81.00 	|          101.0 	|           40.0 	|  203.0 	|  11.380 	|   3.15 	|
| 235 	|             79.50 	|    86.50 	|          106.5 	|           38.0 	|  236.0 	|  11.820 	|   3.52 	|
|  37 	|             72.50 	|    75.75 	|           97.0 	|           31.0 	|  193.0 	|  10.990 	|   3.22 	|


There are 361 rows in  X_train!

  ```python
 X_test
 ```

 Output:

|     	| Height (No Shoes) 	| Wingspan 	| Standing reach 	| Vertical (Max) 	| Weight 	| Agility 	| Sprint 	|
|----:	|------------------:	|---------:	|---------------:	|---------------:	|-------:	|--------:	|-------:	|
| 270 	|             73.00 	|    76.00 	|          97.50 	|           35.0 	|  179.0 	|  11.255 	|   3.28 	|
|  90 	|             78.75 	|    79.75 	|         103.00 	|           34.5 	|  211.0 	|  11.730 	|   3.22 	|
| 133 	|             82.00 	|    87.75 	|         109.50 	|           36.0 	|  217.0 	|  11.880 	|   3.35 	|
| 221 	|             81.75 	|    87.50 	|         111.50 	|           35.0 	|  230.0 	|  11.255 	|   3.28 	|
| 224 	|             76.50 	|    79.00 	|         101.00 	|           37.5 	|  199.0 	|  10.680 	|   3.25 	|
| ... 	|               ... 	|      ... 	|            ... 	|            ... 	|    ... 	|     ... 	|    ... 	|
| 494 	|             75.00 	|    78.50 	|          99.50 	|           35.0 	|  185.0 	|  11.380 	|   3.35 	|
|  95 	|             76.00 	|    78.75 	|         101.75 	|           32.0 	|  207.0 	|  11.430 	|   3.17 	|
| 122 	|             79.75 	|    84.25 	|         106.50 	|           30.5 	|  247.0 	|  12.740 	|   3.45 	|
| 165 	|             75.25 	|    80.50 	|          98.00 	|           36.5 	|  212.0 	|  11.360 	|   3.37 	|
|  23 	|             80.75 	|    85.00 	|         107.00 	|           35.0 	|  240.0 	|  11.980 	|   3.14 	|

 
 There are 156 rows in the X_test!


```python
y_train
```

Output:
|                                           	|     	|
|-------------------------------------------	|-----	|
| 13                                        	| Yes 	|
| 61                                        	| Yes 	|
| 453                                       	| No  	|
| 39                                        	| Yes 	|
| 373                                       	| No  	|
| ...                                       	|     	|
| 129                                       	| Yes 	|
| 144                                       	| No  	|
| 72                                        	| Yes 	|
| 235                                       	| Yes 	|
| 37                                        	| Yes 	|
| Name: Drafted, Length: 361, dtype: object 	|     	|

There are 361 rows in  y_train.



```python
y_test
```

Output:

|                                           	|     	|
|-------------------------------------------	|-----	|
| 270                                       	| No  	|
| 90                                        	| Yes 	|
| 133                                       	| Yes 	|
| 221                                       	| Yes 	|
| 224                                       	| Yes 	|
| ...                                       	|     	|
| 494                                       	| No  	|
| 95                                        	| No  	|
| 122                                       	| Yes 	|
| 165                                       	| Yes 	|
| 23                                        	| Yes 	|
| Name: Drafted, Length: 156, dtype: object 	|     	|

There are 156 rows in y_test.

**Step 4**: Build the decision tree model and apply it to the test data
```python
from sklearn import tree
clf = DecisionTreeClassifier()
clf = clf.fit(X_train,y_train)
y_pred = clf.predict(X_test)
```


**Step 5**: Evaluate the accuracy of the model on the test data

```python
from sklearn.metrics import accuracy_score

print("Accuracy:",metrics.accuracy_score(y_test, y_pred))
```

Output:

```python
Accuracy: 0.6794871794871795
```

We can Visualize the Decision Tree using Scikit-learn's export_graphviz function:

```python
from sklearn import tree
import pydotplus 
dot_data = tree.export_graphviz(clf, out_file=None) 
graph = pydotplus.graph_from_dot_data(dot_data) 
graph.write_pdf("NBA_Draft_Prediction.pdf") 

from IPython.display import Image
Image(graph.create_png())
```

Output:

![insert image](/images/big_data/predictive_modeling/NBA_tree.png)


### Model Evaluation


- Alternative Measures of Classification


**F-Measure:** (or F-Score) is a measure of a test’s accuracy 

**Area under ROC Curve**

https://youtu.be/4jRBRDbJemM

**ROC Curve**

**Python Example**

```python
from sklearn.metrics import confusion_matrix

cm = confusion_matrix(Y_test, Y_pred, labels=['tested_negative','tested_positive'])
cm
```

Output:

```python
array([[284, 119],
       [ 79, 133]])
```

```python
from sklearn.metrics import f1_score

f1 = f1_score(Y_test,Y_pred,labels=['tested_negative','tested_positive'],pos_label='tested_positive')
f1
```

Output:

```python
0.5732758620689655
```

```python
Y_prob = clf.predict_proba(X_test)
Y_prob
```

Output:

```python
array([[0.33333333, 0.66666667],
       [1.        , 0.        ],
       [0.33333333, 0.66666667],
       ...,
       [0.88888889, 0.11111111],
       [0.33333333, 0.66666667],
       [0.33333333, 0.66666667]])
```

```python
import matplotlib.pyplot as plt

from sklearn.metrics import roc_curve, auc
%matplotlib inline

true_labels = (Y_test == 'tested_positive');

fpr, tpr, thresholds = roc_curve(true_labels, Y_prob[:,1])
roc_auc = auc(fpr, tpr)
plt.plot(fpr, tpr)

```

Output:

![insert image](/images/big_data/predictive_modeling/roc_curve.png)


**Holdout Method**



**5-Fold Cross Validation Method**
```python
from sklearn.model_selection import cross_val_score
clf = tree.DecisionTreeClassifier(max_depth=3)
scores = cross_val_score(clf, X, Y, cv=5)
scores
```

Output:

```python
array([0.72727273, 0.72077922, 0.74025974, 0.7124183 , 0.74509804])
```

```python
print("Accuracy: %0.2f (+/- %0.2f)" % (scores.mean(), scores.std() * 2))
```

Output:

```python
Accuracy: 0.73 (+/- 0.02)
```





### Extras

```python
import pandas as p

data = p.read_csv('vehicle.csv',header=0)
data.head()
```

Output:

|   	| compactness 	| circularity 	| distance_circularity 	| radius_ratio 	| pr_axis_aspect_ratio 	| max_length_aspect_ratio 	| scatter_ratio 	| elongatedness 	| pr_axisrectangular 	| lengthrectangular 	| majorvariance 	| minorvariance 	| gyrationradius 	| majorskewness 	| minorskewness 	| minorkurtosis 	| majorkurtosis 	| hollows_ratio 	| class 	|
|--:	|------------:	|------------:	|---------------------:	|-------------:	|---------------------:	|------------------------:	|--------------:	|--------------:	|-------------------:	|------------------:	|--------------:	|--------------:	|---------------:	|--------------:	|--------------:	|--------------:	|--------------:	|--------------:	|------:	|
| 0 	|          95 	|          43 	|                   96 	|          202 	|                   65 	|                      10 	|           189 	|            35 	|                 22 	|               143 	|           217 	|           534 	|            166 	|            71 	|             6 	|            27 	|           190 	|           197 	|  opel 	|
| 1 	|          96 	|          52 	|                  104 	|          222 	|                   67 	|                       9 	|           198 	|            33 	|                 23 	|               163 	|           217 	|           589 	|            226 	|            67 	|            12 	|            20 	|           192 	|           201 	|  opel 	|
| 2 	|         107 	|          52 	|                  101 	|          218 	|                   64 	|                      11 	|           202 	|            33 	|                 23 	|               164 	|           219 	|           610 	|            192 	|            65 	|            17 	|             2 	|           197 	|           206 	|  opel 	|
| 3 	|          97 	|          37 	|                   78 	|          181 	|                   62 	|                       8 	|           161 	|            41 	|                 20 	|               131 	|           182 	|           389 	|            117 	|            62 	|             2 	|            28 	|           203 	|           211 	|  opel 	|
| 4 	|          96 	|          54 	|                  104 	|          175 	|                   58 	|                      10 	|           215 	|            31 	|                 24 	|               175 	|           221 	|           682 	|            222 	|            75 	|            13 	|            23 	|           186 	|           194 	|  opel 	|



```python
data[['compactness','circularity','distance_circularity','radius_ratio']].corr()
```

Output:

|                      	| compactness 	| circularity 	| distance_circularity 	| radius_ratio 	|
|---------------------:	|------------:	|------------:	|---------------------:	|-------------:	|
|          compactness 	|    1.000000 	|    0.692869 	|             0.792444 	|     0.691659 	|
|          circularity 	|    0.692869 	|    1.000000 	|             0.798492 	|     0.622778 	|
| distance_circularity 	|    0.792444 	|    0.798492 	|             1.000000 	|     0.771644 	|
|         radius_ratio 	|    0.691659 	|    0.622778 	|             0.771644 	|     1.000000 	|



**Histogram**

```python
%matplotlib inline
data['compactness'].hist()
```
![insert image](/images/big_data/predictive_modeling/pred_hist.png)

**Box Plot**

```python
data[['compactness','circularity','distance_circularity','radius_ratio']].boxplot()
```
![insert image](/images/big_data/predictive_modeling/box_plot_pred.png)



```python
from sklearn.model_selection import train_test_split

Y = data['class']
X = data.drop('class',axis=1)
X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.23, random_state=1)
```

```python
Y
```

Output:

|     	|      	|
|-----	|------	|
| 0   	| opel 	|
| 1   	| opel 	|
| 2   	| opel 	|
| 3   	| opel 	|
| 4   	| opel 	|
| ... 	|      	|
| 841 	| van  	|
| 842 	| van  	|
| 843 	| van  	|
| 844 	| van  	|
| 845 	| van  	|



# Model Selection and Overfitting

Model Selection


**What is Model Overfitting?**

*	Model Overfitting is error that occur when a function is too closely fit to a *limited set of data points*

* Too many details and noise

* The goal of Predictive Modeling is to build a model with low training and test errors

* Which is challenging because a model with low training errors does not guarantee it will have low test error (due to model overfitting problem)

An example of Model Overfitting:

```python
import numpy as np
import matplotlib.pyplot as plt
from numpy.random import random

%matplotlib inline

N = 1500

mean1 = [6, 14]
mean2 = [10, 6]
mean3 = [14, 14]
cov = [[3.5, 0], [0, 3.5]]  # diagonal covariance

np.random.seed(50)
x1, y1 = np.random.multivariate_normal(mean1, cov, N//6).T
x2, y2 = np.random.multivariate_normal(mean2, cov, N//6).T
x3, y3 = np.random.multivariate_normal(mean3, cov, N//6).T
x4 = 20*np.random.random(N//2)
y4 = 20*np.random.random(N//2)

plt.plot(x1,y1,'ro',x2,y2,'ro',x3,y3,'ro',x4,y4,'g+',ms=4)
```

Output:

![insert image](/images/big_data/predictive_modeling/model_overfitting.png)


## Building Trees of Different Sizes


```python
from sklearn import tree
from sklearn.metrics import accuracy_score

maxdepths = [2,3,4,5,6,7,8,9,10,15,20,25,30,35,40,45,50]

trainAcc = np.zeros(len(maxdepths))
testAcc = np.zeros(len(maxdepths))
index = 0

for depth in maxdepths:
    clf = tree.DecisionTreeClassifier(max_depth=depth)
    clf = clf.fit(X_train, Y_train)
    Y_predTrain = clf.predict(X_train)
    Y_predTest = clf.predict(X_test)
    trainAcc[index] = accuracy_score(Y_train, Y_predTrain)
    testAcc[index] = accuracy_score(Y_test, Y_predTest)
    index += 1
```



**Lets plot a Tree with MaxDepth = 4**

```python
depth = 4
clf = tree.DecisionTreeClassifier(max_depth=depth)
clf = clf.fit(X_train, Y_train)
Y_predTrain = clf.predict(X_train)
Y_predTest = clf.predict(X_test)
AccTrain = accuracy_score(Y_train, Y_predTrain)
AccTest = accuracy_score(Y_test, Y_predTest)
[AccTrain, AccTest]
```

Output:

```python
[0.8888888888888888, 0.6959349593495935]
```

Accuracy Training = 88.88%

Accuracy Test = 69.59%


**Lets Plot the Tree with Depth = 4**

```python
import pydotplus 
from IPython.display import Image

dot_data = tree.export_graphviz(clf, out_file=None) 
graph = pydotplus.graph_from_dot_data(dot_data) 
Image(graph.create_png())
```

Output:

![insert image](/images/big_data/predictive_modeling/tree_4.png)


**Lets plot a Tree with MaxDepth = 20**


```python
depth = 20
clf = tree.DecisionTreeClassifier(max_depth=depth)
clf = clf.fit(X_train, Y_train)
Y_predTrain = clf.predict(X_train)
Y_predTest = clf.predict(X_test)
AccTrain = accuracy_score(Y_train, Y_predTrain)
AccTest = accuracy_score(Y_test, Y_predTest)
[AccTrain, AccTest]
```

Output:

```python
[1.0, 0.640650406504065]
```


Accuracy Training = 100%

Accuracy Test = 64.07%

**Lets Plot the Tree with Depth = 20**

```python
import pydotplus 
from IPython.display import Image

dot_data = tree.export_graphviz(clf, out_file=None) 
graph = pydotplus.graph_from_dot_data(dot_data) 
Image(graph.create_png())
```

![insert image](/images/big_data/predictive_modeling/tree_20.png)




### Lets Plot Model Overfitting and Underfitting

```python
plt.plot(maxdepths,trainAcc,'ro-',maxdepths,testAcc,'bv--')
plt.legend(['Training Accuracy','Test Accuracy'])
```

Output:

Model Overfitting and Underfitting

![insert image](/images/big_data/predictive_modeling/training_plot.png)


**Defintions:**

     * Underfitting: When the model is too simple

     * Overfitting: When the model is too complex 


### Mammal Classification Problem



```python
import pandas as pd

data = pd.read_csv('vertebrate.csv',header='infer')
data
```

Output:

|    	|          Name 	| Body Temperature 	| Skin Cover 	| Gives Birth 	| Aquatic Creature 	| Aerial Creature 	| Has Legs 	| Hibernates 	| Class Label 	|
|---:	|--------------:	|-----------------:	|-----------:	|------------:	|-----------------:	|----------------:	|---------:	|-----------:	|------------:	|
|  0 	|         human 	|     warm-blooded 	|       hair 	|         yes 	|               no 	|              no 	|      yes 	|         no 	|      mammal 	|
|  1 	|        python 	|     cold-blooded 	|     scales 	|          no 	|               no 	|              no 	|       no 	|        yes 	|     reptile 	|
|  2 	|        salmon 	|     cold-blooded 	|     scales 	|          no 	|              yes 	|              no 	|       no 	|         no 	|        fish 	|
|  3 	|         whale 	|     warm-blooded 	|       hair 	|         yes 	|              yes 	|              no 	|       no 	|         no 	|      mammal 	|
|  4 	|          frog 	|     cold-blooded 	|       none 	|          no 	|             semi 	|              no 	|      yes 	|        yes 	|   amphibian 	|
|  5 	| komodo dragon 	|     cold-blooded 	|     scales 	|          no 	|               no 	|              no 	|      yes 	|         no 	|     reptile 	|
|  6 	|           bat 	|     warm-blooded 	|       hair 	|         yes 	|               no 	|             yes 	|      yes 	|        yes 	|      mammal 	|
|  7 	|        pigeon 	|     warm-blooded 	|   feathers 	|          no 	|               no 	|             yes 	|      yes 	|         no 	|        bird 	|
|  8 	|           cat 	|     warm-blooded 	|        fur 	|         yes 	|               no 	|              no 	|      yes 	|         no 	|      mammal 	|
|  9 	| leopard shark 	|     cold-blooded 	|     scales 	|         yes 	|              yes 	|              no 	|       no 	|         no 	|        fish 	|
| 10 	|        turtle 	|     cold-blooded 	|     scales 	|          no 	|             semi 	|              no 	|      yes 	|         no 	|     reptile 	|
| 11 	|       penguin 	|     warm-blooded 	|   feathers 	|          no 	|             semi 	|              no 	|      yes 	|         no 	|        bird 	|
| 12 	|     porcupine 	|     warm-blooded 	|     quills 	|         yes 	|               no 	|              no 	|      yes 	|        yes 	|      mammal 	|
| 13 	|           eel 	|     cold-blooded 	|     scales 	|          no 	|              yes 	|              no 	|       no 	|         no 	|        fish 	|
| 14 	|    salamander 	|     cold-blooded 	|       none 	|          no 	|             semi 	|              no 	|      yes 	|        yes 	|   amphibian 	|
| 15 	|  gila monster 	|     cold-blooded 	|     scales 	|          no 	|               no 	|              no 	|      yes 	|        yes 	|         NaN 	|

## Lessons on Overfitting



## Other Predictive Modeling Techniques



## Nearest-Neighbor Methods


    * Linear Method
    * Nonlinear Method
    * Ensemble Methods




## Other Issues in Classification

