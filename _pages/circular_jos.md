---
layout: archive
permalink: /algorithms/linked_lists/circular_jos
title: "Circular Linked Lists Josephus Problem"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

![inserting an Image](/images/Linked_Lists/jos/Page1.jpg)
![inserting an Image](/images/Linked_Lists/jos/Page2.jpg)


Code:

    def remove_node(self, node):
        
        if self.head == node:
            current = self.head
            
            while current.next != self.head:
                current = current.next 
            current.next = self.head.next
            
            self.head = self.head.next
            
        else:  
            current = self.head
            previous = None
            
            while current.next != self.head:     
                previous = current
                current = current.next
                
                if current == node:       
                    previous.next = current.next       
                    current = current.next
            
                
        
    def josephus_circle(self, step):
        
        current = self.head
        
        while len(self) > 1:
            
            count = 1
            
            while count != step:
                
                current = current.next
                count += 1
                
            print("Removed: ", str(current.data))
            self.remove_node(current)
            
            current = current.next