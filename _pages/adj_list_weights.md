---
layout: archive
permalink: /algorithms/intro_graph/adj_list_weights
title: "Adjacency List Representation of a Graph with Weights!!!"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
---

![inserting an Image](/images/Graphs/adj_list_weighted/weighted1.jpg)
![inserting an Image](/images/Graphs/adj_list_weighted/weighted2.jpg)


#### Weighted Graph

```python
class Graph:
    
    def __init__(self, Nodes, is_directed = False):
        self.nodes = Nodes
        self.adj_list = {}
        
        self.is_directed = is_directed

        
        for node in self.nodes:
            self.adj_list[node] = {}
        
            
    def add_edge(self, u, v, w):
        
        self.adj_list[u][v] = w
        
        if not self.is_directed:
            
            
            self.adj_list[v][u] = w
        
      
    
    def degree(self,node):
        '''Total number of edges coming out a given node'''
        deg = len(self.adj_list[node])
        return deg
    
    def print_adj_list(self):
        
        for node in self.nodes:
            print(node, "->", self.adj_list[node])
    

```

Lets add some Nodes, Edges, and the corresponding weights 

```python
all_edges = [

    ("A","B", 5),("A","C", 4),("B","D", 6),("C","D", 8),
    ("C","E", 6),("D","E",7)
]
nodes = ["A","B","C","D","E"]



graph1 = Graph(nodes)

for u,v,w in all_edges:
    graph1.add_edge(u,v,w)


```

Lets print our Graph

```python

graph1.print_adj_list()
```

Output:
```python

A -> {'B': 5, 'C': 4}
B -> {'A': 5, 'D': 6}
C -> {'A': 4, 'D': 8, 'E': 6}
D -> {'B': 6, 'C': 8, 'E': 7}
E -> {'C': 6, 'D': 7}

```
