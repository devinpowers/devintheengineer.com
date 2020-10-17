---
layout: archive
permalink: /algorithms/linked_lists/linked_split
title: "Circular Linked Lists Split List"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

![inserting an Image](/images/Linked_Lists/circular_split/Page1.jpg)
![inserting an Image](/images/Linked_Lists/circular_split/Page2.jpg)
![inserting an Image](/images/Linked_Lists/circular_split/Page3.jpg)

Code:

    def split_list(self):
        
        size = len(self)    

        if size == 0:
            return None
        if size == 1:
            return self.head

        mid_point = size//2
        
        count = 0

        previous = None
        current = self.head

        while current and count < mid_point:
            
            count += 1
            previous = current
            current = current.next
            
        print("Count", count)
        print("Current Node:", current.data)
        print("Previous Node:", previous.data)
        previous.next = self.head 

    # Create second list 
        split_cllist = CircularLinkedList()
        
        while current.next != self.head:
            
            split_cllist.append(current.data)
            
            current = current.next
            
        split_cllist.append(current.data)

        self.print_list()
        
        print("\n")
        
        split_cllist.print_list()