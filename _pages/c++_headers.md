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


```python
hist(res.age, weights=res.c, bins=len(res))

```

```python
(array([9.0000e+00, 1.1020e+03, 1.9080e+03, 3.4280e+03, 7.9690e+03,
        1.1081e+04, 1.1124e+04, 1.5293e+04, 2.3756e+04, 3.3952e+04,
        3.7243e+04, 3.9164e+04, 4.3190e+04, 4.4856e+04, 4.5525e+04,
        4.5658e+04, 4.2212e+04, 3.7426e+04, 3.5366e+04, 3.5985e+04,
        3.2470e+04, 3.2266e+04, 2.8700e+04, 2.6938e+04, 2.6511e+04,
        2.3881e+04, 2.1399e+04, 2.0058e+04, 2.0024e+04, 2.1203e+04,
        1.8918e+04, 1.8235e+04, 1.8477e+04, 1.9608e+04, 2.1527e+04,
        6.4211e+04, 1.7805e+04, 1.7207e+04, 1.6468e+04, 1.7799e+04,
        1.5611e+04, 1.4832e+04, 1.5068e+04, 1.2714e+04, 1.2908e+04,
        1.1178e+04, 9.2370e+03, 9.1710e+03, 7.2410e+03, 6.5590e+03,
        5.4110e+03, 4.8290e+03, 2.9620e+03, 3.0980e+03, 2.4360e+03,
        1.5920e+03, 1.6630e+03, 1.5200e+03, 1.1110e+03, 6.3200e+02,
        4.3500e+02, 6.6900e+02, 5.8800e+02, 4.1600e+02, 5.5300e+02,
        1.0500e+02]),
 array([14.        , 14.98484848, 15.96969697, 16.95454545, 17.93939394,
        18.92424242, 19.90909091, 20.89393939, 21.87878788, 22.86363636,
        23.84848485, 24.83333333, 25.81818182, 26.8030303 , 27.78787879,
        28.77272727, 29.75757576, 30.74242424, 31.72727273, 32.71212121,
        33.6969697 , 34.68181818, 35.66666667, 36.65151515, 37.63636364,
        38.62121212, 39.60606061, 40.59090909, 41.57575758, 42.56060606,
        43.54545455, 44.53030303, 45.51515152, 46.5       , 47.48484848,
        48.46969697, 49.45454545, 50.43939394, 51.42424242, 52.40909091,
        53.39393939, 54.37878788, 55.36363636, 56.34848485, 57.33333333,
        58.31818182, 59.3030303 , 60.28787879, 61.27272727, 62.25757576,
        63.24242424, 64.22727273, 65.21212121, 66.1969697 , 67.18181818,
        68.16666667, 69.15151515, 70.13636364, 71.12121212, 72.10606061,
        73.09090909, 74.07575758, 75.06060606, 76.04545455, 77.03030303,
        78.01515152, 79.        ]),
 <a list of 66 Patch objects>)


```
