---
layout: archive
permalink: /algorithms/trees/bst_height
title: "Binary Search Tree Height"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

![inserting an Image](/images/tree/bst_height/Page1.jpg)
![inserting an Image](/images/tree/bst_height/Page2.jpg)


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


        def height(self):

            if self.root!=None:

                return self._height(self.root, 0)

            else:
                return 0

        def _height(self, current_node, current_height):

            if current_node == None:
                return current_height

            left_height= self._height(current_node.left,current_height+1)

            right_height=self._height(current_node.right,current_height+1)

            return max(left_height,right_height)



    bst = BST()

    bst.insert(8)
    bst.insert(3)
    bst.insert(10)
    bst.insert(2)
    bst.insert(6)
    bst.insert(9)
    bst.insert(11)
    bst.insert(1)




    print(bst.height())




