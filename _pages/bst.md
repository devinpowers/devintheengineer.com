---
layout: archive
permalink: /algorithms/trees/bst
title: "Binary Search Tree"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

Time Complexity of Binary Search Tree

| Algorithm | Average  | Worst Case |
|-----------|----------|------------|
| Space     | O(n)     | O(n)       |
| Search    | O(log n) | O(n)       |
| Insert    | O(log n) | O(n)       |
| Delete    | O(log n) | O(n)       |



![inserting an Image](/images/tree/bst/Page1.jpg)
![inserting an Image](/images/tree/bst/Page2.jpg)
![inserting an Image](/images/tree/bst/Page3.jpg)
![inserting an Image](/images/tree/bst/Page4.jpg)
![inserting an Image](/images/tree/bst/Page5.jpg)
![inserting an Image](/images/tree/bst/Page6.jpg)
![inserting an Image](/images/tree/bst/Page7.jpg)
![inserting an Image](/images/tree/bst/Page8.jpg)
![inserting an Image](/images/tree/bst/Page9.jpg)



Code:

# Binary Search Tree

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

        def find(self, data):

            if self.root:

                is_found = self._find(data, self.root)

                if is_found:

                    return True

                return False

            else:

                return None


        def _find(self, data, current_node):

            if data > current_node.data and current_node.right:

                return self._find(data, current_node.right)

            elif data < current_node.data and current_node.left:

                return self._find(data, current_node.left)

            if data == current_node.data:
                return True

    bst = BST()

    bst.insert(4)
    bst.insert(2)
    bst.insert(8)
    bst.insert(5)
    bst.insert(10)



    print(bst.find(10))


