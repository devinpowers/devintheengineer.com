---
layout: archive
permalink: /C++/c++_project9
title: "Project 9 in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---


Header File




```cpp
#ifndef FSA_H
#define FSA_H

#include<iostream>
using std::ostream;
#include<fstream>
using std::ifstream;
#include<map>
using std::map;
#include<string>
using std::string;

class FSA{
  
private:
  map<string, map<string, string>> table_;
  string state_;
  string start_;
  string finish_;

public:
  FSA()=default;
  FSA(string strt, string stp);
  FSA(ifstream&);
  bool exists_state(string);
  void add_state(string);
  void add_transition(string, string, string);
  string transitions_to_string(string);
  string next(string,string);
  bool run(string);
  friend ostream& operator<<(ostream&, FSA&);
  // string unreachable();  // something to try, not required
};

#endif
```