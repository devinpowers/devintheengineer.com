---
layout: archive
permalink: /algorithms/intro_graph/Djikstras
title: "Djikstras Algorithm"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
---


![inserting an Image](/images/Graphs/dijkstras/dijk1.jpg)
![inserting an Image](/images/Graphs/dijkstras/dijk2.jpg)
![inserting an Image](/images/Graphs/dijkstras/dijk3.jpg)
![inserting an Image](/images/Graphs/dijkstras/dijk4.jpg)
![inserting an Image](/images/Graphs/dijkstras/dijk5.jpg)


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
            
    def __len__(self):
        return len(nodes)
        
    def __getitem__(self,node):
        
        """retrives items from out Node/vertex"""
        
        return  self.adj_list[node]
            
    def __iter__(self):
        return iter(self.adj_list)

    
    def degree(self,node):
        '''Total number of edges coming out a given node'''
        deg = len(self.adj_list[node])
        return deg
    
    def print_adj_list(self):
        
        for node in self.nodes:
            print(node, "->", self.adj_list[node])
    

```
Let's add some Nodes(Vertex), Edges, and the weights to our Graph!
```python

all_edges = [

    ("A","B", 4),("A","C", 1),("B","D", 1),("C","D", 5),
    ("C","B", 2),("D","E",3)
]

nodes = ["A","B","C","D","E"]

graph1 = Graph(nodes)

for u,v,w in all_edges:
    graph1.add_edge(u,v,w)


```

```python

graph1.print_adj_list()

```

Graph Printed with Edges and Weights

```python
A -> {'B': 4, 'C': 1}
B -> {'A': 4, 'D': 1, 'C': 2}
C -> {'A': 1, 'D': 5, 'B': 2}
D -> {'B': 1, 'C': 5, 'E': 3}
E -> {'D': 3}

```


 
```python


import heapq

def Dijkstras(graph, starting_vertex):
    distances = {}
    distances = {vertex: float('infinity') for vertex in graph}

    distances[starting_vertex] = 0

    pq = [(0, starting_vertex)]


    while len(pq) > 0:


        current_distance, current_vertex = heapq.heappop(pq)
        
        if current_distance > distances[current_vertex]:
            continue

        for neighbor, weight in graph[current_vertex].items():
            distance = current_distance + weight
           
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                
               
                heapq.heappush(pq, (distance, neighbor))

    return distances

```

```python

Dijkstras(graph1, "A")

```

Distance from Vertex A

```python

{'A': 0, 'B': 3, 'C': 1, 'D': 4, 'E': 7}


```


