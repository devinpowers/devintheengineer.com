---
layout: archive
permalink: /algorithms/intro_graph/graphs_dfs
title: "Depth First Search"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
---



Example Code:


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
                

    all_edges = [
        
        ("A","B"),("A","C"),("B","D"),("C","D"),("C","E"),("D","E")
    ]
    nodes = ["A","B","C","D","E"]

    graph1 = Graph(nodes)
    #graph1.print_adj_list()

    for u,v in all_edges:
        graph1.add_edge(u,v)

    ##graph.add_edge("A","B")
    graph1.print_adj_list()



    visited = []

    def dfs(graph, node):
        
        if node not in visited:
            
            visited.append(node)
            
            for neighbor in graph[node]:
                
                dfs(graph,neighbor)
                
        return visited


    dfs(graph1, "A")


    print("Nodes Visted: ", visited)


Output:



    A -> ['B', 'C']
    B -> ['A', 'D']
    C -> ['A', 'D', 'E']
    D -> ['B', 'C', 'E']
    E -> ['C', 'D']
    Nodes Visted:  ['A', 'B', 'D', 'C', 'E']

