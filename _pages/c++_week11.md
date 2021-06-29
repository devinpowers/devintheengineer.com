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


* Whenever the **const** keyword is attached with any method(), variable, pointer variable, and with the object of a class it prevents that specific object/method()/variable to modify its data items value.

**Theres different ways to use the const keyword**


**One Way: Can't change a const variable** (EASY)

**Example of const variable:**

```cpp
#include<iostream>
#include <string>

using std::cout;
using std::endl;

int main() {

    const int max_age = 90;

    // max_age = 23;  // Can't change a const variable (won't compile here)

    cout << max_age << endl;
}
```
**Output:**

```cpp
90
```



### What about with Pointers?

* Pointers can be declared with a **const** keyword

* There are *3 possible ways* to use **const** keyword with a pointer

**When the Pointer variable point to const value**

**Basic Syntax:**

```cpp
const data_type* variable_name;
```

Lets implement the above concept:

```cpp
#include<iostream>
using std::cout;
using std::endl;

int main()
{
    int x = 10;
    char y = 'D';
 
    int* i = &x;
    const char* j = &y;

    cout << "*i = " << *i << " " << "*j = " << *j << endl; 
 
    
    x = 9;
    y = 'A';

    cout << "x = " << x << " " << "y = " << y << endl;

    cout << "*i = " << *i << " " << "*j = " << *j << endl; 

    *i = 6; // can change since it's not const
    // *j = 7; won't compile
 
    cout << "*i = " << *i << " " << "*j = " << *j << endl; 
}
```

**Output:**

```cpp
*i = 10 *j = D
x = 9 y = A
*i = 9 *j = A
*i = 6 *j = A
```

* The values of x and y can be altered since they're not **const** variables above

* The value j is pointing to *const-char* type value while the value i is pointing to a non-const int for demo

* i and j are two pointer variables that are **pointing to a memory location**  int-type and **const** char-type, but the value stored at these corresponding locations can be changed as we have done above. (by changing the variables x and y)

* Otherwise we would get an error if we try to modify the *const* variable for const j


**When the const pointer variable point to the value**

**Syntax:**

```cpp
data_type* const variable_name;
```

Lets demonstrate the concept

```cpp
#include<iostream>
using std::cout;
using std::endl;

int main()
{
    int x = 5;
    int z = 6;
 
    char y = 'A';
    char p = 'C';
 
    int* const i = &x;     // const pointer(i) pointing to variable x's location
    char* const j = &y;     // const pointer(j) pointing to variable y's location

    int* q = &z; // pointer (q) pointing to variable z's location

    // print to see before changing
    cout << "*i = " << *i << " and " << "*j = " << *j << endl;


    // The values that is stored at the memory location can modified
    // even if we modify it through the pointer itself
    // No compile time error!
    *i = 10;
    *j = 'F';
    *q = 69;
 
    // CTE because pointer variable is const type so the address
    // pointed by the pointer variables
    // can't be changed
    // *i = &z;
    // *j = &p;

    cout << "j address: " << j << endl;
    
    cout << "*i = " << *i << " and " << "*j = " << *j << endl;

    cout << "Address of i: " << "i = " <<  i << " and " <<  "Address of j: " << j << endl;
}
```

**Output:**

```cpp
*i = 5 and *j = A
j address: FE
*i = 10 and *j = F
Address of i: i = 0x7ffee1f8e5ec and Address of j: FE
```

* The values that are stored in the pointer variables i and j are modifiable, but the locations that they're pointed to by the *const-pointer* variable where the corresponding value of x and y are stored aren't modifiable


**When const pointer pointing to a const variable**

**Syntax:**

```cpp
const data_type* const variable_name;
```

