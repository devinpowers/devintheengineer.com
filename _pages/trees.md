---
layout: archive
permalink: /algorithms/trees
title: "Tree Data Structures"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---






## General Trees

![inserting an Image](/images/tree/tree.jpg)

Trees are a non-linear Data Structure, compared to arrays, linked lists, stacks and queues which are linear data strcutures

```python
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
```




[General Properties of Trees](https://devintheengineer.com/algorithms/trees/general_tree)

 - Including the Height and Depth of a Tree


 

# Binary Trees

![inserting an Image](/images/tree/binary_tree.jpg)


A Binary Tree is a Tree data structure in which each node has at most two childern.

When we implement a binary tree each node has three attributes:

- Data
- Left Child
- Right Child.

```python
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
```


## Binary Tree Traversals

Tree Traversal is the Process of visiting (checking and/or updating) each node in a tree data structure, exactly once. Unliked other data structures, trees can be traversed in multiple ways.

Depth-First or Breadth-First Order

#### Depth-First Order:

1. [In-Order Traversal](https://devintheengineer.com/algorithms/trees/in_order)
2. [Pre-Order Traversal](https://devintheengineer.com/algorithms/trees/pre_order)
3. [Post-Order Traversal](https://devintheengineer.com/algorithms/trees/post_order)

#### Breadth-First Order (or Level Order Traversal)

[Level Order Traversal](https://devintheengineer.com/algorithms/trees/level_order)

[Level Order Reverse Traversal](https://devintheengineer.com/algorithms/trees/level_order_reverse)

### Different Operations on Binary Trees:

Time Complexity of Different Operations in a Binary Tree

| Operation | Running Time (Worst) |
|-----------|----------------------|
| Search    | O(n)                 |
| Delete    | O(n)                 |
| Insertion | O(n)                 |


[Calculating Height of a Binary Tree](https://devintheengineer.com/algorithms/trees/height_of_tree)

[Calculating the Size of a Binary Tree](https://devintheengineer.com/algorithms/trees/calculate_size_binary_tree)

[Insertion into a Regular Binary Tree](https://devintheengineer.com/algorithms/trees/insert_regular_binary_tree)

[Deletion of a Node in a Regular Binary Tree](https://devintheengineer.com/algorithms/trees/deletion_regular_binary_tree)



### Implementing a Binary Tree

Coming Soon:

Binary Tree from an Array

Binary Tree from an Linked list





# Binary Search Tree

![inserting an Image](/images/tree/bst.jpg)

A BST is a SPECIAL FORM of a Binary Tree data structure where each node has a comparable value, and smaller valued childern attached to left and larger valued childern attached to the right

## Pros and Cons of a Binary Search Tree

Pros: 
- Inserting and Deleting
- Speed of Access
- Maintains sorted order; retrieval of elements is in order

Cons:
- Expensive because of their creation and management

[Binary Search Tree Introduction](https://devintheengineer.com/algorithms/trees/bst)

### Operations on Binary Search Tree:

[Insertion into a Binary Search Tree](https://devintheengineer.com/algorithms/trees/bst_insertion)


[Deletion of a Node in a Binary Search Tree](https://devintheengineer.com/algorithms/trees/bst_deletion)


[Searching for a Value in  a Binary Search Tree](https://devintheengineer.com/algorithms/trees/bst_search)

[Height of Binary Search Tree](https://devintheengineer.com/algorithms/trees/bst_height)


Time Complexity of Different Operations of a Binary Search Tree

| Operation | Average  | Worst Case |
|-----------|----------|------------|
| Space     | O(n)     | O(n)       |
| Search    | O(log n) | O(n)       |
| Delete    | O(log n) | O(n)       |
| Insertion | O(log n) | O(n)       |



### Coming Soon:


# Rebalancing a Binary Search Tree by Rotation

![inserting an Image](/images/tree/bst_balance.jpg)

[Rebalance Operations](https://devintheengineer.com/algorithms/trees/rebalance_operations)

- Left Rotation

- Right Rotation

- Left Left Rotation

- Right Right Rotation



## AVL Tree

[AVL Tree Introduction](https://devintheengineer.com/algorithms/trees/avl_intro)

#### Operations on AVL Tree

[AVL Tree Insertion](https://devintheengineer.com/algorithms/trees/avl_insertion)

[AVL Tree Deletion](https://devintheengineer.com/algorithms/trees/avl_deletion)

- AVL Tree Search

Time Complexity of Different Operations of a AVL Tree

| Operation | Average  | Worst Case |
|-----------|----------|------------|
| Space     | O(n)     | O(n)       |
| Search    | O(log n) | O(log n)   |
| Delete    | O(log n) | O(log n)   |
| Insertion | O(log n) | O(log n)   |



# Coming Soon ( End of 2021)


## Red-Black Tree

- Red-Black Tree Introduction

#### Operations on Red-Black Tree

- Red-Black Tree Insertion

- Red-Black Tree Deletion

- Red-Black Tree Search

Time Complexity of Different Operations of a Red-Black Tree

| Operation | Average  | Worst Case |
|-----------|----------|------------|
| Space     | O(n)     | O(n)       |
| Search    | O(log n) | O(log n)   |
| Delete    | O(log n) | O(log n)   |
| Insertion | O(log n) | O(log n)   |


## Splay Tree

- Splay Tree Introduction

### Operations on a Splay Tree

- Splay Tree Insertion

- Splay Tree Deletion

- Splay Tree Search


Time Complexity of Different Operations of a Splay Tree

| Operation | Average  | Worst Case |
|-----------|----------|------------|
| Space     | O(n)     | O(n)       |
| Search    | O(log n) | O(log n)   |
| Delete    | O(log n) | O(log n)   |
| Insertion | O(log n) | O(log n)   |


## Treap

- Treap Tree Introduction

## Operations on a Treap

- Treap Tree Insertion

- Treap Tree Deletion

- Treap Tree Search

Time Complexity of Different Operations of a Treap

| Operation | Average  | Worst Case |
|-----------|----------|------------|
| Space     | O(n)     | O(n)       |
| Search    | O(log n) | O(n)       |
| Delete    | O(log n) | O(n)       |
| Insertion | O(log n) | O(n)       |

## B-Tree

- B-Tree Introduction

## Operations on a B-Tree

- B-Tree Insertion

- B-Tree Deletion

- B-Tree Search

Time Complexity of Different Operations of a B-Tree

| Operation | Average  | Worst Case |
|-----------|----------|------------|
| Space     | O(n)     | O(n)       |
| Search    | O(log n) | O(log n)   |
| Delete    | O(log n) | O(log n)   |
| Insertion | O(log n) | O(log n)   |




