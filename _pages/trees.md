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

![inserting an Image](/images/tree/binary_tree.jpg)


A Binary Tree is a Tree data structure in which each node has at most two childern.

When we implement a binary tree each node has three attributes:

- data
- left child
- right child.



        class Node(object):
        
            def __init__(self, value):
                self.value = value
                self.left = None
                self.right = None


        class BinaryTree(object):
        
            def __init__(self, root):
                self.root = Node(root)



        tree = BinaryTree(1)
        tree.root.left = Node(2)
        tree.root.right = Node(3)
        tree.root.left.left = Node(4)
        tree.root.left.right = Node(5)
        tree.root.right.left = Node(6)
        tree.root.right.right = Node(7)

        #          DISPLAYED TREE:

        #               1
        #           /       \  
        #          2          3  
        #         /  \      /   \
        #        4    5     6   7 


## Binary Tree Traversals

Tree Traversal is the Process of visiting (checking and/or updating) each node in a tree data structure, exactly once. Unliked other data structures, trees can be traversed in multiple ways.

Depth-First or Breadth-First Order

### Depth-First Order:

1. [In-Order Traversal](https://devintheengineer.com/algorithms/trees/in_order)
2. [Pre-Order Traversal](https://devintheengineer.com/algorithms/trees/pre_order)
3. [Post-Order Traversal](https://devintheengineer.com/algorithms/trees/post_order)

### Breadth-First Order (or Level Order Traversal)

- Level Order Traversal
- Reverse Level Order Traversal


### Other things We can dO with Binary Trees:

- Binary Tree Insertion

- Binary Tree Reversal Level-order Traversal

- Binary Tree Level- Order Traversal

[Calculating Height of a Binary Tree](https://devintheengineer.com/algorithms/trees/height_of_tree)

- Calcualting Size of Binary Tree

- Calculating Height of a Binary Tree

- Calculating the Size of a Binary Tree

# Coming Soon:

## Binary Search Tree

## AVL Tree

## Red-black tree

## Splay Tree

## Treap

## B-Tree


