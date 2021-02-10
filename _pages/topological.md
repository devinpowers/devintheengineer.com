---
layout: archive
permalink: /algorithms/intro_graph/topological
title: "Topological Sort Algorithm"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
---




![inserting an Image](/images/Graphs/topo/top1.jpg)
![inserting an Image](/images/Graphs/topo/top2.jpg)
![inserting an Image](/images/Graphs/topo/top3.jpg)
![inserting an Image](/images/Graphs/topo/top4.jpg)
![inserting an Image](/images/Graphs/topo/top5.jpg)
![inserting an Image](/images/Graphs/topo/top6.jpg)
![inserting an Image](/images/Graphs/topo/top7.jpg)





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
            
    def __len__(self):
        return len(self.nodes)
    
    def __getitem__(self, node):
        
        """retrives items from out Node/vertex"""

        return  self.adj_list[node]
    
    def __iter__(self):
        """ This will allow us to iterate over our Graph Object"""
        """ We can iterate over the keys or "Vertexs" by: """
        """ using just the Object->  graph:  """
        return iter(self.adj_list)
    
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

Let's add a Deque Data Structure

```python

class Deque:
    def __init__(self):
        self.items = []

    def isEmpty(self):
        return self.items == []

    def addFront(self, item):
        self.items.append(item)

    def addRear(self, item):
        """ add to rear"""
        self.items.insert(0,item)

    def removeFront(self):
        return self.items.pop()

    def removeRear(self):
        return self.items.pop(0)

    def size(self):
        return len(self.items)
    
    def _print(self):
        '''print Deque Values'''
        return self.items
        
```


Now lets Create a Topological Function and Corresponding DFS

```python

def dfs(graph, source, stack, visited):
    
    visited.append(source)

    for neighbour in graph[source]:
    
        if neighbour not in visited:
            
            dfs(graph, neighbour, stack, visited)

    stack.addRear(source)



def topological_sort_of(graph):
    
    stack = Deque() 
    visited = []

    for vertex in graph:
        
        if vertex not in visited:
            
            dfs(graph, vertex, stack, visited)
    
    return stack
```

Running our Topological Sort Algorithm
```python

topological_ordering = topological_sort_of(graph1)

topological_ordering._print()

```

Topological Ordering Output:


```python

['E', 'F', 'K', 'C', 'B', 'A', 'D', 'G', 'H', 'I', 'J', 'L', 'M']

```