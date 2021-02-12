---
layout: archive
permalink: /algorithms/intro_graph/Djikstras
title: "Djikstras Algorithm"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
---


Heres are Graph:


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

```python

graph1.print_adj_list()

```

Graph Printed with Edges and Weights

```python
A -> {'B': 5, 'C': 4}
B -> {'A': 5, 'D': 6}
C -> {'A': 4, 'D': 8, 'E': 6}
D -> {'B': 6, 'C': 8, 'E': 7}
E -> {'C': 6, 'D': 7}

```


 
```python

import heapq

def calculate_distances(graph, starting_vertex):
    distances = {}
    distances = {vertex: float('infinity') for vertex in graph}
    
    distances[starting_vertex] = 0
    
    
    ## Priority Queue
    pq = [(0, starting_vertex)]
    
    
    while len(pq) > 0:
        
        print("Current Priority Queue:",pq)
        
        current_distance, current_vertex = heapq.heappop(pq)
        

        # Nodes can get added to the priority queue multiple times. We only
        # process a vertex the first time we remove it from the priority queue.
        
        if current_distance > distances[current_vertex]:
            continue

        for neighbor, weight in graph[current_vertex].items():
            distance = current_distance + weight

            # Only consider this new path if it's better than any path we've
            # already found.
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                print("Distance:", distance)
                print("Neighbor:", neighbor)
                print("Next")
                heapq.heappush(pq, (distance, neighbor))
                
                print("Priority Q now: ", pq)

    return distances

```

```python

{'A': inf, 'B': inf, 'C': inf, 'D': inf, 'E': inf}

```

```python

calculate_distances(graph1, "A")

```

Distance from Vertex A

```python

{'A': 0, 'B': 3, 'C': 4, 'D': 9, 'E': 10}


```


