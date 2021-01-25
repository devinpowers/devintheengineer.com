---
layout: archive
permalink: /algorithms/hash
title: "Intro to Hash Tables"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
  
---
## Time Complexity of Hash Tables

| Operation | Running Time (Average) | Running Time (Worst) |
|-----------|------------------------|----------------------|
| Space     | O(n)                   | O(n)                 |
| Search    | O(1)                   | O(n)                 |
| Insert    | O(1)                   | O(n)                 |
| Delete    | O(1)                   | O(n)                 |

![inserting an Image](/images/hashing/intro/Page1.jpg)
![inserting an Image](/images/hashing/intro/Page2.jpg)
![inserting an Image](/images/hashing/intro/Page3.jpg)
![inserting an Image](/images/hashing/intro/Page4.jpg)




## Advantages of Hash Tables

- Speed
- Set of key-value pairs is fixed and known ahead of time, which reduces the average lookup cost


## Drawbacks



# Example of a Hash Table in Python


  initial_capacity = 20


  class Node:
      '''Hash Table node, part of Linked List'''
      '''each Bucket will contain a linked list of nodes containing
      the objects stored at that index'''
      
      def __init__(self, key, value):
          self.key = key
          self.value = value
          self.next = None
          
      def __str__(self):
          """Retun a string representation of the Object"""
          return "<Node: (%s, %s), next: %s> \t" % (self.key, self.value, self.next.key)
      
      def __repr__(self):
          return str(self)
          

  class HashTable:
      # Initialize Hash Table
      def __init__(self):
          
          self.capacity = initial_capacity 
          self.size = 0
          self.buckets = [None]*self.capacity
          
      
      def hash(self, key):
          
          '''Hash Function will take our Keys and give a index for our Buckets Array! '''
          '''We want our hash values to be evenly distributed among our Buckets '''
          
          hash_sum = 0
          
          for index, c in enumerate(key):
              
              hash_sum += (index + len(key)) ** ord(c)
              
              hash_sum = hash_sum % self.capacity
              
          print("Hash Value for", key, "Is: ", hash_sum)
          
          return hash_sum



      def insert(self, key, value ):
          
          
          
          # 1. Increase size
          
          self.size += 1
          
          # 2. Compute the index of the key (send to hash function)
          
          index = self.hash(key)
          
          # Go to node corresponding to the hash
          
          node = self.buckets[index]
          
      
          if node is None:
              # create a new Node and add
              
              self.buckets[index] = Node(key, value)
              return
          
          # 4. Otherwise there is Collision, since the Bucket has nodes in it
          # so we have to iterate to the end of the Linked list in the Bucket
          
          prev = node
          while node is not None: #loop through linked list
              
              prev = node
              node = node.next
          
          # add a new node to the end of the linked list
          
          prev.next = Node(key,value)
          
      
      def find(self, key):
          
          index = self.has(key)
          
          node = self.buckets[index]
          
          while node is not None and node.key != key:
              node = node.next
          
          if node is None:
              
              return None 
          else:
              # Found and return the data value
              
              return node.value
          
      
      def remove(self, key):
          
          # compute the hash to find 
          
          index = self.hash(key)
          node = self.buckets[index]
          prev = None

          # iterate to requested
          
          while node is not None and node.key != key:
              prev = node
              node = node.next
              
          
          if node is None:
              return None
          
          else:
              
              self.size -= 1
              result = node.value
              
              # delete this element in linked list
              
              if prev is None:
                  self.buckets[index] = node.next
              
              else:
                  prev.next = prev.next.next 
                  
              return result


  ht = HashTable()


  ## lets inserted values into our hash Table
          

                                      
  heat = ["Lebron", "Wade", "Bosh"]

  pistons = ["Wallace", "Billups", "Hamilton", "Prince"]

  bulls =["Jordan", "Pippin", "Rose"]

  bucks = ["Giannas", "Redd", "Allen"]

  clippers = ["Griffin", "Paul"]

  hawks = ["Trae", "Horford"]

  lakers = ["Kobe", "Shaq", "Gasol"]

  warriors = ["Curry", "Klay", "Green"]

  jazz = ["Mitchell", "Gobert"]

  suns =[ "Booker", "Paul", "Ayton"]

  ht.insert("Pistons", pistons)
  ht.insert("Bulls", bulls)
  ht.insert("Bucks", bucks)
  ht.insert("Clippers", clippers)

  ht.insert("Hawks", hawks)
  ht.insert("Lakers", lakers)
  ht.insert("Warriors", warriors)

  ht.insert("Jazz", jazz)
  ht.insert("Suns", suns)







  print("Size of our Hash Table is:", ht.size)
  print("The Current Buckets in our Hash Table: ", ht.buckets)







