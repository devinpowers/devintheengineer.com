---
layout: archive
permalink: /algorithms/heaps/min_heap
title: "Min Heap"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---


Insertion Into Min Heap

![inserting an Image](/images/heaps/min_heap/Page1.jpg)
![inserting an Image](/images/heaps/min_heap/Page2.jpg)
![inserting an Image](/images/heaps/min_heap/Page3.jpg)
![inserting an Image](/images/heaps/min_heap/Page4.jpg)
![inserting an Image](/images/heaps/min_heap/Page5.jpg)


Code:

    class MinHeap:
        
        
        def __init__(self):
              
            self.heap_list = [0]      
            self.current_size = 0
            
        def print_(self):
                  
            return self.heap_list
      
        def sift_up(self, i):
                  
            while i // 2 > 0:
                
                if self.heap_list[i] < self.heap_list[i // 2]:
                    
                    self.heap_list[i], self.heap_list[i // 2] = self.heap_list[i // 2], self.heap_list[i]

                i = i // 2
    
        def insert(self, k):
        
            self.heap_list.append(k)
            self.current_size += 1
            
            # Move Element up the Heap
            self.sift_up(self.current_size)
    
    
    my_heap = MinHeap()
    my_heap.insert(10)
    my_heap.insert(30)
    my_heap.insert(20)
    my_heap.insert(35)

    my_heap.insert(40)
    my_heap.insert(32)

    print("Before inserting 8")
    print(my_heap.print_())


    print("After inserting 8")

    my_heap.insert(8)
    print(my_heap.print_())





Deletion of Minimum Value in Min Heap:

Code:


    class MinHeap:
        
        def __init__(self):
      
            self.heap_list = [0]
            self.current_size = 0
    
        def print_(self):

            return self.heap_list
        
        def sift_up(self, i):
          
            while i // 2 > 0:
                if self.heap_list[i] < self.heap_list[i // 2]:
                    self.heap_list[i], self.heap_list[i // 2] = self.heap_list[i // 2], self.heap_list[i]
                i = i // 2
    
        def insert(self, k):
        
            self.heap_list.append(k)
            self.current_size += 1
            self.sift_up(self.current_size)
    
    
        def sift_down(self, i):
            while (i * 2) <= self.current_size:

                mc = self.min_child(i)
                if self.heap_list[i] > self.heap_list[mc]:
                    
                    self.heap_list[i], self.heap_list[mc] = self.heap_list[mc], self.heap_list[i]
                i = mc
    
        def min_child(self, i):
            if (i * 2)+1 > self.current_size:
                return i * 2
            else:
          
                if self.heap_list[i*2] < self.heap_list[(i*2)+1]:
                    return i * 2
                else:
                    return (i * 2) + 1
    
        def delete_min(self):
            
            if len(self.heap_list) == 1:
                return 'Empty heap'
    
            root = self.heap_list[1]
    
            self.heap_list[1] = self.heap_list[self.current_size]
    
            *self.heap_list, _ = self.heap_list
    
            self.current_size -= 1
    
            self.sift_down(1)
            return root
        
    my_heap = MinHeap()
    my_heap.insert(10)
    my_heap.insert(30)
    my_heap.insert(20)
    my_heap.insert(35)
    my_heap.insert(40)
    my_heap.insert(32)
    my_heap.insert(8)

    print("Heap Before Deletion of Min Value")
    print(my_heap.print_())

    my_heap.delete_min()

    print("\n Heap after Deletion of Min Value")
    print(my_heap.print_())
