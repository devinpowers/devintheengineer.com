---
layout: archive
permalink: /C++/c++_project8
title: "Project 8 in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

Header File

```cpp
#ifndef NETWORK
#define NETWORK

#include<vector>
using std::vector;

#include<utility>
using std::pair;

#include<string>
using std::string;

#include<fstream>
using std::ifstream;


struct Node{

    int x;
    int y;
    string label;

    Node() = default;

    Node(int i, int j, string l) : x(i), j(i), label(l) {}; // constructor

    string_to_string() const;   // method

    bool equal_nodes( const Node&);   // method

    double distance (const Node &);    // method

};


struct Network{

    string label;
    map<string, Node> nodes; // map of Nodes and their labels
    vector<string> route; // shortest route (greedys)

    Network() = default // constructor

    Network(ifstream &);       // ifstream: Stream class to read from files

    string to_string() const;
    Node get_node(string);

    void put_node(string);
    bool in_route(const Node&);
    Node closest(Node &);

    string calculate_route(const Node&, const Node&)

};


#endif
```

