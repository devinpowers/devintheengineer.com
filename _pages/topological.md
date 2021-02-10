---
layout: archive
permalink: /algorithms/intro_graph/topological
title: "Topological Sort Algorithm"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
---




Creating our "Directed Graph"

```python
class Graph:
    
    def __init__(self, Nodes, is_directed = False):
        self.nodes = Nodes
        self.adj_list = {}
        
        self.is_directed = is_directed
        
        for node in self.nodes:
            self.adj_list[node] = []
            
    def add_edge(self, u, v):
        self.adj_list[u].append(v)
        
        if not self.is_directed:
            
            self.adj_list[v].append(u)
        
    
    def degree(self,node):
        '''Total number of edges coming out a given node'''
        deg = len(self.adj_list[node])
        return deg
    
    def print_adj_list(self):
        
        for node in self.nodes:
            print(node, "->", self.adj_list[node])
    
    def __getitem__(self, node):
        
        """retrives items from out Node/vertex"""
        
        return  self.adj_list[node]
            
```

Lets add out Edges and Nodes

```python
all_edges = [
    
    ("A","D"),("B","D"),("C","B"),("C","A"),("E","A"),("E","D"),
    ("E","F"),("D","H"),("D","G"),("F","K"),("F","J"),("H","J"),
    ("H","I"),("G","I"),("K","J"),("J","M"),("J","L"),("I","L")

]
nodes = ["A","B","C","D","E","F","G","H","I","J","K","L","M"]

```

Lets create a Graph Object 

```python

graph1 = Graph(nodes, is_directed = True)

for u,v in all_edges:
    graph1.add_edge(u,v)

graph1.print_adj_list()

```

Output of Graph:
```python

A -> ['D']
B -> ['D']
C -> ['B', 'A']
D -> ['H', 'G']
E -> ['A', 'D', 'F']
F -> ['K', 'J']
G -> ['I']
H -> ['J', 'I']
I -> ['L']
J -> ['M', 'L']
K -> ['J']
L -> []
M -> []
```