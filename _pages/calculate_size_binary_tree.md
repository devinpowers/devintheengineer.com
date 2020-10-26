---
layout: archive
permalink: /algorithms/trees/calculate_size_binary_tree
title: "Calculate Size of a Binary Tree"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

![inserting an Image](/images/tree/size/Page1.jpg)
![inserting an Image](/images/tree/size/Page2.jpg)
![inserting an Image](/images/tree/size/Page3.jpg)
![inserting an Image](/images/tree/size/Page4.jpg)

Code:

    class Stack(object):
        def __init__(self):
            self.items = []

        def __len__(self):
            return self.size()

        def size(self):
            return len(self.items)

        def push(self, item):
            self.items.append(item)

        def pop(self):  
            if not self.is_empty():
                return self.items.pop()

        def peek(self):
            if not self.is_empty():
                return self.items[-1]

        def is_empty(self):
            return len(self.items) == 0


    class Node(object):

        def __init__(self, value):
            self.value = value
            self.left = None
            self.right = None

    class BinaryTree(object):

        def __init__(self, root):

            self.root = Node(root)

        def size(self):

            if self.root is None:

                return 0

            stack = Stack()

            stack.push(self.root)

            size = 1

            while stack:

                node = stack.pop()

                if node.left:

                    size += 1

                    stack.push(node.left)

                if node.right:

                    size += 1

                    stack.push(node.right)

            return size


        def size_recursive(self, node):
            if node is None:
                return 0
            return 1 + self.size_recursive(node.left) + self.size_recursive(node.right)



    tree = BinaryTree(1)
    tree.root.left = Node(2)
    tree.root.right = Node(3)
    tree.root.left.left = Node(4)
    tree.root.left.right = Node(5)



    print(tree.size_recursive(tree.root))


    print(tree.size())

