---

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

```cpp
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

**Code:**

```cpp

#include <iostream>

using std::cout;
using std::endl;

// What is the Difference Between Pass By Value, Pass By Reference, and Pass By Pointer, C++

// Functions
void passByVal(int val);   // passing in a copy of an integer
void passByRef(int & ref); // Pass in the actual variable
void passByPtr(int *ptr);  // pass by pointer


int main() {

    // Pass by variable    
    int x = 5;
    cout << "x = " << x << endl;
    passByVal(x);
    cout << "x = " << x << endl;

    // Pass by Reference

    int y = 10;
    passByRef(y);
    cout << "y = " << y << endl;

    // Pass by Pointer
    
    int c = 10;

    int* cptr = &c; // pointer, reference to c
    cout << "c = " << c << endl;
    cout << "*cptr = " << *cptr << endl;
    cout << "cptr (address) = " << cptr << endl;

    passByPtr(cptr);

    cout << "c = " << c << endl;
    cout << "*cptr = " << *cptr << endl;
    cout << "cptr (address) = " << cptr << endl;

    
}

void passByVal(int val)
{
    // pass a copy of the integer we provided
    val = 10;
    cout << "val = " << val << endl;
}

void passByRef(int & ref)
{
    ref = 20;
    cout << "ref = " << ref << endl;
}

void passByPtr(int * ptr)
{   
    // reference the pointer we passed in
    *ptr = 30;

    cout << "*ptr = " << *ptr << endl;
    cout << "ptr (address) = " << ptr << endl;
}
```

**Output:**

```cpp
x = 5
val = 10
x = 5
ref = 20
y = 20
c = 10
*cptr = 10
cptr (address) = 0x7ffee828a8d4
*ptr = 30
ptr (address) = 0x7ffee828a8d4
c = 30
*cptr = 30
cptr (address) = 0x7ffee828a8d4
```



- insert notes here


### What is the Difference Between Pass By Pointer and Pass By Pointer Reference (int * and int * &)?

![inserting an Image](/images/C++/pointers/ref_point.jpg)

**Code:**

```cpp
#include <iostream>

using std::cout;
using std::endl;


void passByPtr(int * ptr);
void passByPtrRef(int * & ptrRef); // integar pointer reference 

int * gptr;


int main() {

    int box1 = 1;
    int box2 = 2;

    int * p = &box1; // integer pointer

    gptr = &box2;

    cout << "_________ Current Conditions _______" << endl;

    // passByPtr(p);


    // passByPtrRef(p);

    if (p == &box1)
    {
        cout << "p is pointing to box1 " << endl;
    }
    else if (p == &box2 )
    {
        cout << "p is pointing to box2" << endl;
    }
    else
    {
        // won't see this though
        cout << "p is pointing to another box " << endl;
    }

    if (gptr == &box1)
    {
        cout << "gptr is pointing to box1 " << endl;
    }
    else if (gptr == &box2)
    {
        cout << "gptr is pointing to box2 " << endl;
    }
    else 
    {
        // won't see this though
        cout << "gptr is pointing to another box" << endl;
    }

    cout << "box1 contains the value: " << box1 << endl;
    cout << "box2 contains the value: " << box2 << endl;

}

void passByPtr( int *ptr )
{
    *ptr = 3;
    ptr = gptr;

    *ptr = 4;
    cout << "____passByPtr has been called______" << endl;
}

void passByPtrRef( int* & ptrRef)
{
    *ptrRef = 5;
    ptrRef = gptr;
    *ptrRef = 6;
    cout << "_______passByPtrRef has been called____" << endl;
}
```

**Output:**

```cpp
_________ Current Conditions _______
p is pointing to box1 
gptr is pointing to box2 
box1 contains the value: 1
box2 contains the value: 2
```


#### Pass by Pointer Example:

![inserting an Image](/images/C++/pointers/pass_point.jpg)

```cpp
#include <iostream>

using std::cout;
using std::endl;


void passByPtr(int * ptr);
void passByPtrRef(int * & ptrRef); // integar pointer reference 

int * gptr;


int main() {

    int box1 = 1;
    int box2 = 2;

    int * p = &box1; // integer pointer

    gptr = &box2;

    cout << "_________ Current Conditions _______" << endl;

    passByPtr(p);


    // passByPtrRef(p);

    if (p == &box1)
    {
        cout << "p is pointing to box1 " << endl;
    }
    else if (p == &box2 )
    {
        cout << "p is pointing to box2" << endl;
    }
    else
    {
        // won't see this though
        cout << "p is pointing to another box " << endl;
    }

    if (gptr == &box1)
    {
        cout << "gptr is pointing to box1 " << endl;
    }
    else if (gptr == &box2)
    {
        cout << "gptr is pointing to box2 " << endl;
    }
    else 
    {
        // won't see this though
        cout << "gptr is pointing to another box" << endl;
    }

    cout << "box1 contains the value: " << box1 << endl;
    cout << "box2 contains the value: " << box2 << endl;

}

void passByPtr( int *ptr )
{
    *ptr = 3;
    ptr = gptr;

    *ptr = 4;
    cout << "____passByPtr has been called______" << endl;
}

void passByPtrRef( int* & ptrRef)
{
    *ptrRef = 5;
    ptrRef = gptr;
    *ptrRef = 6;
    cout << "_______passByPtrRef has been called____" << endl;
}
```

**Output:**

```cpp
_________ Current Conditions _______
____passByPtr has been called______
p is pointing to box1 
gptr is pointing to box2 
box1 contains the value: 3
box2 contains the value: 4
```


#### Pass by Pointer Reference Example:

![inserting an Image](/images/C++/pointers/pass_ref.jpg)


```cpp
#include <iostream>

using std::cout;
using std::endl;


void passByPtr(int * ptr);
void passByPtrRef(int * & ptrRef); // integar pointer reference 

int * gptr;


int main() {

    int box1 = 1;
    int box2 = 2;

    int * p = &box1; // integer pointer

    gptr = &box2;

    cout << "_________ Current Conditions _______" << endl;

    // passByPtr(p);


    passByPtrRef(p);

    if (p == &box1)
    {
        cout << "p is pointing to box1 " << endl;
    }
    else if (p == &box2 )
    {
        cout << "p is pointing to box2" << endl;
    }
    else
    {
        // won't see this though
        cout << "p is pointing to another box " << endl;
    }

    if (gptr == &box1)
    {
        cout << "gptr is pointing to box1 " << endl;
    }
    else if (gptr == &box2)
    {
        cout << "gptr is pointing to box2 " << endl;
    }
    else 
    {
        // won't see this though
        cout << "gptr is pointing to another box" << endl;
    }

    cout << "box1 contains the value: " << box1 << endl;
    cout << "box2 contains the value: " << box2 << endl;

}

void passByPtr( int *ptr )
{
    *ptr = 3;
    ptr = gptr;

    *ptr = 4;
    cout << "____passByPtr has been called______" << endl;
}

void passByPtrRef( int* & ptrRef)
{
    *ptrRef = 5;
    ptrRef = gptr;
    *ptrRef = 6;
    cout << "_______passByPtrRef has been called____" << endl;
}
```

**Output:**

```cpp
_________ Current Conditions _______
_______passByPtrRef has been called____
p is pointing to box2
gptr is pointing to box2 
box1 contains the value: 5
box2 contains the value: 6
```