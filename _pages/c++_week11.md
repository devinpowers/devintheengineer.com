---
layout: archive
permalink: /C++/c++_week11
title: "C++ Week 11 Stuff (extra)"
author_profile: true

header:
  image: "/images/tower3.jpeg"

toc: true
toc_label: "Table of Contents" 
---

## Const Keywork in C++

https://www.geeksforgeeks.org/const-keyword-in-cpp/

* Whenever the **const** keyword is attached with any method(), variable, pointer variable, and with the object of a class it prevents that specific object/method()/variable to modify its data items value.

* Can't change a *const* variable

**Basic C++ Program Example**

```cpp
#include<iostream>
#include <string>

using std::cout;
using std::endl;

int main() {

    const int max_age = 90;

    // max_age = 23;  // Can't change a const variable

    cout << max_age << endl;
}
```
**Output:**

```cpp
90
```




#### What about with Pointers?

* Pointers can be declared with a **const** keyword

* There are 3 possible ways to use **const** keyword with a pointer

### When the Pointer variable point to const value

**Basic Syntax:**

```cpp
const data_type* variable_name;
```

Lets implement the above concept:

```cpp
#include <iostream>
using std::cout;
using std::endl;
 
// Driver Code
int main()
{
    int x = 10;
    char y = 'D';
 
    const int* i = &x;
    const char* j = &y;
 
    
    x = 9;
    y = 'A';

    cout << x << " " << y << endl;

    // *i = 6;
    // *j = 7;
 
    cout << *i << " " << *j << endl;
}
```

**Output:**

```cpp
9 A
9 A
```

* The values of x and y can be altered since they're not **const** variables above

* The values of i and j are pointing to the const-int and const-char type value

* i and j are two pointer variables that are **pointing to a memory location** const int-type and char-type, but the value stored at these corresponding locations can be changed as we have done above. 

* Otherwise we would get an error if we try to modify the *const* variable

### When the const pointer variable point to the value

**Syntax:**

```cpp
data_type* const variable_name;
```

Lets demonstrate the concept

```cpp


```






### When const pointer pointing to a const variable


**Syntax:**

```cpp
const data_type* const variable_name;
```







### Const with Class and Methods


```cpp

#include<iostream>
#include <string>

using std::cout;
using std::endl;

class Entity
{
    private:
        int m_X, m_Y;
        int var;
    public:
        int GetX() const // promises not to touch anything in the function
        {
            return m_X;
        }
      
        void SetX(int x)
        {
            m_X = x;
        }
};

void PrintEntity(const Entity& e)
{
    cout << e.GetX() << endl;
}

int main(){
    
    Entity e;
    e.SetX(23);

    PrintEntity(e);

}

// Make sure to add const to method if it's not suppose to modify the class

```

**Output:**

```cpp
23
```


**Mutable Keyword**

```cpp

#include<iostream>
#include <string>

using std::cout;
using std::endl;

class Entity
{
    private:
        int m_X, m_Y;
        mutable int var;   // can modify 
    public:
        int GetX() const // promises not to touch anything in the function
        {
            var = 2;   // we can modify it 
            return m_X;
        }
        int GetX()
        {
            return m_X;
        }


        void SetX(int x)
        {
            m_X = x;
        }
};

void PrintEntity(const Entity& e)
{
    cout << e.GetX() << endl;
}

int main(){
    
    Entity e;

    e.SetX(23);

    PrintEntity(e);

}
```

**Output:**

```cpp
23
```
