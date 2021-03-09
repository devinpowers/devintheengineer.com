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

* Problem of learning a mapping function from inputs to outputs called function approximation

    **y = f(X)**


| Task           	| Target Variable              	| Example Applications                                                                        	|
|----------------	|------------------------------	|---------------------------------------------------------------------------------------------	|
| **Regression**    | Quantitative (ratio/interval) | Stock Market Prediction, revenue/sales Forecast, Temperature Prediction, Calorie Prediction 	|
| **Classification**| Qualitative (nominal)        	| Disease Prediction, Image Classification, Twitter Mood Prediction                           	|



Classification is about predicting a label and regression is about predicting a quantity.

**Classification vs Regression**

**Classification** is the task of “classifying” things into sub-categories.

It has two types:

1. Binary Classification:Categorizes given data into two distinct classes

2. Multiclass Classification: The number of classes is more than 2

Involves prediction of Discrete Values

Method of Calculation: Measuring Accuracy 

**Examples of Classification:** Decision Tree, Logestic Regression


**Regression** is the process of finding a model or function for distinguishing the data into continuous real values instead of using classes

Involves prediction Continuous Values

Method of Calculation: Measurement of root mean square error

**Examples of Regression** Regression Tree (random forest) , Linear Regression


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

- It's called/referred to as *decision tree induction*

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

* Using a *diabetes* file to predict if the person will test positive for Diabetes

**Steps**

**Step 1**: Load the data

```python
import pandas as p

col_names = ['pregnant', 'glucose', 'bp', 'skin', 'insulin', 'bmi', 'pedigree', 'age', 'label']
# load dataset
pima = p.read_csv("diabetes.csv", header=None, names=col_names )

pima
```

Output

|     	| pregnant 	| glucose 	|   bp 	| skin 	| insulin 	|  bmi 	| pedigree 	| age 	|           label 	|
|----:	|---------:	|--------:	|-----:	|-----:	|--------:	|-----:	|---------:	|----:	|----------------:	|
|   0 	|     preg 	|    plas 	| pres 	| skin 	|    insu 	| mass 	|     pedi 	| age 	|           class 	|
|   1 	|        6 	|     148 	|   72 	|   35 	|       0 	| 33.6 	|    0.627 	|  50 	| tested_positive 	|
|   2 	|        1 	|      85 	|   66 	|   29 	|       0 	| 26.6 	|    0.351 	|  31 	| tested_negative 	|
|   3 	|        8 	|     183 	|   64 	|    0 	|       0 	| 23.3 	|    0.672 	|  32 	| tested_positive 	|
|   4 	|        1 	|      89 	|   66 	|   23 	|      94 	| 28.1 	|    0.167 	|  21 	| tested_negative 	|
| ... 	|      ... 	|     ... 	|  ... 	|  ... 	|     ... 	|  ... 	|      ... 	| ... 	|             ... 	|
| 764 	|       10 	|     101 	|   76 	|   48 	|     180 	| 32.9 	|    0.171 	|  63 	| tested_negative 	|
| 765 	|        2 	|     122 	|   70 	|   27 	|       0 	| 36.8 	|     0.34 	|  27 	| tested_negative 	|
| 766 	|        5 	|     121 	|   72 	|   23 	|     112 	| 26.2 	|    0.245 	|  30 	| tested_negative 	|
| 767 	|        1 	|     126 	|   60 	|    0 	|       0 	| 30.1 	|    0.349 	|  47 	| tested_positive 	|
| 768 	|        1 	|      93 	|   70 	|   31 	|       0 	| 30.4 	|    0.315 	|  23 	| tested_negative 	|


**Step 2**: Extract the predictor (X) and the Target (y) variables

