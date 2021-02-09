---
layout: archive
permalink: /algorithms/intro_graph/adj_list
title: "Adjacency List Representation of a Graph"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
---


![inserting an Image](/images/Graphs/adj_list/adj1.jpg)
![inserting an Image](/images/Graphs/adj_list/adj2.jpg)
![inserting an Image](/images/Graphs/adj_list/adj3.jpg)


### Adjacency List Implementation

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
    
    
```

          