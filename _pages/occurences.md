---
layout: archive
permalink: /algorithms/linked_lists/occurences
title: "Linked Lists- Occurences of a Node"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

![inserting an Image](/images/Linked_Lists/occurences/Page1.jpg)

Code:

        def count_occurences_iterative(self, data):

                count = 0
                current = self.head
                while current:
                    if current.data == data:
                        count += 1
                    current = current.next

                return count 

            def count_occurences_recursive(self, node, data):

                if not node:
                    return 0 
                if node.data == data:
                    return 1 + self.count_occurences_recursive(node.next, data)
                else:
                    return self.count_occurences_recursive(node.next, data)