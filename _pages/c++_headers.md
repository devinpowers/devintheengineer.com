---
layout: archive
permalink: /C++/c++_headers
title: "Headers in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

C++ code files (with a .cpp extension) are not the only files commonly seen in C++ programs. The other type of file is called a header file. Header files usually have a .h extension, but you will occasionally see them with a .hpp extension or no extension at all. The primary purpose of a header file is to propagate declarations to code files.

Header files allow us to put declarations in one location and then import them wherever we need them. This can save a lot of typing in multi-file programs.

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

We have 3 files:

1. functions.cpp

```cpp

#include "functions.h"


long f1(long p1, long p2){
  return p1 * p2;
}

```

2. main.cpp

```cpp

#include<iostream>
using std::cout; using std::endl;

#include "functions.h"

int main(){
  cout << f1(10,20) << endl;
  cout << f1(20) << endl;
}

```

3. functions.h

```cpp
#ifndef DEFAULT_TEST
#define DEFAULT_TEST

long f1(long p1, long p2=2);

#endif

```

We see that the Header file contains Declerations


As you can see both the main.cpp and support.cpp file have the #include "support.h" file,
when we include header files from C++ standard libraries or other tools we use the angle brackets <>
- #include <iosteam>

But when we include from our own local directory we use " "

- #include "header.h"


How do we complile everything?

- lets go to our terminal

```cpp
g++ -Wall -std=c++17 -c functions.cpp
```
Will return -> functions.o file

```cpp
g++ -Wall -std=c++17 -c main.cpp
```
Will return -> main.o file

Now that we have object files we can link them

```cpp
g++ main.o functions.o
```

Will return -> a.out

Now we can run the File (a.out or outfile.exe)

```
./a.out
```


We can also just compile in one-step:

```cpp
g++ -Wall -std=c++17 main.cpp functions.cpp
```

And it spits out the a.out file, that we can run to execute the program!!

```
./a.out
```

more to come......