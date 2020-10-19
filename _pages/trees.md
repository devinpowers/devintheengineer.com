---
layout: archive
permalink: /algorithms/trees
title: "Trees"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

# General Trees

![inserting an Image](/images/tree/general_tree.jpg)

Trees are a non-linear Data Structure, compared to arrays, linked lists, stacks and queues which are linear data strcutures

Tree Node Class:

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

    



[General Properties of Trees](https://devintheengineer.com/algorithms/trees/general_tree)




- Link to Implement Tree

 - Depth and Height Properties
 

# Binary Trees

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