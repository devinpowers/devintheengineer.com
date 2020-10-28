---
layout: archive
permalink: /algorithms/trees/bst_deletion
title: "Binary Search Tree Deletion"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---






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


        def print_tree(self, traversal_type):


            if traversal_type == "inorder":
                return self.inorder_print(tree.root, "")

            else:
                print("Traversal type " + str(traversal_type) + " is not supported.")
                return False    

        def inorder_print(self, start, traversal):

            if start:

                traversal = self.inorder_print(start.left, traversal)

                traversal += (str(start.data) + "-")

                traversal = self.inorder_print(start.right, traversal)

            return traversal




        def minValueNode(self,node): 

            '''Find the minimum value'''

            current = node 

            while current.left is not None: 

                current = current.left  

            return current  


        def delete_node(self, current_node, data):

            # Base Case

            if current_node is None:

                return current_node

            # if data to be deleted is smaller the root is lies in the left subtree

            if data < current_node.data:

                current_node.left = self.delete_node(current_node.left, data)

            # elif most lie in the right subtree
            elif data > current_node.data:

                current_node.right = self.delete_node(current_node.right, data)

            # if the value is the same as root data 

            else:
                print('Root Value is:', current_node.data)


                # Node with only one child or no child

                if current_node.left is None:

                    temp = current_node.right

                    current_node = None

                    return temp

                elif current_node.right is None:
                    temp = current_node.left
                    current_node =None
                    return temp



                temp = self.minValueNode(current_node.right) 

                # Copy the inorder successor's content to this node 
                current_node.data = temp.data 

                # Delete the inorder successor 
                current_node.right = self.delete_node(current_node.right , temp.data) 

            return current_node 


    tree = BST()

    tree.insert(50)
    tree.insert(30)
    tree.insert(20)
    tree.insert(40)
    tree.insert(70)
    tree.insert(60)
    tree.insert(80)

    # delete 20
    tree.delete_node(tree.root,20)

    print(tree.print_tree("inorder"))

    #delete 30

    tree.delete_node(tree.root, 30)
    print(tree.print_tree("inorder"))

    #deletee 50
    tree.delete_node(tree.root, 50)

    print(tree.print_tree("inorder"))




