---
layout: archive
permalink: /algorithms/intro_graph/graphs_dfs
title: "Depth First Search"
author_profile: true

header:
  image: "/images/chicagotwo.jpeg"
---


def dfs(graph,start):
    visited = set()
    stack = [start]
    
    while stack:
        
        vertex = stack.pop()
        
        if vertex not in visited:
            visited.add(vertex) 
            stack.extend(graph[vertex]-visited)
            
    return visited


# dfs with graph and D which is the starting point

vis = dfs(graph,'D')
print(vis)


