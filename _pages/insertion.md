---
layout: archive
permalink: /algorithms/insertion
title: "Insertion Sort"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---


![inserting an Image](/images/sorting/insertion/Page1.jpg)
![inserting an Image](/images/sorting/insertion/Page2.jpg)
![inserting an Image](/images/sorting/insertion/Page3.jpg)
![inserting an Image](/images/sorting/insertion/Page4.jpg)

Code:
```python
from time import time
    ''' insertion sort Algorithm'''


def insertion_sort(list_to_sort):
    
    indexing_length = range(1, len(list_to_sort))
        
    for i in indexing_length:
        
        value_to_sort = list_to_sort[i]
        
        
        while list_to_sort[i-1] > value_to_sort and i>0: # python allows negative indexing
            
            list_to_sort[i], list_to_sort[i-1] = list_to_sort[i-1], list_to_sort[i]
        
            i = i -1  # move down the sorted list to check if number is less than the previous number
        
    return list_to_sort


array = [7,2,1,6,8,5,3,102,1,31,45,232,4,25,12,8,2,4,2,0,9,12,6,2,4,1,3]

start_time = time()

sorted_array = insertion_sort(array)

end_time = time()

print('Time to Complete Soring:', end_time-start_time)
print(sorted_array)
```