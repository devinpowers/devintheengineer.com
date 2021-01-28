---
layout: archive
permalink: /algorithms/linked_lists/linked_list_insertion
title: "Linked Lists Insertion"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

![inserting an Image](/images/Linked_Lists/insertion/Page1.jpg)
![inserting an Image](/images/Linked_Lists/insertion/Page2.jpg)
![inserting an Image](/images/Linked_Lists/insertion/Page3.jpg)
![inserting an Image](/images/Linked_Lists/insertion/Page4.jpg)

Code for different ways to Insert into a singular Linked List:


    class Node:

            def __init__(self,data):
                self.data = data
                self.next = None

    class linkedList():

        def __init__(self):
            
            self.head = None

        def print_list(self):

            current_node = self.head

            while current_node:

                print(current_node.data)
                current_node = current_node.next


        def append(self, data):

            new_node = Node(data)

            if self.head is None:

                self.head = new_node

                return

            last_node = self.head

            while last_node.next:
                # loop thru linked list until last_node.next is pointing to null
                last_node = last_node.next

            # after it exits the loop, we append new node:

            last_node.next = new_node

        def prepend(self,data):

            new_node = Node(data)

            new_node.next = self.head 

            self.head = new_node

        def insertion_after_node(self, previous_node, data):

            if not previous_node:
                print("Previous node is not in the list")
                return

            new_node = Node(data)

            new_node.next = previous_node.next
            previous_node.next = new_node
        
        
        def __iter__(self):
            
            node = self.head
            while node:
                
                '''iterate thru linked list, while node is TRUE,
                    which means it exists.
                '''
                yield node.data
                node = node.next
        
            
        def __repr__(self):
            """Represented String of the Linked List!"""
            return str([v for v in self])
        
            

        

    llist = linkedList()

    llist.append('A')
    llist.append('B')
    llist.append('C')
    llist.append('D')
    llist.append('E')

    llist.print_list()
    print("")
    llist.prepend('Z')
    llist.print_list()

    print("")


    llist.insertion_after_node(llist.head.next, "T")

    llist.print_list()




    print(repr(llist))


Output

    A
    B
    C
    D
    E

    Z
    A
    B
    C
    D
    E

    Z
    A
    T
    B
    C
    D
    E
    ['Z', 'A', 'T', 'B', 'C', 'D', 'E']