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

What do we need to do with our .o files?

The .o file is an object file to be linked, it's not executable!, it still needs to be linked!

We can compile all of our .cpp files into .o files, then we can subsequently run the linker on the .o file to produce an executable:

```cpp
g++ file1.o file2.o -o outfile.exe
```

Here, the -o allows us to name the executable (.exe is common)
- Note that one of the .o files must have a main function or you will get a link error


### Declaration vs Definition

Declaration Example

```cpp
void swap_nodes(long &, long &);
```

Definition Example
```cpp
void swap_nodes(long &first, long &second){
    long temp = first;
    first = second;
    second = temp;
}
```

What are the benefit of seperating definitions and declerations?

- Reusable
- Hides implementation details (the library doesnt need to explain how any of the function need to work)
- Independent coding



### Libraries

- increases the power of language becuase they allow commonly-used functions to be shared

What are the components in a Library

1. Header File
- interface
- declarations
- templates
- inserted into using program using #include


2. Implementation File

- (Function) Definitions
- Classes
- Must be seperately complied and linked by the complier (.o files)


** insert Picture here **


### Public / Private

Public
- Items defined in the implementation file that are declared in the header file can be used by any program which includes the header

Private
- Items defined in the implementation that are not declared in the header file cannot be used by any program, even if they include the header file


### Example of Header Files and Separate Compilation

*** insert photos ***

