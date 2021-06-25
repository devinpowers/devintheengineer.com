---
layout: archive
permalink: /C++/c++_this
title: "C++ this Pointer"
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

Every object in C++ has access to its own address through an **important pointer** called **this** pointer. The this pointer is an implicit parameter to *all member functions*. Therefore, inside a member function, this may be used to refer to the invoking object.

* think of how python calls self in its *classes*


To understand how "this" pointer works it's important to know how objects (classes) look at functions and data members of a class

1. Each object gets its own copy of the data member
2. All-access the same function definition as present in the code segment

Which means that each object gets its own copy of data members and all objects **share** a single copy of member function

Then now question is that if only one copy of each member function exists and is used by multiple objects, how are the proper data members are accessed and updated?

The compiler supplies an implicit pointer along with the names of the functions as ‘this’.
The ‘this’ pointer is *passed as a hidden argument* to all nonstatic member function calls and is available as a local variable within the body of all nonstatic functions.


## Static

https://www.youtube.com/watch?v=V-BFlMrBtqQ


## Example of this

Use either this-> or (*this), look at the example problem below!

```cpp
#include <iostream>
 
using namespace std;

class Box {
   public:
      // Constructor definition
      Box(double l = 2.0, double b = 2.0, double h = 2.0) {
         cout <<"Constructor called." << endl;
         length = l;
         breadth = b;
         height = h;
      }
      double Volume() {
         return length * breadth * height;
      }
      int compare(Box box) {
         return (*this).Volume() > box.Volume();  // or return this->Volume() > box.Volume();
      }
      
   private:
      double length;     // Length of a box
      double breadth;    // Breadth of a box
      double height;     // Height of a box
};

int main(void) {
   Box Box1(3.3, 1.2, 1.5);    // Declare box1
   Box Box2(8.5, 6.0, 2.0);    // Declare box2

   if(Box1.compare(Box2)) {
      cout << "Box2 is smaller than Box1" <<endl;
   } else {
      cout << "Box2 is equal to or larger than Box1" <<endl;
   }
   
   return 0;
}
```

**Output:**

```cpp
Constructor called.
Constructor called.
Box2 is equal to or larger than Box1
```
