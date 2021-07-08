---
##layout: archive
permalink: /C++/c++_week13
title: "C++ More on Classes"
author_profile: true

header:
  image: "/images/C++/C++_home.jpeg"

toc: true
toc_label: "Table of Contents" 
---

If we can use STL containers (Vectors, Maps, etc )/ algorithms to solve any problem do them. Containers *handle* their own memory

But, let's go through some class design where we have to do the *memory management* on a container ourself

# Rule of Three

* the **Rule of Three** is used for any object that **dynamically allocates memory**. Will need

  * Copy Constructor 
  * Assignment Operator (Overloaded)
  * Destructor


* **Rule:** If you need one, then you need all three!!!!

### Copy Constructor in C++

* Is a member function that *initializes* an object using another object of the same class.

General Syntax for the Header File:
    * Part of the construction of the Class

```cpp
ClassName(const ClassName &old_object);
```

General Syntax for the Function 

```cpp
ClassName::ClassName(const ClassName &old_object )
{
    // Body of the Constructor
}
```

### Destructors in C++

* A Destructor is an instance member function which is invoked automatically whenever an object is going to destroy

Basis Syntax:

```cpp
~constructor-name();
```

**Properties**

Destructor function is automatically invoked when the objects are destroyed.



**When do you destructor called?**

A destructor function is called automatically when the object goes out of scope: 
(1) the function ends 
(2) the program ends 
(3) a block containing local variables ends 
(4) a delete operator is called  











**Example of Rule of Three**

**Header File**
```cpp

#ifndef GCHARACTER_H_
#define GCHARACTER_H_

#include <iostream>
#include <string>

class GCharacter
{
    public:

        static const int DEFAULT_CAPACITY = 5;

        // Constructor
        GCharacter(std::string name = "John", int capacity = DEFAULT_CAPACITY );

        // Copy Constructor
        GCharacter(const GCharacter& source);

        // Overloaded Assignment 
        GCharacter& operator = (const GCharacter& source);

        // Destructor (easy to write)
        ~GCharacter();

        // Insert (member function) a new tool into the tool array (holder)
        void insert(const std::string& toolName);
    
    private:
        // Data Members
        std::string name;
        int capacity;
        int used;
        std::string* toolHolder;

    // Overloading the << operator (syntax)
    friend std::ostream& operator <<(std::ostream& os, const GCharacter& gc);

};


#endif
```

**Functions File**

```cpp
#include<iostream>
using std::cout; using std::endl; 
#include<string>
using std::string;
#include<algorithm>
using std::copy;

#include "GCharacter.h"


// Constructor

GCharacter::GCharacter(string n, int cap)
{
    name = n;
    capacity = cap;
    used = 0;
    toolHolder = new string[cap];
}

// Copy Constructor

GCharacter::GCharacter(const GCharacter& source)
{
    cout << "Copy Constructor Called. " << endl;

    this->name  = source.name;
    this->capacity = source.capacity;
    used = source.used;
    toolHolder = new string[source.capacity]; // In order to do a  Deep Copy, we need to create a brand new string array

    copy(source.toolHolder, source.toolHolder + used, this->toolHolder );
}

// Overloaded Assignment Operator

GCharacter& GCharacter::operator=(const GCharacter& source)
{
    // Testing for self-assignment
    cout << "Overloaded Assignment Called. " << endl;
    
    // Check for self assignment
    // gc1 = gc1;
    if (this == &source)
    {
        return *this; // return GCharacter Object
    }
    this->name  = source.name;
    this->capacity = source.capacity;
    used = source.used;

    copy(source.toolHolder, source.toolHolder + used, this->toolHolder );

    return *this; // return GCharacter Object
}


// Destructor

GCharacter::~GCharacter()
{
    // only handling the dynamic memory
    cout << "Destructor called for " << this->name << " at this memory location " << this << endl;

    delete[] toolHolder; 
}

// Inserting a new tool into our toolHolder

void GCharacter::insert(const string& toolName)
{
    if (used == capacity) 
    {
        cout << "Tool Holder is full. Cannot add any additional tools " << endl;
    }
    else
    {
        toolHolder[used] = toolName;
        used++; //increment
    }

}

std::ostream& operator<<(std::ostream& os, const GCharacter& gc)
{
    os << "Game Character " << gc.name << " has the following tools: " << std::endl; 
    
    // iterate over our tool array

    for(int i = 0; i < gc.used; i++)
    {
        os << gc.toolHolder[i] + " | ";
    }

    return os << std::endl;
}
```


**Main file**

```cpp
#include <iostream>
using std::cout;
using std::endl;

#include "GCharacter.h"


GCharacter exCopyConstructor(GCharacter tempGC)
{
    cout << "Copy Constructor called twice." << endl;
    cout << "Once for the formal parameter being passed by value" << endl;
    cout << "Once for the return value." << endl; 

    return tempGC;
}


int main()
{
    GCharacter gc1;

    gc1.insert("Potion");
    gc1.insert("Crossbow");
    gc1.insert("Gun");
    gc1.insert("Ray Gun");
    gc1.insert("Cloak");
    gc1.insert("Sword"); // won't get added in since we have a tool array of 5 by default

    cout << endl;
    cout << gc1 << endl;
    cout << endl;

    GCharacter gc2("Devin", 5); // 5 size for the tool array


    gc2.insert("Axe");

    exCopyConstructor(gc2);

    
    // Copy Constructor 
    GCharacter gc3 = gc2; // gc3 wasn't in exisitence

    // Over loaded Assignment Operator
    gc2 = gc1;

    // overloaded insertion operator
    cout << "_____________________ " << endl;
    cout << "gc2: " << gc2 << endl;
    cout << "gc1: " << gc1 << endl;
    cout << "gc3: " << gc3 << endl;

}
```

**Output**

```cpp
Tool Holder is full. Cannot add any additional tools 

Game Character John has the following tools: 
Potion | Crossbow | Gun | Ray Gun | Cloak | 


Copy Constructor Called. 
Copy Constructor called twice.
Once for the formal parameter being passed by value
Once for the return value.
Copy Constructor Called. 
Destructor called for Devin at this memory location 0x7ffeef08f490
Destructor called for Devin at this memory location 0x7ffeef08f468
Copy Constructor Called. 
Overloaded Assignment Called. 
_____________________ 
gc2: Game Character John has the following tools: 
Potion | Crossbow | Gun | Ray Gun | Cloak | 

gc1: Game Character John has the following tools: 
Potion | Crossbow | Gun | Ray Gun | Cloak | 

gc3: Game Character Devin has the following tools: 
Axe | 

Destructor called for Devin at this memory location 0x7ffeef08f440
Destructor called for John at this memory location 0x7ffeef08f4e8
Destructor called for John at this memory location 0x7ffeef08f5c8
```



## Composite Class

* A composite class, is a class that is build by using the operations of other classes in the implementation (think of using a stack in a Graph)


**Example with a custom Stack Data Structure**




## Bad Dynamic Memory Class

## Fixing the Dynamic Memory

## Copy and Swap Idiom

## Templates and Classes

## Templated Friends

