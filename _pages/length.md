---
layout: archive
permalink: /algorithms/linked_lists/length
title: "Linked Lists- length of List"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

![inserting an Image](/images/Linked_Lists/length/Page1.jpg)

Code:

        def length_iterative(self):

            count = 0
            current_node = self.head

            while current_node:
                count += 1
                current_node = current_node.next
            return count

        def length_recursive(self, node):
            if node is None:
                return 0
            return 1 + self.length_recursive(node.next)