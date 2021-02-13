---
layout: archive
permalink: /algorithms/intro_graph/graph_project
title: "Graph Project"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
---


```python
import math
from operator import itemgetter

class Graph:
    def __init__(self, n):
        """
        Constructor
        :param n: Number of vertices
        """
        self.nodes = n
        
        self.size = 0

        self.graph = {}
        
        #inner Dictionary
        for node in self.nodes:
            self.graph[node] = {}
    
    def print_nodes(self):
        return self.nodes
    
    def insert_edge(self, u, v, w):
        #first check if vertex is already in the Graph
        # funciton creates a new edge
        ## non-directed graph
        self.graph[u][v] = w
        
        self.graph[v][u] = w
        
        #increase size of graph
        self.size += 1 
    
    def _print(self):
        
        for node in self.nodes:
            print(node, "->", self.graph[node])

    def degree(self, v):
        
        '''number of edges connected to a vertex'''
        
        if v not in self.nodes:
            
            print("Dude this Vertex is not in the Graph!!!")
            
            raise IndexError 
    
        return len(self.graph[v])
        
         

    def are_connected(self, u, v):
        '''See if two vertices are connected!'''
        '''Return Boolean (True or False)'''
        
        if u not in self.nodes or v not in self.nodes:
            print("The Vertex, Edge, or both are not in Graph")
        
            raise IndexError
        
        return v in self.graph[u]
    
    
    def is_path_valid(self, path):
        
        '''is path valid'''
        '''Pass in a list of vertices in the order of the path'''
        
        for i in range(len(path) - 1):
            # if not connected, then it's not a path and we can return False
            
            print(path[i])
            
            if not self.are_connected(path[i], path[i+1]):
                return False
        
        return True
        
    def edge_weight(self, u, v):
        
        '''Returns the weight between vertices'''
        # Check if vertices exists
        if u not in self.nodes or v not in self.nodes:
            raise IndexError
        # ok they exist, so lets see if they're connected
        if v in self.graph[u]:
            
            return self.graph[u][v]
        
        else:
            return math.inf
        
        
        return math.inf

    def path_weight(self, path):
        '''get the total weight of a path'''
        '''Return weight of a Path'''
        weight = 0
        
        for i in range(len(path) - 1 ):
            weight += self.edge_weight(path[i], path[i+1])
            
        return weight
    
    def does_path_exist(self, u, v):
        

        # Vertex not in graph
        if u not in self.nodes or v not in self.nodes:
            raise IndexError
        
        #Create a Queue
        queue = []        
        # Keep track of which vertices we've visited

        visited = []
        visited.append(u)
        queue.append(u)
    
        # while Queue isnt empty
        while queue:
            
            vertex = queue.pop(0)
                        
            # Found path is found
            if vertex == v:
                return True
            
            for neighbour in self.graph[vertex]:
                if neighbour not in visited:
            
                    queue.append(neighbour)                      # if neighbour node hasnt been visited we will add to the Queue 
                    visited.append(neighbour)                # and add it to the list of visited nodes
        
              #  else:
                 #   print("Already Visited that node!")       # if the neighbour is already in our visited list we alread visited it!!
        
        #if path doesnt exist
        return False


```