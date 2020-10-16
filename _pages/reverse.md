---
layout: archive
permalink: /algorithms/linked_lists/reverse
title: "Linked Lists- Reverse the List"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---
![inserting an Image](/images/Linked_Lists/reverse/Page1.jpg)
![inserting an Image](/images/Linked_Lists/reverse/Page2.jpg)


Code:


        def reverse_iterative(self):


            previous = None 
            current_node = self.head

            while current_node:

                next_node = current_node.next
                current_node.next = previous


                self.print_helper(previous, "Previous")
                self.print_helper(current_node, "Current Node")
                self.print_helper(next_node, "Next Node")
                print("\n")

                previous = current_node

                current_node = next_node

            self.head = previous



