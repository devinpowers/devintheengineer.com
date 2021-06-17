---
permalink: /Big_Data/big_data/pga_golf
title: "Golf Project"
author_profile: true

header:
  image: "/images/big_data/golf/tiger.jpeg"

toc: true
toc_label: "Table of Contents" 

---

Lets import the Libraries we need and the data (csv) file!

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```


```python
df = pd.read_csv("golfdata.csv")

# Return first 5 rows
df.head()
```

**Output:**

|   	|    Player Name 	| Rounds 	| Fairway Percentage 	| Year 	| Avg Distance 	|   gir 	| Average Putts 	| Average Scrambling 	| Average Score 	| Points 	| Wins 	| Top 10 	| Average SG Putts 	| Average SG Total 	| SG:OTT 	| SG:APR 	| SG:ARG 	|      Money 	|
|--:	|---------------:	|-------:	|-------------------:	|-----:	|-------------:	|------:	|--------------:	|-------------------:	|--------------:	|-------:	|-----:	|-------:	|-----------------:	|-----------------:	|-------:	|-------:	|-------:	|-----------:	|
| 0 	| Henrik Stenson 	|   60.0 	|              75.19 	| 2018 	|        291.5 	| 73.51 	|         29.93 	|              60.67 	|        69.617 	|    868 	|  NaN 	|    5.0 	|           -0.207 	|            1.153 	|  0.427 	|  0.960 	| -0.027 	| $2,680,487 	|
| 1 	|    Ryan Armour 	|  109.0 	|              73.58 	| 2018 	|        283.5 	| 68.22 	|         29.31 	|              60.13 	|        70.758 	|  1,006 	|  1.0 	|    3.0 	|           -0.058 	|            0.337 	| -0.012 	|  0.213 	|  0.194 	| $2,485,203 	|
| 2 	|    Chez Reavie 	|   93.0 	|              72.24 	| 2018 	|        286.5 	| 68.67 	|         29.12 	|              62.27 	|        70.432 	|  1,020 	|  NaN 	|    3.0 	|            0.192 	|            0.674 	|  0.183 	|  0.437 	| -0.137 	| $2,700,018 	|
| 3 	|     Ryan Moore 	|   78.0 	|              71.94 	| 2018 	|        289.2 	| 68.80 	|         29.17 	|              64.16 	|        70.015 	|    795 	|  NaN 	|    5.0 	|           -0.271 	|            0.941 	|  0.406 	|  0.532 	|  0.273 	| $1,986,608 	|
| 4 	|   Brian Stuard 	|  103.0 	|              71.44 	| 2018 	|        278.9 	| 67.12 	|         29.11 	|              59.23 	|        71.038 	|    421 	|  NaN 	|    3.0 	|            0.164 	|            0.062 	| -0.227 	|  0.099 	|  0.026 	| $1,089,763 	|


