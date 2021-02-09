---
layout: archive
permalink: /algorithms/intro_graph/graph_bfs
title: "Breadth First Search"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
---


Graph Search, why?

we can explore a graph!


Applications:

- Web Crawling
- Social Networking
- Solving Puzzles and Games

![inserting an Image](/images/Graphs/bfs/bfs1.jpg)
![inserting an Image](/images/Graphs/bfs/bfs2.jpg)
![inserting an Image](/images/Graphs/bfs/bfs4.jpg)
![inserting an Image](/images/Graphs/bfs/bfs5.jpg)
![inserting an Image](/images/Graphs/bfs/bfs6.jpg)
![inserting an Image](/images/Graphs/bfs/bfs7.jpg)
![inserting an Image](/images/Graphs/bfs/bfs8.jpg)



Example Code:

Queue Code:

```python
class Queue:

    def __init__(self):
        self.queue = []
        self.size = 0;

    def enqueue(self, item):
        """Add to Queue"""
        self.queue.append(item)
        self.size += 1

    def dequeue(self):
        """pop/remove from Queue"""
        if len(self.queue) < 1:
            return None
        return self.queue.pop(0)
        self.size -= 1
    
        
    def is_empty(self):
        "Return True if the queue is empty"
        return self.size == 0
    
```

Graph Code:
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

Lets created a Graph instance and the Vertex/Nodes and Edges

```python
all_edges = [ 
    
    ("A","B"), ("A","E"), ("B","E"), ("E","D"), ("B","D"), ("A","C"), ("C","F"), ("C","G")
]
nodes = ["A","B","C","D","E", "F", "G"]


graph1 = Graph(nodes)

for u,v in all_edges:
    graph1.add_edge(u,v)

graph1.print_adj_list()
```

Here is out Graph:

```python

A -> ['B', 'E', 'C']
B -> ['A', 'E', 'D']
C -> ['A', 'F', 'G']
D -> ['E', 'B']
E -> ['A', 'B', 'D']
F -> ['C']
G -> ['C']

```

Breadth-First Search


```python
def bfs(graph, start):
    # keep track of all visited nodes
    visited = []
    queue = Queue()
    queue.enqueue(start)
 
    # keep looping until there are nodes still to be checked
    while not queue.is_empty():
    
    
        node = queue.dequeue()
        
        if node is None:
            break
        
        if node not in visited:
            visited.append(node)
            neighbours = graph[node]
 
            for neighbour in neighbours:
                queue.enqueue(neighbour)
    return visited

print("Breadth First Search, Nodes visited: ")
print(bfs(graph1,'A') )

```


Output:

```python

Breadth First Search, Nodes visited: 
['A', 'B', 'E', 'C', 'D', 'F', 'G']
```