```python
feature_cols = ['pregnant', 'insulin', 'bmi', 'age','glucose','bp','pedigree']
X = pima[feature_cols] # Features
y = pima.label # Target variable
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

 |     	| pregnant 	| insulin 	|  bmi 	| age 	| glucose 	|  bp 	| pedigree 	|
|----:	|---------:	|--------:	|-----:	|----:	|--------:	|----:	|---------:	|
|  89 	|       15 	|     110 	| 37.1 	|  43 	|     136 	|  70 	|    0.153 	|
| 468 	|        0 	|     100 	| 36.8 	|  25 	|      97 	|  64 	|      0.6 	|
| 551 	|        1 	|       0 	| 27.4 	|  21 	|     116 	|  70 	|    0.204 	|
| 148 	|        2 	|     119 	| 30.5 	|  34 	|     106 	|  64 	|      1.4 	|
| 482 	|        0 	|       0 	| 35.2 	|  29 	|     123 	|  88 	|    0.197 	|
| ... 	|      ... 	|     ... 	|  ... 	| ... 	|     ... 	| ... 	|      ... 	|
| 646 	|        2 	|     440 	| 39.4 	|  30 	|     157 	|  74 	|    0.134 	|
| 716 	|        7 	|     392 	| 33.9 	|  34 	|     187 	|  50 	|    0.826 	|
|  73 	|       13 	|       0 	| 43.4 	|  42 	|     126 	|  90 	|    0.583 	|
| 236 	|        4 	|       0 	| 43.6 	|  26 	|     171 	|  72 	|    0.479 	|
|  38 	|        9 	|       0 	| 32.9 	|  46 	|     102 	|  76 	|    0.665 	|



There are 537 rows in  X_train!

  ```python
 X_test
 ```

 Output:

|     	| pregnant 	| insulin 	|  bmi 	| age 	| glucose 	|  bp 	| pedigree 	|
|----:	|---------:	|--------:	|-----:	|----:	|--------:	|----:	|---------:	|
| 286 	|        7 	|     135 	|   26 	|  51 	|     136 	|  74 	|    0.647 	|
| 102 	|        1 	|       0 	| 26.1 	|  22 	|     151 	|  60 	|    0.179 	|
| 582 	|        6 	|       0 	|   25 	|  27 	|     109 	|  60 	|    0.206 	|
| 353 	|        3 	|       0 	| 34.4 	|  46 	|      61 	|  82 	|    0.243 	|
| 727 	|        1 	|     180 	| 36.1 	|  25 	|     116 	|  78 	|    0.496 	|
| ... 	|      ... 	|     ... 	|  ... 	| ... 	|     ... 	| ... 	|      ... 	|
| 242 	|        4 	|      88 	| 33.1 	|  22 	|      91 	|  70 	|    0.446 	|
| 600 	|        1 	|     120 	| 23.1 	|  26 	|     109 	|  38 	|    0.407 	|
| 651 	|        1 	|     100 	| 25.2 	|  23 	|      91 	|  54 	|    0.234 	|
|  12 	|       10 	|       0 	|   38 	|  34 	|     168 	|  74 	|    0.537 	|
| 215 	|        9 	|     175 	| 34.2 	|  36 	|     112 	|  82 	|     0.26 	|

 
 There are 231 rows in the X_test!


```python
y_train
```

Output:

|     	|                 	|
|-----	|-----------------	|
| 89  	| tested_positive 	|
| 468 	| tested_negative 	|
| 551 	| tested_negative 	|
| 148 	| tested_negative 	|
| 482 	| tested_negative 	|
| ... 	|                 	|
| 646 	| tested_negative 	|
| 716 	| tested_positive 	|
| 73  	| tested_positive 	|
| 236 	| tested_positive 	|
| 38  	| tested_positive 	|

There are 527 rows in  y_train.



```python
y_test
```

Output:

|     	|                 	|
|-----	|-----------------	|
| 286 	| tested_negative 	|
| 102 	| tested_negative 	|
| 582 	| tested_negative 	|
| 353 	| tested_negative 	|
| 727 	| tested_negative 	|
| ... 	|                 	|
| 242 	| tested_negative 	|
| 600 	| tested_negative 	|
| 651 	| tested_negative 	|
| 12  	| tested_positive 	|
| 215 	| tested_positive 	|


There are 231 rows in y_test.

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
Accuracy: 0.6666666666666666
```

We can Visualize the Decision Tree using Scikit-learn's export_graphviz function:

```python
from sklearn import tree
import pydotplus 
dot_data = tree.export_graphviz(clf, out_file=None) 
graph = pydotplus.graph_from_dot_data(dot_data) 
graph.write_pdf("diabetes.pdf") 

from IPython.display import Image
Image(graph.create_png())
```

Output:

![insert image](/images/big_data/predictive_modeling/diabetes_tree.png)


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

    * Which is challenging because a model with low training erro does not guarantee it will have low test error (due to model overfitting problem)

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

Lets Plot

```python
plt.plot(maxdepths,trainAcc,'ro-',maxdepths,testAcc,'bv--')
plt.legend(['Training Accuracy','Test Accuracy'])
```

Output:

Training Accuracy vs Test Accuracy

![insert image](/images/big_data/predictive_modeling/training_plot.png)


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
