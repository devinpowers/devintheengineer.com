---
layout: archive
permalink: /C++/c++_project8
title: "Project 8 in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---


Project creating a **Ad-Hoc Network**!


**Header File** (Given in Problem)

(functions.h)

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
  // Attributes
  int x;
  int y;
  string label;

  Node()=default;  // Default constructor
  Node(int i, int j, string l) :  x(i), y(j), label(l) {} ;  // Constructor with 3 Argumennts passsed in!

  // Methods on Node
  string to_string () const;        // Method that converts the Node to a string displaying the x,y and label
  bool equal_nodes(const Node &);        // Method that checks if the 2 nodes passed in are equal
  double distance(const Node &)const;   // Method that checks the distance between two nodes passed in
};

struct Network{
  // Attributrs
  string label;              
  map<string, Node> nodes;      // Map of our Network of Labels and Nodes
  vector<string> route;         // Route of our Nodes

  Network()=default; // Default constructor
  Network(ifstream &);   // Constructor that is defined outside in the function.cpp file


  // Methods on Networks
  string to_string () const; // Uses Nodes Struct to print ! (const means it won't modify the variable)

  Node get_node(string);  // Gets a node

  void node_to_network(Node);      // Adds Node to Network
  
  bool in_route(const Node&);
  Node closest(Node &);
  string calculate_route(const Node&, const Node&);
};

#endif

```


**Functions**

Heres the functions for the **Node Struct**

```cpp
//NODE FUNCTIONS
string Node::to_string () const {
    // returns one big string that has the " label: (x:y) " of the node
    ostringstream oss;
    // Puts everything into the oss keyword below 
    //Label:(X,Y)

    oss << label << ":(" << x << "," << y << ")";
    // Returns oss string
    return oss.str();
}

bool Node::equal_nodes(const Node & other){
    //Can assume that the nodes are equal if the labels are the same
    // With other being the other node that you're comparing it too!
    return label == other.label;
}

double Node::distance(const Node & other) const{
    //Distance is the square root of the coordinates subtracted and squared
    // the other is the other node passed in
    return sqrt(pow(x-other.x, 2) + pow(y - other.y, 2));
}

```

Heres the functions/methods for the **Network Struct**

```cpp
Network::Network(ifstream &file){

    // Constructor
    // Takes in input/reads from file (.txt) into our varaibles
    
    long first, second;
    string label;

    // Lets get the values from each line
    while(file >> first >> second >> second >> label){
        // reads file and now we need to create a node and put the node into our Network
        // The constructor of the Node will work
        // The node_to_network will first create a node for each line in the file, and then add it to the Network
        node_to_network(Node(first, second, label));

    }

}

string Network::to_string() const {

    // Reads the Entire Network and prints it out via one big string using ostringstream
    // Uses the to_string method for the individual nodes 
    ostringstream oss;
    string s;


    for (pair<string, Node> p : nodes){
        // iterates  our "nodes" map in the Network 
        // calls for the to_string() method, which returns --> label:(x,y)

        oss << p.second.to_string() << ",";
    }
    // oss is now one long string of label:(x,y), label:(x,y), label:(x,y), etc
    s = oss.str();
    // Remove last comma and space
    s = s.substr(0, s.size()- 2);

    // Returns one Long string that is of our Network!!!!
    return s;
}


void Network::node_to_network(Node new_node){
    // pass in new node that we created from the file and add it the list of nodes

    nodes[new_node.label] = new_node;
}

Node Network::get_node(string s){

    // Searches for Node and adds it if need 
    auto iter = nodes.find(s);
    // If the string is not in the nodes, throw the error
    if (iter == nodes.end()){
        // Throw a error
        string error_string = "Node was not found: " + s;
        throw std::out_of_range(error_string);
    }
    // Else the node was found and we can return it
    pair<string, Node> p = *iter;
    // Return the Node
    return p.second;

}

bool Network::in_route( const Node& node){

    // Checks to seee if the node is not in the route

    if (find(route.begin(), route.end(), node.label) == route.end()){
        return false;
    }
    // Else return true if it's in the route

    return true;

}

Node Network::closest(Node & node){

    double shortest_distance = 100000000.0;
    Node closest;
    // Loop thru each pair

    for (pair<string, Node> p : nodes){
        // find the node in the route
        auto it = find(route.begin(),route.end(), p.second.label);
        // if the nodes are not the same, and the node is not in the route
        if (! p.second.equal_nodes(node) && (it == route.end())){
            // check to see if it is the closet
            if (node.distance(p.second) < shortest_distance){
                shortest_distance = node.distance(p.second);
                closest = p.second;
            }
        }
    }
    return closest;


}

