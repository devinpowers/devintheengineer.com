---
layout: archive
permalink: /algorithms/Queues
title: "Queues"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---


FIFO Concept, first in is the first out

Time Complexity of a Queue

| Operation | Running Time (Average) | Running Time (Worst) |
|-----------|------------------------|----------------------|
| Access    | O (n)                  | O (n)                |
| Search    | O (n)                  | O (n)                |
| Insertion | O (1)                  | O (1)                |
| Deletion  | O (1)                  | O (1)                |


Regular Array Implmentation:

Circular Array Implmentation:

![inserting an Image](/images/queues/Page1.jpg)
![inserting an Image](/images/queues/Page2.jpg)
![inserting an Image](/images/queues/Page3.jpg)
![inserting an Image](/images/queues/Page4.jpg)
![inserting an Image](/images/queues/Page5.jpg)
![inserting an Image](/images/queues/Page6.jpg)
![inserting an Image](/images/queues/Page7.jpg)
![inserting an Image](/images/queues/Page8.jpg)
![inserting an Image](/images/queues/Page9.jpg)
![inserting an Image](/images/queues/Page10.jpg)
![inserting an Image](/images/queues/Page11.jpg)
![inserting an Image](/images/queues/Page12.jpg)



# Deque Data Structure:

Let's add a Deque Data Structure

```python

class Deque:
    def __init__(self):
        self.items = []

    def isEmpty(self):
        return self.items == []

    def addFront(self, item):
        self.items.append(item)

    def addRear(self, item):
        """ add to rear"""
        self.items.insert(0,item)

    def removeFront(self):
        return self.items.pop()

    def removeRear(self):
        return self.items.pop(0)

    def size(self):
        return len(self.items)
    
    def _print(self):
        '''print Deque Values'''
        return self.items
        
```