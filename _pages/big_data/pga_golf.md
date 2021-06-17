---
permalink: /Big_Data/big_data/pga_golf
title: "ETL Pipeline"
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

