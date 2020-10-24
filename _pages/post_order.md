---
layout: archive
permalink: /algorithms/trees/post_order
title: "Post-Order Tree Traversal"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

![inserting an Image](/images/tree/postorder/Page1.jpg)
![inserting an Image](/images/tree/postorder/Page2.jpg)


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

            if traversal_type == "postorder":   
                return self.postorder_print(tree.root, "")

            else: 
                print("Traversal type " + str(traversal_type) + " is not supported.")
                return False


        def postorder_print(self, start, traversal):

            """Left->Right->Root"""

            if start:

                print("Start Node:", start.value)

                traversal = self.postorder_print(start.left, traversal)


                traversal = self.postorder_print(start.right, traversal)


                traversal += (str(start.value) + "-")

                print('Traversal:', traversal)


            return traversal


    tree = BinaryTree(1)
    tree.root.left = Node(2)
    tree.root.right = Node(3)
    tree.root.left.left = Node(4)
    tree.root.left.right = Node(5)
    tree.root.right.left = Node(6)
    tree.root.right.right = Node(7)


    print(tree.print_tree("postorder"))

