---
layout: archive
permalink: /algorithms/trees/bst_deletion
title: "Binary Search Tree Deletion"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

![inserting an Image](/images/tree/bst_delete/Page1.jpg)
![inserting an Image](/images/tree/bst_delete/Page2.jpg)
![inserting an Image](/images/tree/bst_delete/Page3.jpg)
![inserting an Image](/images/tree/bst_delete/Page4.jpg)
![inserting an Image](/images/tree/bst_delete/Page5.jpg)

# including deleting a node

    class Node(object):

        def __init__(self, data = None):

            self.data = data
            self.left = None
            self.right = None
            self.parent = None



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

                    current_node.left.parent=current_node

                else:
                    self._insert(data, current_node.left)

            elif data > current_node.data:

                if current_node.right is None:

                    current_node.right = Node(data)

                    current_node.right.parent=current_node



                else:
                    self._insert(data, current_node.right)

            else:
                print("Value is Already present in Tree.")

        def print_tree(self):

            if self.root != None:

                self._print_tree(self.root)


        def _print_tree(self, current_node):

            if current_node != None:

                self._print_tree(current_node.left)
                print(str(current_node.data))
                self._print_tree(current_node.right)



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


        def find(self, value):

            if self.root != None:

                return self._find(value,self.root )   # recurseive Call to _find Function

            else:
                return None

        def _find(self, value, current_node):

            if value == current_node.data:

                return current_node

            elif value < current_node.data and current_node.left != None:
                return self._find(value, current_node.left)

            elif value > current_node.data and current_node.right != None:
                return self._find(value, current_node.right)

        def delete_value(self,value):

            return self.delete_node(self.find(value))


        def delete_node(self, node):

            # IN case Node doesnt exisit in the tree or no elemnts in the tree
            if node == None or self.find(node.data) == None:

                print("Node to be deleted doesnt exist and isnt in the tree")
                return None

            # returns the node with min value in tree rooted at input node
            def min_value_node(n):

                current = n

                while current.left != None:

                    current = current.left
                return current

            # returns the number of children for the specified node
            def number_childern(n):

                number_childern = 0

                if n.left != None:

                    number_childern += 1

                if n.right != None:

                    number_childern += 1

                return number_childern


            # get the parent of the node to be deleted

            node_parent = node.parent


            # get the number of children of the node to be deleted

            node_childern = number_childern(node)

            # break operation into different cases based on the
            # structure of the tree & node to be deleted

            # CASE 1 (node has no children)

            if node_childern == 0:

                # Added this if statement post-video, previously if you 
                # deleted the root node it would delete entire tree.

                if node_parent != None:
                    # remove reference to the node from the parent

                    if node_parent.left == node:
                        node_parent.left = None

                    else:
                        node_parent.right = None

                else:
                    self.root = None


            # CASE 2 (node has a single child)

            if node_childern == 1:

                # get the single child node

                if node.left != None:

                    child = node.left

                else:
                    child = node.right

                # deleted the root node it would delete entire tree.

                if node_parent != None:
                    # replce the node to be deleted with its child

                    if node_parent.left_child == node:

                        node_parent.left = child

                    else:
                        node_parent.right = child

                else:
                    self.root = child


                #correct the parent parent in node
                child.parent = node_parent

            # CASE 3 (node has two children)
            if node_childern == 2:

                # get inorder sucessof of the deleted node

                sucessor = min_value_node(node.right)

                #copy the inorder successor's value to the node formerly holding the value we wished to delete

                node.data = sucessor.data

                #delete the inorder sucessor now that it's value was copied into th other node

                self.delete_node(sucessor)




    bst = BST()

    bst.insert(8)
    bst.insert(3)
    bst.insert(10)
    bst.insert(2)
    bst.insert(6)
    bst.insert(9)
    bst.insert(11)
    bst.insert(1)



    bst.delete_value(8)

    bst.print_tree()



