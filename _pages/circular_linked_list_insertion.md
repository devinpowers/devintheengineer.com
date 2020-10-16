---
layout: archive
permalink: /algorithms/linked_lists/circular_linked_list_insertion
title: "Circular Linked Lists Insertion"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---
![inserting an Image](/images/Linked_Lists/Circular_append/Page1.jpg)
![inserting an Image](/images/Linked_Lists/Circular_append/Page2.jpg)
![inserting an Image](/images/Linked_Lists/Circular_append/Page3.jpg)

Code:

        class Node:

            def __init__(self, data):
                self.data = data
                self.next = None


        class CircularLinkedList:

            def __init__(self):

                self.head = None

            def append(self, data):

                if not self.head:  

                    self.head = Node(data)
                    self.head.next = self.head    

                else:
                    new_node = Node(data)

                    current = self.head

                    while current.next != self.head:
                        current = current.next

                    current.next = new_node

                    new_node.next = self.head


            def print_list(self):

                current = self.head

                while self.head:

                    print(current.data)

                    current = current.next

                    if current == self.head:  
                        break



            def prepend(self,data):

                new_node = Node(data)

                current = self.head

                new_node.next = self.head

                if not self.head:

                    new_node.next = new_node

                else:

                    while current.next != self.head:
                        current = current.next

                    current.next = new_node

                self.head = new_node













