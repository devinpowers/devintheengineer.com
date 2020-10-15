---
layout: archive
permalink: /algorithms/linked_lists/linked_list_nth
title: "Linked Lists- Nth-to-Last Node"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

![inserting an Image](/images/Linked_Lists/nth/Page1.jpg)
![inserting an Image](/images/Linked_Lists/nth/Page2.jpg)

Code:

Method 1:

        def print_nth_from_last(self, n):

                total_length = self.length_iterative()

                current = self.head 
                while current:
                    if total_length == n:
                        print(current.data)

                        return current

                    total_length -= 1
                    current = current.next
                if current is None:
                   return

Method 2:

        def print_nth_from_last(self, n):


                p = self.head
                q = self.head

                count = 0
                while q and count < n:

                    q = q.next
                    count += 1

                if not q:

                    print(str(n) + " is greater than the number of nodes in list.")
                    return

                while p and q:

                    p = p.next
                    q = q.next

                return p.data