```cpp
#include<iostream>
using std::cout;
using std::endl;

int main()
{
    int x = 9;
    
    // const pointer pointing to a const variable (double trouble!)
    const int* const i = &x;

    // *i=10;  
    // The above statement will give CTE
    // Once Ptr(*i) value is
    // assigned, later it can't
    // be modified(Error)
    
    char y = 'A'; 
    const char* const j = &y;
   
    // *j='B';
    // The above statement will give CTE
    // Once Ptr(*j) value is
    // assigned, later it can't
    // be modified(Error)
 
    cout << *i << " and " << *j << endl;
    cout << i << " and " << j << endl;
}
```

**Output:**

```cpp
9 and A
0x7ffee388b5ec and A쵈��
```

* With a const pointer pointing to a const variable you can *neither* allowed to change the const pointer nor the value stored at the location pointed by that pointer






# Const with Class and Methods

When you declare a member function as **const**, like:

```cpp
int GetValue() const;
```

Then you're telling the compiler that it will not modify anything in the object, this also means you can call the member function on a constant objects like this object

```cpp
const Object obj1;
```
* this is a const object, meaning that you cannot change anything on this object, and this object can only call *const* member functions like the one above.








* Harder stuff


```cpp

#include<iostream>
using std::cout;
using std::endl;

class Entity
{
    private:
        int m_X, m_Y;
        int var;
    public:
        int GetX() const // promises not to touch anything in the function
        {   // m_x = 100; <- can't change or compile error will occur! Can't modify the class with a const
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
    
    Entity e;    // create object
    e.SetX(23);   // Set variable x to 23
    PrintEntity(e); // print 
}

```

**Output:**

```cpp
23
```


**Mutable Keyword**


* However, there is a *mutable keyword* that does allow to change variables even with the *const* member function, see example below:

```cpp

#include<iostream>

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


## Const member functions in C++ Extra Stuff

https://www.geeksforgeeks.org/const-member-functions-c/

* The objects of a class can be declared as **const**, and object declared as const *cannot* be modified and hence can invoke only const memeber functions ensure not to modify the object.

* A const object can be created by prefixing the const keyword to the object declaration

* Any attempt to change the data member of const objects results in a compile-time error. 


**Basic Syntax:**

```cpp
const Class_Name Object_name; 
```

* The idea of const functions is not to allow them to modify the object on which they are called

**Example:**

```cpp

#include <iostream>

using std::cout;
using std::endl;


class Test {
    int value;
 
public:
    Test(int v = 0) {
       value = v;
     }
 
    int getValue() const {
    
    // Can't change -> value
     return value;
      }
};
 
int main()
{
    Test t(20);
    cout << t.getValue() << endl;

}
```

**Output**

```cpp
20
```


When you declare an object *const*, the **only** functions that can be called on the object are functions are *const*. 

```cpp
#include <iostream>
using std::cout;
using std::endl;

class Test {
    int value;
 
public:
    Test(int v = 1) {
       value = v;
     }
 
    int getValue() const  {
      
      return value;
      }

};
 
int main()
{
    const Test t;

    cout << t.getValue() << endl;
}
```

**Output**

```cpp
1
```


**Another Example** of const member functions 

```cpp
#include<iostream>
using std::cout;
using std::endl;
class Demo
{   private:
    int value;

    public:
    Demo(int v = 0) {value = v;}

    void showMessage()
    {
        cout<<"Hello World, this showMessage ran" <<endl;
    }
    void display()const
    {
        cout<<"Hello world, this display() Function ran "<<endl;
    }
};
int main()
{
   //Constant object are initialised at the time of declaration using constructor
    const Demo d1;
    // d1.showMessage();  Error occurred if uncomment.
    d1.display();
    Demo d2;
    d2.showMessage(); // Will Run
    d2.display();  // Will RUn
    
}
```

**Output**

```cpp
Hello world, this display() Function ran 
Hello World, this showMessage ran
Hello world, this display() Function ran 
```

* You can see above that the *const* object (d1) would only run with *const* member functions will the non-const object (d2) ran *both* member functions

