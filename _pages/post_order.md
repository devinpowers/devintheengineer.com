---
layout: archive
permalink: /algorithms/trees/post_order
title: "Post-Order Tree Traversal"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

![inserting an Image](/images/tree/in_order/Page1.jpg)
![inserting an Image](/images/tree/in_order/Page2.jpg)

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

            if traversal_type == "inorder":
                return self.inorder_print(tree.root, "")

            else:
                print("Traversal type " + str(traversal_type) + " is not supported.")
                return False


        def inorder_print(self, start, traversal):

            """Left->Root->Right"""

            if start:

                traversal = self.inorder_print(start.left, traversal)

                traversal += (str(start.value) + "-")

                traversal = self.inorder_print(start.right, traversal)

            return traversal



    tree = BinaryTree(1)
    tree.root.left = Node(2)
    tree.root.right = Node(3)
    tree.root.left.left = Node(4)
    tree.root.left.right = Node(5)
    tree.root.right.left = Node(6)
    tree.root.right.right = Node(7)

    print(tree.print_tree('inorder'))

 