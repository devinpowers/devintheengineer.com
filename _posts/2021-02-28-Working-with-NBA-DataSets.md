---
title: 'Big Data Analysis with NBA DataSets '

date: 2021-2-28

---

```python
import pandas as p
data = p.read_csv('nba_draft_combine_all_years.csv', header = 0)
```

```python
other = data[:10][["Player", "Weight", "Height (No Shoes)", "Wingspan"]]
```

Output:

```python
	Player	            Weight	Height (No Shoes)	Wingspan
0	Blake Griffin	    248.0	    80.50	        83.25
1	Terrence Williams	213.0	    77.00	        81.00
2	Gerald Henderson	215.0	    76.00	        82.25
3	Tyler Hansbrough	234.0	    80.25	        83.50
4	Earl Clark	        228.0	    80.50	        86.50
5	Austin Daye	        192.0	    81.75	        86.75
6	James Johnson	    257.0	    79.00	        84.75
7	Jrue Holiday	    199.0	    75.25	        79.00
8	Ty Lawson	        197.0	    71.25	        72.75
9	Jeff Teague     	175.0	    72.25	        79.50

```
