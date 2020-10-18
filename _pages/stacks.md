---
layout: archive
permalink: /algorithms/stacks
title: "Stacks"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---


Analyzing the Array- Based Stack Implementation

| Operation  | Running Time |
|------------|--------------|
| push(e)    | O (1)        |
| pop()      | O (1)        |
| peak()     | O (1)        |
| is_empty() | O (1)        |
| len()      | O (1)        |




## Implementing  a Stack using an Array:

Pros: Easy
Cons: Not dynamic 


Code:

    class Stack():
        def __init__(self):
            self.items = []

        def push(self, item):
            self.items.append(item)				

        def pop(self):
            return self.items.pop()

        def is_empty(self):
            return self.items == []

        def peek(self):
            if not self.is_empty():
                return self.items[-1]

        def get_stack(self):
            return self.items





## Implementing  a Stack using an Linked List:

Pros:
Cons: