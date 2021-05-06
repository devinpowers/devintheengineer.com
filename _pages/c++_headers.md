---
layout: archive
permalink: /C++/c++_headers
title: "Headers in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

### Multiple File Compilation

* In C++ you can compile multiple files separetly which can be combined/linked

* It's very common to break a large problem into smaller problems
* You can actually create seperate files for each code solution and then combine them later (link time)


C++ code files (with a .cpp extension) are not the only files commonly seen in C++ programs. The other type of file is called a **header file**. Header files usually have a .h extension, but you will occasionally see them with a .hpp extension or no extension at all. The **primary purpose** of a **header file** is to propagate *declarations* to code files.

Header files allow us to put **declarations in one location** and then **import them wherever we need them**. This can save a lot of typing in multi-file programs.

### Declaration vs. Definitions

#### Declaration

 A Declaration function has **no function body**, but it does have all **the types** the function uses.

- Knowing the types, the complier can compile (check types) under the assumption that the **function definition** is provided later at link time (which is usually include when you compile a main.cpp and functions.cpp)

- A declaration  registers the *signature* of a function:
    - **its name**
    - **its return type** 
    - **its parameter types**

#### Definitions

* A definition is the actual *body* of the functions 



### Header Files (.h)

Header files are those filled with **Function Declarations**

With the functions signature, C++ can *check that the types* used by calling a program are correct

* When you include (header files) from our own local directory, we use  " "
  * The "" means; *find this file thats in my current directory*
  * **#include "my_header.h"**

* When we include normal header files from the C++ libraries or other standard tools, we use <>
  * #include <iostream>




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

**Declaration Example**

* Which includes the **name of the function** (swap_nodes), its **return type** (void), and its **parameters** (long &, long &)

```cpp
void swap_nodes(long &, long &);
```

**Definition Example**

* Here is the definition of the function, a semicolon at the end of declaration Param name not necessary

```cpp
void swap_nodes(long &first, long &second){
    long temp = first;
    first = second;
    second = temp;
}
```

What are the **benefits** of seperating **definitions** and **declerations**?

- Reusable
- Hides implementation details (the library doesnt need to explain how any of the function need to work)
- Independent coding
- Ease maintenance
- Simplify testing
- Support independent coding

### Libraries

- increases the power of language becuase they allow commonly-used functions to be shared

What are the **components** in a Library?

1. **Header File**
- Interface
- Declarations
- Templates
- Inserted into using program using **#include**

2. **Implementation File**

- (Function) Definitions
- Classes (covered in bit later!!!)
- Must be seperately complied and linked by the complier (.o files)



### Public / Private

Public
- Items defined in the implementation file that are declared in the header file can be used by any program which includes the header

Private
- Items defined in the implementation that are not declared in the header file cannot be used by any program, even if they include the header file


## Example of Header Files and Separate Compilation


**We have 3 files**

**functions.h** File

  * Includes the decleration of the function **f1**


```cpp
#ifndef DEFAULT_TEST
#define DEFAULT_TEST

long f1(long p1, long p2=2);

#endif
```

**functions.cpp** File
  
  * Includes the definition of the function **f1**

```cpp
#include "functions.h"

long f1(long p1, long p2){
  return p1 * p2;
}
```

**main.cpp** File

  * Main file, that calls our function!

```cpp
#include<iostream>
using std::cout; using std::endl;

#include "functions.h"

int main(){
  cout << f1(10,20) << endl;
  cout << f1(20) << endl;
}
```


**Lets compile and run**

Terminal:

```cpp
g++ main.cpp functions.cpp
./a.out
```


**Output:**

```cpp
200
40
```

* That was so much fun!!

### Multiple File Compilation

**Question**

What files need to be compiled?

**All .cpp files!**


##### Preprocessor

* The Preprocessor allows us to modify our code before it compiles!

Here are three important preprocessor commands (**header guards**)

#ifndef some_variable_we_make_up
#define some_variable_we_make_up

... stuff we want to include..

#endif




**Heres a bigger example:**

**support.h** File

```cpp
#ifndef ROOTS_SOLVER
#define ROOTS_SOLVER

bool get_coefficients( double &, double &, double & );
int roots( double, double, double, double &, double & );

#endif
```

**support.cpp** File

```cpp
#include <iostream>
using std::cout; using std::endl; using std::cin;
#include <cmath>
using std::sqrt;

#include "support.h"

/*
  Purpose:  Accept the three coefficients of 
            an equation from the user.
  params:   Coefficients (A, B and C) of the equation
  return: True if "end-of-file"; 
        : false otherwise (as the return expression)
*/

bool get_coefficients( double & A, double & B,
		       double & C ){
    int status;

    cout << "\nEnter quadratic equation coefficients\n";
    cout << "(space separated A, B and C, EOF to halt):";
    cin >> A >> B >> C;

    if (cin.eof())
	    status = false;
    else
	    status = true;

    return status;
}

/*
  Purpose: Given the coefficients, compute roots
           of a quadratic equation.
  params: (A, B and C) of the equation
          root_1, root_2 (as ref parameters)
  return status:(3-not a quad, 2-complex,
                1-one real root, 0-two real roots
*/

int roots(double A, double B, double C,
	      double & root_1, double & root_2){
    int status;
    double discriminant;

    if (A == 0.0) {
	status = 3;    // Not a quadratic equation
    } else {
        discriminant = B*B - 4.0*A*C;
        if (discriminant < 0.0) {
            status = 2;    // two complex roots
        } else if (discriminant == 0.0) {
            status = 1;    // one real root
            root_1 = (-B)/(2.0*A);
        } else {
            status = 0;    // two real roots
            root_1 = (-B + sqrt(discriminant))/(2.0*A);
            root_2 = (-B - sqrt(discriminant))/(2.0*A);
        }
    }
    return status;
}
```


**main.cpp** File

```cpp
#include <iostream>
using std::cout; using std::endl; using std::fixed;
#include <iomanip>
using std::setprecision; 

#include "support.h"

int main(){
    int input_status, root_status;
    double A, B, C, root_1, root_2;

    cout << fixed << setprecision( 1 );

    input_status = get_coefficients( A, B, C );
    while (input_status != 0) {
		root_status = roots( A, B, C, root_1, root_2 );
		cout << endl << "The equation:" << endl;
		cout << "  " << A << " x^2 + " << B
			<< " x + " << C << endl;
		switch (root_status) {
			case 0:
				cout << "\n has the following roots"<<endl;
				cout << "  root 1 = " << root_1 << endl;
				cout << "  root 2 = " << root_2 << endl;
				break;
			
			case 1:
				cout <<"\n has the following root:" << endl;
				cout << "  root = " << root_1 << endl;
				break;
			
			case 2:
				cout << endl << "has complex roots." << endl;
				break;
			
			case 3:
				cout << "\n is not quadratic." << endl;
				break;
		}
		input_status = get_coefficients( A, B, C );
    }
}

```

![inserting an Image](/images/C++/headers/quad1.jpg)
![inserting an Image](/images/C++/headers/quad2.jpg)

