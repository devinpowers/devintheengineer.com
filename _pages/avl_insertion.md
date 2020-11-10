---
layout: archive
permalink: /algorithms/trees/avl_insertion
title: "AVL Insertion"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

![inserting an Image](/images/tree/avl_insertion/Page1.jpg)
![inserting an Image](/images/tree/avl_insertion/Page2.jpg)
![inserting an Image](/images/tree/avl_insertion/Page3.jpg)



Code:

    import sys

    class Node(object):

        def __init__(self, data = None):

            self.data = data
            self.left = None
            self.right = None
            self.height = 1

    class AVL():

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


            current_node.height = 1 + max(self.GetHeight(current_node.left),self.GetHeight(current_node.right))


            # Update the balance factor and balance the tree


            balanceFactor = self.GetBalance(current_node)

            if balanceFactor > 1:

                if data < current_node.left.data:

                    return self.rightRotate(current_node)

                else:
                    current_node.left = self.leftRotate(current_node.left)

                    return self.rightRotate(current_node)

            if balanceFactor < -1:

                if data > current_node.right.data:

                    return self.leftRotate(current_node)

                else:
                    current_node.right = self.rightRotate(current_node.right)

                    return self.leftRotate(current_node)

            return current_node




        # Function to perform left rotation
        def leftRotate(self, z):
            y = z.right
            T2 = y.left
            y.left = z
            z.right = T2
            z.height = 1 + max(self.GetHeight(z.left),self.GetHeight(z.right))
            y.height = 1 + max(self.GetHeight(y.left),self.GetHeight(y.right))
            return y

        # Function to perform right rotation
        def rightRotate(self, z):
            y = z.left
            T3 = y.right
            y.right = z
            z.left = T3
            z.height = 1 + max(self.GetHeight(z.left),self.GetHeight(z.right))
            y.height = 1 + max(self.GetHeight(y.left),self.GetHeight(y.right))

            return y


        # Get Balance of the Node were on


        def GetBalance(self, current_node):

            if not current_node:

                return 0

            return self.GetHeight(current_node.left) - self.GetHeight(current_node.right)



        # Get the Height of the Node


        def GetHeight(self, current_node):

            if not current_node:

                return 0

            return current_node.height



        def print_tree(self):
            '''Inorder Traversal'''

            if self.root != None:

                self._print_tree(self.root)


        def _print_tree(self, current_node):

            if current_node != None:

                self._print_tree(current_node.left)
                print(str(current_node.data))
                self._print_tree(current_node.right)

        def printHelper(self, currPtr, indent, last):
            if currPtr != None:
                sys.stdout.write(indent)
                if last:
                    sys.stdout.write("R----")
                    indent += "     "
                else:
                    sys.stdout.write("L----")
                    indent += "|    "
                print(currPtr.data)
                self.printHelper(currPtr.left, indent, False)
                self.printHelper(currPtr.right, indent, True)



    mytree = AVL()

    mytree.insert(33)
    mytree.insert(13)
    mytree.insert(52)
    print("")
    mytree.insert(9)
    mytree.insert(21)

    mytree.insert(61)

    mytree.insert(8)
    mytree.insert(11)

    mytree.print_tree()
    print("")

    mytree.printHelper(mytree.root , "", True)


