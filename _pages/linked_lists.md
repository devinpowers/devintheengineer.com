---
layout: archive
permalink: /algorithms/linked_lists
title: "Linked Lists"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---


- Here are different operations that are commonly performed on Singular, Doubly, and Circular Linked Lists
- Code and Step-by-Step diagrams/Notes are provided


# Singular Linked Lists:

![inserting an Image](/images/Linked_Lists/home/single_node.jpg)

A new Class "Node" is required to create the data structure:

    class Node:

        def __init__ (self,data):
            self.data = data
            self.next = None

Once we have created a Node Class we can Create a Linked List Class:

    class linkedList():

        def __init__(self):
            self.head = None

From here we can add functionality like insertion and deletion of Nodes, the following links on this page show the step-by-step processes of different functionality of a Singly Linked List.


Time Complexity for Singly-Linked List:

| Operation | Running Time (Average) | Running Time (Worst) |
|-----------|------------------------|----------------------|
| Access    | O (n)                  | O (n)                |
| Search    | O (n)                  | O (n)                |
| Insertion | O (1)                  | O (1)                |
| Deletion  | O (1)                  | O (1)                |

[Linked Lists Insertion](https://devintheengineer.com/algorithms/linked_lists/linked_list_insertion)


[Linked Lists Deletion](https://devintheengineer.com/algorithms/linked_lists/linked_list_deletion)


[Find the Nth-to-Last Node](https://devintheengineer.com/algorithms/linked_lists/linked_list_nth)


[Find the Occerences of a Node](https://devintheengineer.com/algorithms/linked_lists/occurences)

[Length of Singly Linked List](https://devintheengineer.com/algorithms/linked_lists/length)

[Rotate Around Pivot](https://devintheengineer.com/algorithms/linked_lists/rotate)


[Reverse Linked List](https://devintheengineer.com/algorithms/linked_lists/reverse)


[Node Swap Singly Linked Lists](https://devintheengineer.com/algorithms/linked_lists/Node_Swap)


[Remove Duplicates of Singular Linked Lists](https://devintheengineer.com/algorithms/linked_lists/duplicates)

[Move Tail to head](https://devintheengineer.com/algorithms/linked_lists/tail_head)

[Merge Two Sorted Lists](https://devintheengineer.com/algorithms/linked_lists/single_merge)

Coming Soon:
- Check if Linked list is a Palindrome
- Sum two Lists


# Doubly Linked Lists:

![inserting an Image](/images/Linked_Lists/home/double.jpg)

For a Doubly Linked List we need to adjust the Node Class to include Previous

    class Node:

        def __init__(self, data):
            self.data = data 
            self.next = None
            self.prev = None

From here we can add functionality like we did in Single Linked List


Time Complexity for Doubly-Linked List:

| Operation | Running Time (Average) | Running Time (Worst) |
|-----------|------------------------|----------------------|
| Access    | O (n)                  | O (n)                |
| Search    | O (n)                  | O (n)                |
| Insertion | O (1)                  | O (1)                |
| Deletion  | O (1)                  | O (1)                |


[Doubly Linked Lists Add Node Before and After](https://devintheengineer.com/algorithms/linked_lists/double_add)

[Doubly Linked Lists Append and Prepend](https://devintheengineer.com/algorithms/linked_lists/double_append)

[Doubly Linked Lists Delete Node](https://devintheengineer.com/algorithms/linked_lists/double_delete)

Coming Soon:
 - Pairs with Sum
 - Remove Duplicates
 - Reverse list
 

# Circular Linked Lists:

![inserting an Image](/images/Linked_Lists/home/circle.jpg)

For a Circular Linked List we can use the same Node Class that we used in Single Linked List


[Circular Linked Lists Insertion](https://devintheengineer.com/algorithms/linked_lists/circular_linked_list_insertion)

[Circular Linked Lists Remove Node](https://devintheengineer.com/algorithms/linked_lists/circular_remove)

[Circular Linked List Split](https://devintheengineer.com/algorithms/linked_lists/linked_split)

[Circular Linked List Josephus Problem](https://devintheengineer.com/algorithms/linked_lists/circular_jos)


