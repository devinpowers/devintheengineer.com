---
layout: archive
permalink: /algorithms/linked_list/Node_Swap
title: "Node Swap"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

![inserting an Image](/images/node1.jpg)
![inserting an Image](/images/node2.jpg)
![inserting an Image](/images/node3.jpg)
![inserting an Image](/images/node4.jpg)

# Code


        def swap_nodes(self, key_1, key_2):

                if key_1 == key_2:
                    return 

                prev_1 = None 
                curr_1 = self.head 
                while curr_1 and curr_1.data != key_1:
                    prev_1 = curr_1 
                    curr_1 = curr_1.next

                prev_2 = None 
                curr_2 = self.head 
                while curr_2 and curr_2.data != key_2:
                    prev_2 = curr_2 
                    curr_2 = curr_2.next

                if not curr_1 or not curr_2:
                    return 

                if prev_1:
                    prev_1.next = curr_2
                else:
                    self.head = curr_2

                if prev_2:
                    prev_2.next = curr_1
                else:
                    self.head = curr_1
                    
                print('Before Swap')
                print('current 1 next:', curr_1.data)
                print('current 2 next:', curr_2.data)
                
                curr_1.next, curr_2.next = curr_2.next, curr_1.next
                
                print('\nAfter Swap')
                print('current 1 next:', curr_1.data)
                print('current 2 next:', curr_2.data)
                
            ''' Alternate swap node function , swap by changing the data attribute of node '''
            def swap_nodes_alt(self, key_1, key_2):
                if key_1 == key_2:
                    return
                curr  = self.head
                x , y = None , None # Assign None to avoid reference error
                while curr :
                    if curr.data == key_1:
                        x = curr # key_1 found
                    if curr.data == key_2:
                        y =curr # key_2 found
                    curr = curr.next
                
                if x and y: # Check if both key's exist
                    x.data , y.data = y.data , x.data
                else : 
                    return