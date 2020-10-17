---
layout: archive
permalink: /algorithms/linked_lists/double_append
title: "Doubly Linked Lists- Append and Prepend"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

![inserting an Image](/images/Linked_Lists/double/append/Page1.jpg)
![inserting an Image](/images/Linked_Lists/double/append/Page2.jpg)
![inserting an Image](/images/Linked_Lists/double/append/Page3.jpg)
![inserting an Image](/images/Linked_Lists/double/append/Page4.jpg)

Code:

    class Node:
        def __init__(self, data):
            self.data = data 
            self.next = None
            self.prev = None


    class DoublyLinkedList:
        def __init__(self):
            self.head = None

        def append(self, data):
            if self.head is None:
                new_node = Node(data)
                new_node.prev = None
                self.head = new_node 

            else:
                new_node = Node(data)
                cur = self.head 
                while cur.next:
                    cur = cur.next 
                cur.next = new_node 
                new_node.prev = cur 
                new_node.next = None

        def prepend(self, data):
            if self.head is None:
                new_node = Node(data)
                new_node.next = self.head
                self.head = new_node

            else:
                new_node = Node(data)
                self.head.prev = new_node
                new_node.next = self.head
                self.head = new_node
        def print_list(self):
            cur = self.head 
            while cur:
                print(cur.data)
                cur = cur.next