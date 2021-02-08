---
layout: archive
permalink: /algorithms/intro_graph/graphs_dfs
title: "Depth First Search"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
---



Example Code:


    graph1 = {
        'A' : ['B','S'],
        'B' : ['A'],
        'C' : ['D','E','F','S'],
        'D' : ['C'],
        'E' : ['C','H'],
        'F' : ['C','G'],
        'G' : ['F','S'],
        'H' : ['E','G'],
        'S' : ['A','C','G']
    }

    visited = []

    def dfs(graph, node):
        
        if node not in visited:
            visited.append(node)
            for neighbor in graph[node]:
                dfs(graph,neighbor)
        return visited


    dfs(graph1, "E")


Output

    ['E', 'C', 'D', 'F', 'G', 'S', 'A', 'B', 'H']


        

