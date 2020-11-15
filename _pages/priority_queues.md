---
layout: archive
permalink: /algorithms/heaps/priority_queues
title: "Priority Queues"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

code:


    # Python code to implement Priority Queue using Linked List

    class Node:
        
        def __init__(self, item, priority):
            
            self.item = item
            self.next = None
            self.priority = priority


    class PriorityQueue:
        
        def __init__(self):
            
            self.front = None
            self.rear = None

        def isEmpty(self):
            
            return self.front == None   #Return True if Empty
        

        # Adds the given item to the queue by inserting it in the proper 
        # position based on the given priority. The new node is appended to 
        # the end of the linked list
        def enqueue(self, item, priority):
            
            newNode = Node(item, priority)
            
            
            if not self.rear:
                
                self.front = newNode
                self.rear= newNode
                
                return
            
            if self.front.priority <= newNode.priority:
                
                newNode.next = self.front
                self.front = newNode
                
                return
            
            previous = None
            current = self.front
            while(current and newNode.priority < current.priority):
                previous = current
                current = current.next

            if current:
                previous.next = newNode
                newNode.next = current
            else:
                self.rear.next = newNode
                self.rear = newNode

        # Removes and returns the next item from the queue, which is the 
        # item with the highest priority. If two or more items have the 
        # same priority, those items are removed in FIFO order. An item 
        # cannot be dequeued from an empty queue. 
        def dequeue(self):
            if self.isEmpty():
                print('Queue is empty')
                return
            temp = self.front
            self.front = self.front.next
            if self.front == None:
                self.rear = None
            return temp.item
        

    q = PriorityQueue()

    q.enqueue('Devin', 1)
    q.enqueue('Kobe', 1)
    q.enqueue('Lebron', 2)
    q.enqueue('Michael', 3)


    print(q.dequeue())
    print(q.dequeue())
    print(q.dequeue())
    print(q.dequeue())


    # Python code to implement Priority Queue using Linked List

    class Node:
        
        def __init__(self, item, priority):
            
            self.item = item
            self.next = None
            self.priority = priority


    class PriorityQueue:
        
        def __init__(self):
            
            self.front = None
            self.rear = None

        def isEmpty(self):
            
            return self.front == None   #Return True if Empty
        

        # Adds the given item to the queue by inserting it in the proper 
        # position based on the given priority. The new node is appended to 
        # the end of the linked list
        def enqueue(self, item, priority):
            
            newNode = Node(item, priority)
            
            
            if not self.rear:
                
                self.front = newNode
                self.rear= newNode
                
                return
            
            if self.front.priority <= newNode.priority:
                
                newNode.next = self.front
                self.front = newNode
                
                return
            
            previous = None
            current = self.front
            while(current and newNode.priority < current.priority):
                previous = current
                current = current.next

            if current:
                previous.next = newNode
                newNode.next = current
            else:
                self.rear.next = newNode
                self.rear = newNode

        # Removes and returns the next item from the queue, which is the 
        # item with the highest priority. If two or more items have the 
        # same priority, those items are removed in FIFO order. An item 
        # cannot be dequeued from an empty queue. 
        def dequeue(self):
            if self.isEmpty():
                print('Queue is empty')
                return
            temp = self.front
            self.front = self.front.next
            if self.front == None:
                self.rear = None
            return temp.item
        

    q = PriorityQueue()

    q.enqueue('Devin', 1)
    q.enqueue('Kobe', 1)
    q.enqueue('Lebron', 2)
    q.enqueue('Michael', 3)


    print(q.dequeue())
    print(q.dequeue())
    print(q.dequeue())
    print(q.dequeue())

