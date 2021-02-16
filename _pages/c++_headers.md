---
layout: archive
permalink: /C++/c++_headers
title: "Headers in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

It is common to break a large problem into smaller problems

We do this in C++ where we create seperate file for each code section and then combine them later



### Declaration

 A Declaration function has no function body, but it does have all the types the function uses.

- Knowing the types, the complier can compile (check types) under the assumption that the function definition is provided later at link time.

- A declaration  registers the signature of a function:
    - its name
    - its return type 
    - its parameter types


### Header Files

Header files are those filled with function declarations 

With the functions signature, C++ can check that the types used by calling a program are correct


### An Example of Complile Execute Cycle:


- insert example



We can instruct the complier to comppile but not link with the -c flag

```cpp
g++ -std=c++17 -Wall -g -c file.cpp
```

This will produce a .o file

```cpp
file.o
```

The .o file is an object file to be linked, it's not executable!, it still needs to be linked!

