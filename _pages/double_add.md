---
layout: archive
permalink: /algorithms/linked_lists/double_add
title: "Doubly Linked Lists- Add Node Before and After"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

![inserting an Image](/images/Linked_Lists/double/add/Page1.jpg)
![inserting an Image](/images/Linked_Lists/double/add/Page2.jpg)
![inserting an Image](/images/Linked_Lists/double/add/Page3.jpg)
![inserting an Image](/images/Linked_Lists/double/add/Page4.jpg)

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

        def add_after_node(self, key, data):

            current = self.head

            while current:

                if current.next is None and current.data == key:  # Case One

                    self.append(data)
                    return

                elif current.data == key:

                    new_node = Node(data)

                    nxt = current.next 

                    current.next = new_node

                    new_node.next = nxt

                    nxt.previous = new_node

                    new_node.prev = current

                current = current.next



        def add_before_node(self, key, data):

            current = self.head 

            while current:
                if current.prev is None and current.data == key:

                    self.prepend(data)

                elif current.data == key:

                    new_node = Node(data)

                    prev = current.prev

                    prev.next = new_node

                    current.prev = new_node

                    new_node.next = current

                    new_node.prev = prev

                current = current.next


        def print_list(self):
            cur = self.head 
            while cur:
            print(cur.data)
            cur = cur.next