---
layout: archive
permalink: /algorithms/linked_lists/tail_head
title: "Linked Lists- length of List"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---


![inserting an Image](/images/Linked_Lists/tail/Page1.jpg)

Code:

    def move_tail_to_head(self):
            
        last = self.head
        second_to_last = None
        
        while last.next:
            second_to_last = last
            last = last.next
        
        last.next = self.head
        second_to_last.next = None
        self.head = last
        