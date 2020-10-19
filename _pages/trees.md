---
layout: archive
permalink: /algorithms/trees
title: "Trees"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

# General Trees

![inserting an Image](/images/tree/tree.jpg)

Trees are a non-linear Data Structure, compared to arrays, linked lists, stacks and queues which are linear data strcutures


    class Node(object):

        def __init__(self, data):
            self.data = data
            self.children = []

        def add_child(self, obj):
            self.children.append(obj)

    Root = Node(1)

    Red = Node(2)

    Yellow = Node(3)

    Pink_1 = Node(4)
    Pink_2 = Node(5)
    Pink_3 = Node(6)

    Brown_2 = Node(7)

    Brown_1 = Node(8)

    Green_1 = Node(9)
    Green_2 = Node(10)

    Blue = Node(11)

    Root.add_child(Red)
    Root.add_child(Yellow)

    Red.add_child(Pink_1)
    Red.add_child(Pink_2)
    Red.add_child(Pink_3)

    Yellow.add_child(Brown_1)
    Yellow.add_child(Brown_2)

    Pink_1.add_child(Green_1)
    Pink_1.add_child(Green_2)

    Brown_2.add_child(Blue)

    



[General Properties of Trees](https://devintheengineer.com/algorithms/trees/general_tree)

 - Including the height and depth


 

# Binary Trees

Binary Tree

    class Node:
    
        def __int__(self, data):

            self.left = None
            self.right = None
            self.data = data
            
    
    node2 = Node(2)
    node3 = Node(3)
    node4 = Node(4)
    node5 = Node(5)
    node6 = Node(6)

    node2.left = node3
    node2.right = node4
    node3.left = node5
    node3.right = node6

    
    #  Our example tree looks like this:
    #         2
    #       /   \
    #      3     4
    #     / \
    #    5   6


- [insert Binary Tree Picture]
-- IMplementing Binary Tree

 - Dynamically Created Nodes
 - Arrays
- Binary Tree Level-Order Traversal

- Binary Tree Insertion

- Binary Tree Reversal Level-order Traversal

- Binary Tree Level- Order Traversal

[Calculating Height of a Binary Tree](https://devintheengineer.com/algorithms/trees/height_of_tree)

- Calcualting Size of Binary Tree