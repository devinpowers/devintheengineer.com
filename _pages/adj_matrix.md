---
layout: archive
permalink: /algorithms/intro_graph/adj_matrix
title: "Adjacency Matrix Representation of a Graph"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
---


![inserting an Image](/images/Graphs/adj_matrix/adj_matrix1.jpg)
![inserting an Image](/images/Graphs/adj_matrix/adj_matrix2.jpg)



### Adjacency Matrix Implementation

```python
class Graph():
    
    def __init__(self, matrix_size):
        self.matrix = []
        self.matrix_size = matrix_size
        
        # add to our matrix using the size passed in
        
        for i in range(matrix_size):
            self.matrix.append([0 for i in  range(matrix_size)])
    
    def print_matrix(self):
        """Prints our matrix out"""
        
        for row in self.matrix:
            print(row)
    
    def size(self):
        """Returns Size of the Matrix"""
        return self.matrix_size
    
    def add_edge(self, vertex_1, vertex_2):
        
        if vertex_1 == vertex_2:
            print("Same vertex passed in!")
            return
        
        self.matrix[vertex_1][vertex_2] = 1
        self.matrix[vertex_2][vertex_1] = 1

    
    def remove_edge(self, vertex_1, vertex_2):
        
        if self.matrix[vertex_1][vertex_2] == 0:
            print("No edge exisited between the 2")
            return
        
        self.matrix[vertex_1][vertex_2] = 0
        self.matrix[vertex_2][vertex_1] = 0

```

Create a Graph Instance:

```python
g = Graph(5)

print("Matrix Before:")
g.print_matrix()

print("Size of the Matrix: ", g.size())

## adding edges
g.add_edge(0, 2)
g.add_edge(1, 2)
g.add_edge(2, 0)
g.add_edge(2, 3)

print("Matrix After Adding Edges:")
g.print_matrix()

# removing edges from Matrix
g.remove_edge(0,3)
g.remove_edge(0,2)

print("Matrix after removing certain Edges:")
g.print_matrix()

```

Output the Graph:

```python
Matrix Before:
[0, 0, 0, 0, 0]
[0, 0, 0, 0, 0]
[0, 0, 0, 0, 0]
[0, 0, 0, 0, 0]
[0, 0, 0, 0, 0]
Size of the Matrix:  5
Matrix After Adding Edges:
[0, 0, 1, 0, 0]
[0, 0, 1, 0, 0]
[1, 1, 0, 1, 0]
[0, 0, 1, 0, 0]
[0, 0, 0, 0, 0]
No edge exisited between the 2
Matrix after removing certain Edges:
[0, 0, 0, 0, 0]
[0, 0, 1, 0, 0]
[0, 1, 0, 1, 0]
[0, 0, 1, 0, 0]
[0, 0, 0, 0, 0]

```