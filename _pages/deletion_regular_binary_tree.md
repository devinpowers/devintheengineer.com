---
layout: archive
permalink: /algorithms/trees/deletion_regular_binary_tree
title: "How to Delete a Node in a Regular Binary Tree"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---

![inserting an Image](/images/tree/delete_binary/Page1.jpg)
![inserting an Image](/images/tree/delete_binary/Page2.jpg)
![inserting an Image](/images/tree/delete_binary/Page3.jpg)
![inserting an Image](/images/tree/delete_binary/Page4.jpg)
![inserting an Image](/images/tree/delete_binary/Page5.jpg)




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

            if not current_node:    

                return

            self.inorder(current_node.left) 

            print(current_node.value,end = " ")

            self.inorder(current_node.right) 

        def delete_deepest(self, root, d_node):

            queue = Queue()

            queue.enqueue(root)

            while len(queue):

                temp = queue.dequeue()

                if temp is d_node:

                    temp = None
                    return

                if temp.right:

                    if temp.right is d_node:   # comparison here

                        temp.right = None

                        return

                    else:

                        queue.enqueue(temp.right)

                if temp.left:

                    if temp.left is d_node:

                        temp.left = None

                        return

                    else:
                        queue.enqueue(temp.left)



        def deletion(self, root, key):   # pass in the root and Key, which is the Node to be deleted
            '''Delete Node in the Tree'''


            if root == None :  # no elements exist in the tree

                return None

            if root.left == None and root.right == None:    # if there exist only the Root!

                if root.key == key:  

                    return None

                else: 

                    return root 


            key_node = None   

            queue = Queue() 

            queue.enqueue(root) # add root to the Queue

            while(len(queue)): 

                temp = queue.dequeue()  # pop Node from the Q


                if temp.value == key:  # if our Temp value is equal to the value to  be deleted, we set the key_node to the temp

                    key_node = temp  

                if temp.left:  # if child of the Left node exists, add it to the Queue

                    queue.enqueue(temp.left) 

                if temp.right: # if Child of Right node  exists, add it to the Queue

                    queue.enqueue(temp.right) 


            if key_node:  


                x = temp.value     

                self.delete_deepest(root,temp)      # call delete Deepest function, pass in our root and the temp value

                key_node.value = x 


            return root 






    tree = BinaryTree(13)

    tree.root.left = Node(12)
    tree.root.left.left = Node(4)
    tree.root.left.right = Node(19)


    tree.root.right = Node(10)
    tree.root.right.left = Node(16)
    tree.root.right.right = Node(9)

    print("Inorder traversal before insertion:", end = " ")

    tree.inorder(tree.root) 


    key = 12
    tree.deletion(tree.root, key) 

    print() 
    print("Inorder traversal after insertion:", end = " ")
    tree.inorder(tree.root) 

