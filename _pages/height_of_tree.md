---
layout: archive
permalink: /algorithms/trees/height_of_tree
title: "How to Calculate the Height of a Binary Tree"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---
![inserting an Image](/images/tree/height/Page1.jpg)
![inserting an Image](/images/tree/height/Page2.jpg)
![inserting an Image](/images/tree/height/Page3.jpg)
![inserting an Image](/images/tree/height/Page4.jpg)
![inserting an Image](/images/tree/height/Page5.jpg)
![inserting an Image](/images/tree/height/Page6.jpg)
![inserting an Image](/images/tree/height/Page7.jpg)


Code:

    class Node(object):

        def __init__(self, value):
            self.value = value
            self.left = None
            self.right = None


    class BinaryTree(object):

        def __init__(self, root):

            self.root = Node(root)

        def height(self, node):

            if node is None:

                return -1

            left_height = self.height(node.left)

            right_height = self.height(node.right)

            return 1 + max(left_height, right_height)

    tree = BinaryTree(1)
    tree.root.left = Node(2)
    tree.root.right = Node(3)
    tree.root.left.left = Node(4)
    tree.root.left.right = Node(5)

    print(tree.height(tree.root))

