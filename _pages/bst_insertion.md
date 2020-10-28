---
layout: archive
permalink: /algorithms/trees/bst_insertion
title: "Binary Search Tree Insertion"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---
![inserting an Image](/images/tree/bst_insertion/Page1.jpg)
![inserting an Image](/images/tree/bst_insertion/Page2.jpg)
![inserting an Image](/images/tree/bst_insertion/Page3.jpg)
![inserting an Image](/images/tree/bst_insertion/Page4.jpg)


Code:


    class Node(object):

        def __init__(self, data = None):

            self.data = data
            self.left = None
            self.right = None


    class BST:

        def __init__(self):

            self.root = None

        def insert(self, data):

            if self.root is None:

                self.root = Node(data)

            else:
                self._insert(data,self.root)

        def _insert(self, data, current_node):

            if data < current_node.data:

                if current_node.left is None:

                    current_node.left = Node(data)

                else:
                    self._insert(data, current_node.left)

            elif data > current_node.data:

                if current_node.right is None:

                    current_node.right = Node(data)

                else:
                    self._insert(data, current_node.right)

            else:
                print("Value is Already present in Tree.")
