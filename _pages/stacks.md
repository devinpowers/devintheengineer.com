---
layout: archive
permalink: /algorithms/stacks
title: "Stacks"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---



![inserting an Image](/images/stacks/Page1.jpg)
![inserting an Image](/images/stacks/Page2.jpg)
![inserting an Image](/images/stacks/Page3.jpg)
![inserting an Image](/images/stacks/Page4.jpg)



Analyzing the Array - Based Stack Implementation

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
    
    def print_stack(self):
        
        for element in self.items:
            print(element)

    

    stack_practice = Stack()

    stack_practice.push('A')
    stack_practice.push('B')
    stack_practice.push('D')
    stack_practice.push('C')
    stack_practice.push('J')
    print("Stack Before Popping: ")
    stack_practice.print_stack()
    print("\n")
    stack_practice.pop()
    print("Stack After Popping: ")
    stack_practice.print_stack()







## Implementing  a Stack using an Linked List:


Code:

    class Node: 

        def __init__(self, data): 
            self.data = data  
            self.next = None

    class Stack: 

        def __init__(self): 
            self.head = None

        def isEmpty(self): 
            return True if self.head is None else  False 

        def push(self, data): 

            new_node = Node(data)

            new_node = self.head

            self.head = new_node

            print("Push onto stack", data)


        def pop(self): 
            if (self.isEmpty()): 
                return float("-inf") 
            temp = self.head
            self.head = self.head.next 
            popped = temp.data 
            return popped 

        def peek(self): 
            if self.isEmpty(): 
                return float("-inf") 
            return self.head.data 
            
            
