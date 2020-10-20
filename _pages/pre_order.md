---
layout: archive
permalink: /algorithms/trees/pre_order
title: "Pre-Order Tree Traversal"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

![inserting an Image](/images/tree/pre_order/Page1.jpg)
![inserting an Image](/images/tree/pre_order/Page2.jpg)
![inserting an Image](/images/tree/pre_order/Page3.jpg)
![inserting an Image](/images/tree/pre_order/Page4.jpg)


Code:

    class Node(object):
        def __init__(self, value):
            self.value = value
            self.left = None
            self.right = None


    class BinaryTree(object):

        def __init__(self, root):
            self.root = Node(root)

        def print_tree(self, traversal_type):

            if traversal_type == "preorder":

                return self.preorder_print(tree.root, "")

            else:
                print("Traversal Type " + str(traversal_type) + " is not supported in out function")
                return False            

        def preorder_print(self, start, traversal):

            """Root->Left->Right"""
            if start:

                traversal += (str(start.value) + "-")
                print('Traversal:', traversal)

                traversal = self.preorder_print(start.left, traversal)

                traversal = self.preorder_print(start.right, traversal)

            return traversal


    tree = BinaryTree(1)
    tree.root.left = Node(2)
    tree.root.right = Node(3)
    tree.root.left.left = Node(4)
    tree.root.left.right = Node(5)
    tree.root.right.left = Node(6)
    tree.root.right.right = Node(7)

    print(tree.print_tree('preorder'))