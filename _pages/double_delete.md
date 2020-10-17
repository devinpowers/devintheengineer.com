---
layout: archive
permalink: /algorithms/linked_lists/double_delete
title: "Doubly Linked Lists- Delete Node"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

![inserting an Image](/images/Linked_Lists/double/delete/Page1.jpg)
![inserting an Image](/images/Linked_Lists/double/delete/Page2.jpg)
![inserting an Image](/images/Linked_Lists/double/delete/Page3.jpg)
![inserting an Image](/images/Linked_Lists/double/delete/Page4.jpg)
![inserting an Image](/images/Linked_Lists/double/delete/Page5.jpg)

Code:

    def delete(self, key):

            current = self.head

            while current:
                if current.data == key and current == self.head:
                    # Case 1:
                    if not current.next:
                        current = None 
                        self.head = None
                        return

                    # Case 2:
                    else:
                        nxt = current.next
                        current.next = None 
                        nxt.prev = None
                        current = None
                        self.head = nxt
                        return 

                elif current.data == key:
                    # Case 3:
                    if current.next:
                        nxt = current.next 
                        prev = current.prev
                        prev.next = nxt
                        nxt.prev = prev
                        current.next = None 
                        current.prev = None
                        current = None
                        return

                    # Case 4:
                    else:
                        prev = current.prev 
                        prev.next = None 
                        current.prev = None 
                        current = None 
                        return 
                current = current.next


