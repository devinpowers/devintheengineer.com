---
permalink: /Big_Data/big_data/day_13
title: "A/B Testing"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"

toc: true
toc_label: "Table of Contents" 

---

### What is A/B Testing ?

* A/B testing is a method for comparing 2 verisions of something against each other to discover which is *more* successful.


### What is Multivariate Testing?

* Multivariate Testing is just an expansion of A/B testing in which *more than* two versions are compared and more variation is included, in which you can test multiple items at once and see how they interact together.

### Example of an A/B Test 

Lets first import all the libraries needed
```python

import numpy as np
import pandas as pd
from scipy.stats import ttest_ind
import matplotlib.pyplot as plt
import seaborn as sns

```


Now lets import our **DATA** using Pandas 



```python

test_df = pd.read_csv('test_table.csv')

user_df = pd.read_csv('user_table.csv')

```

Lets check our data using **.info()**

```python
test_df.info()
```

<iframe src="https://cdn.wallethub.com/wallethub/embed/90947/covid-recovering-v2.html" width="556" height="347" frameBorder="0" scrolling="no"></iframe><div style="width:556px;font-size:12px;color:#888;">Source: <a href="https://wallethub.com/edu/states-covid-recovery/90947">WalletHub</a></div>

