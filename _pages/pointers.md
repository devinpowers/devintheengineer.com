---
layout: archive
permalink: /C++/pointers
title: " Pointers in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"

toc: true
toc_label: "Table of Contents" 
---


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


## Pointers

* A pointer is just a **variable** that holds the memory address

``cpp
#include <iostream>

using std::cout;
using std::endl;

int main() {

    int* ptr; // create our pointer

    int var = 7;

    int foo = 21;

    cout << "ptr: " << ptr << endl;
    cout << "var: " << var << endl;
    cout << "foo: " << foo << endl;
 
}
```

**Output:**

```cpp
ptr: 0x10ee0d025
var: 7
foo: 21
```


**Now lets have the pointer (ptr) *point* to something**

* ptr will point to address A

```cpp
#include <iostream>

using std::cout;
using std::endl;

int main() {

    int* ptr; // create our pointer

    int var = 7;

    int foo = 21;

    ptr = &var;

    cout << "ptr: " << ptr << endl;
    cout << "var: " << var << endl;
    cout << "foo: " << foo << endl;
    cout << "ptr value: " << *ptr << endl;
 
}
```

**Output:**

```cpp
ptr: 0x7ffeea2675e4
var: 7
foo: 21
ptr value: 7
```

* Now once we print *ptr* we get  0x7ffeea2675e4, which is the address that it is pointed to (which is the address of **var**)

* Now if we print the dereferenced value of *ptr we get 7



**Now** lets have our pointer point to foo

```cpp
#include <iostream>

using std::cout;
using std::endl;

int main() {

    int* ptr; // create our pointer

    int var = 7;

    int foo = 21;

    ptr = &var;
    ptr = &foo;

    
    cout << "ptr: " << ptr << endl;
    cout << "var: " << var << endl;
    cout << "foo: " << foo << endl;
    cout << "ptr value: " << *ptr << endl;
 
}
```

**Output**

```cpp
ptr: 0x7ffeed3705e0
var: 7
foo: 21
ptr value: 21
```

Now our pointer is pointing to the address of *foo*

That's how pointers work, now what is a **reference?**


* it's just giving another name for the variable, new way to call this location in memory


```cpp
#include <iostream>

using std::cout;
using std::endl;

int main() {

    int* ptr; // create our pointer

    int var = 7;

    int foo = 21;

    ptr = &var;
    ptr = &foo;

    int& ref = var; // reference 


    cout << "ptr: " << ptr << endl;
    cout << "var: " << var << endl;
    cout << "foo: " << foo << endl;
    cout << "ptr value: " << *ptr << endl;
 
}
```

* References can't be moved (to point to foo variable for example)


We could now point back to our variable using either **var** or **ref**

**Difference:**

Pointer has freedom to move around  and point to different variables, while the reference is assigned one time and it just becomes a reference to that location in memory.

![inserting an Image](/images/C++/pointers/point1.jpg)
![inserting an Image](/images/C++/pointers/point2.jpg)


## Difference Between Pass by Value, Pass By Reference, and Pass By Pointer in C++