string Network::calculate_route(const Node& start, const Node& end){
    ostringstream oss;
    string s;
    double total_distance = 0.0;
    Node last_node;

    // Set the first node
    route.push_back(start.label);
    Node next_closet = start;

    while(! next_closet.equal_nodes(end)){
        // Store last node
        last_node = next_closet;
        //find the next closet
        next_closet = closest(last_node);
        total_distance += last_node.distance(next_closet);
        // add to the route
        route.push_back(next_closet.label);
    }
    // Lets crerate a output string

    oss << total_distance << ": ";
    copy(route.begin(), route.end(),std::ostream_iterator<string>(oss,","));
    s = oss.str();
    s = s.substr(0, s.size() - 1);
    return s;

}  

```


**Main File**

(main.cpp)

```cpp
#include<iostream>
using std::cout; using std::endl; using std::cin; using std::ostream;
using std::boolalpha;
#include<iomanip>
using std::setprecision;
#include<vector>
using std::vector;
#include<map>
using std::map;
#include<utility>
using std::pair; using std::make_pair;
#include<string>
using std::string; using std::getline;
#include<algorithm>
using std::copy; using std::sort; using std::transform;
#include<iterator>
using std::ostream_iterator;
#include<fstream>
using std::ifstream;
#include<sstream>
using std::istringstream; using std::ostringstream;
#include<stdexcept>
using std::out_of_range;
#include<cmath>

#include "functions.h"

int main(){
  cout << boolalpha;

  int test_no;
  cin >> test_no;

  switch(test_no){

  case 1:{
    Node n(10,10,"temp");
    cout << n.to_string() << endl;
    break;
  }

  case 2:{
    Node n1(10,10, "tens");
    Node n2(20, 20, "twentys");
    cout << n1.equal_nodes(n2) << endl;
    cout << n1.equal_nodes(n1) << endl;
    break;
  }

  case 3:{
    Node n1(10,10, "tens");
    Node n2(20, 20, "twentys");
    cout << n1.distance(n2) << endl;
    break;
  }

  case 4:{
    string fname;
    cin >> fname;
    ifstream fin(fname);
    Network net(fin);
    Node n = net.nodes["A"];
    cout << n.to_string() << endl;
    break;
  }

  case 5:{
    string fname;
    cin >> fname;
    ifstream fin(fname);
    Network net(fin);
    cout << net.to_string() << endl;
    break;
  }

  case 6:{
    string fname;
    cin >> fname;
    ifstream fin(fname);
    Network net(fin);
    Node n1, n2;
    try{
      n1 = net.get_node("A");
      n2 = net.get_node("X");
    }
    catch (out_of_range &e){
      cout << "Error:"<< e.what() << endl;
    }
    cout << n1.to_string() << endl;
    break;
  }

  case 7:{
    Network net;
    net.node_to_network( Node(10,10,"tens") );
    net.node_to_network( Node(20, 20, "twentys") );
    cout << net.to_string() << endl;
    net.node_to_network( Node(100, 100, "tens") );
    cout << net.to_string() << endl;    
    break;
  }

  case 8:{
    Network net;
    Node n1(10,10,"tens");
    Node n2(100, 100, "hundreds");
    net.route={"tens", "twentys"};
    cout << net.in_route(n1) << endl;
    cout << net.in_route(n2) << endl;
    break;
  }
    
  case 9:{
    string fname;
    cin >> fname;
    ifstream fin(fname);
    Network net(fin);
    auto n = net.get_node("A");
    auto close = net.closest(n);
    cout << close.to_string() << endl;
    cout << close.distance(n) << endl;
    break;
  }

  case 10:{
    string fname;
    cin >> fname;
    ifstream fin(fname);
    Network net(fin);
    Node n1 = net.get_node("A");
    Node n2 = net.get_node("D");
    cout << net.calculate_route(n1,n2) << endl;
    break;
  }
  case 11: {
      ifstream fin("empty.txt");
      Network net(fin);
      cout << net.to_string() << endl;
  }
  case 12:{
      string fname;
      cin >> fname;
      ifstream fin(fname);
      Network net(fin);
      Node n1 = net.get_node("A");
      Node n2 = net.get_node("A");
      cout << net.calculate_route(n1,n2) << endl;
      break;
  }
      case 13:{
          ifstream fin("network_same.txt");
          Network net(fin);
          Node n1 = net.get_node("A");
          Node n2 = net.get_node("H");
          cout << net.calculate_route(n1,n2) << endl;
          break;
      }


  }// of switch
} // of main

```




**Example Input and Output**