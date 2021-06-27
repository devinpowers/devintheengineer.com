---
layout: archive
permalink: /C++/pointers
title: " Pointers in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

Pointers in C++ Practice.....s



## Pointers vs References in C++

* References is an *alias*, that is, another name for an already exisiting variable

**Example of Reference**

```cpp

int i = 23;

// declare reference variable for i

int& g = i;
```

* The & in these declarations as reference, thus read as "g is an integer reference initialized to i"

**Another Quick Example of a Reference**

```cpp
#include <iostream>

using std::cout;
using std::endl;

int main() {

    int a = 5;

    // int &b = a;

    // int & b = a;

    int &b = a;

    cout << "b: " <<  b << endl;
}
```