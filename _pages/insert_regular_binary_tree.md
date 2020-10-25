---
layout: archive
permalink: /algorithms/trees/insert_regular_binary_tree
title: "How to Insert a Node into a Regular Binary Tree"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

![inserting an Image](/images/tree/insertion_binary/Page1.jpg)
![inserting an Image](/images/tree/insertion_binary/Page2.jpg)
![inserting an Image](/images/tree/insertion_binary/Page3.jpg)
![inserting an Image](/images/tree/insertion_binary/Page4.jpg)
![inserting an Image](/images/tree/insertion_binary/Page5.jpg)




Code:

    class Queue(object):

        def __init__(self):
            self.items = []

        def enqueue(self, item):
            self.items.insert(0, item)

        def dequeue(self):
            if not self.is_empty():
                return self.items.pop()

        def is_empty(self):
            return len(self.items) == 0

        def peek(self):
            if not self.is_empty():
                return self.items[-1].value

        def __len__(self):
            return self.size()

        def size(self):
            return len(self.items)


    class Node(object):

        def __init__(self, value):

            self.value = value
            self.left = None
            self.right = None


    class BinaryTree(object):

        def __init__(self, root):

            self.root = Node(root)


        def inorder(self,current_node):

            '''Prints our Binary Tree In-Order Traversal'''

            if not current_node:    # tree is empty

                return

            self.inorder(current_node.left) 

            print(current_node.value,end = " ")

            self.inorder(current_node.right) 


        def insert(self,current_node,key):

            if not current_node:   # tree must be empty

                root = Node(key)

                return

            # Create a Queue Data Structure
            queue = Queue()

            # Add Current Node to the Queue
            queue.enqueue(current_node)

            # Do level order traversal until we find an Empty space

            while len(queue) > 0:

                current_node = queue.dequeue()

                if not current_node.left:

                    current_node.left = Node(key) 
                    break
                else:

                    queue.enqueue(current_node.left) 

                if (not current_node.right):
                    current_node.right = Node(key) 
                    break
                else:
                    queue.enqueue(current_node.right) 



    tree = BinaryTree(10)


    tree.root.left = Node(11)
    tree.root.left.left = Node(7)
    tree.root.right = Node(9)
    tree.root.right.left = Node(15)
    tree.root.right.right = Node(8)


    print("Inorder traversal before insertion:", end = " ")

    tree.inorder(tree.root) 



    key = 25
    tree.insert(tree.root, key) 

    print() 
    print("Inorder traversal after insertion:", end = " ")
    tree.inorder(tree.root) 

