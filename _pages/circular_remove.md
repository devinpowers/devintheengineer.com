---
layout: archive
permalink: /algorithms/linked_lists/circular_remove
title: "Circular Linked Lists Remove Nodes"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---
![inserting an Image](/images/Linked_Lists/circular_remove/Page1.jpg)
![inserting an Image](/images/Linked_Lists/circular_remove/Page2.jpg)
![inserting an Image](/images/Linked_Lists/circular_remove/Page3.jpg)


Code:

    def remove(self, key):
        
        if self.head.data == key:  
            
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
                
                if current.data  == key:
                    
                    previous.next = current.next
                    
                    current = current.next
            







