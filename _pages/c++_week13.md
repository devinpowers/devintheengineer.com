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


### Example with a Custom Stack Data Structure**

**Header File (stack.h)**

```cpp
#ifndef STACK_H
#define STACK_H

using std::ostream;
#include<iostream>
using std::string;
#include<string>
#include<vector>
using std::vector;
#include<initializer_list>
using std::initializer_list;

class Stack{
 private:
  vector<char> vec_;
  
 public:
  Stack()=default;
  // Stack(size_t sz)
  Stack(initializer_list<char> c) : vec_(c) {};
  
  char top();
  void pop();
  void push(char);
  bool empty();
  // bool full();  // not a problem with vectors
  void clear();
  
  friend ostream& operator<<(ostream& out, const Stack &s);
};

ostream& operator<<(ostream& out, const Stack &s);

#endif
```

**Stack Functions File (functions.cpp)**

* Includes basic methods of stacks including top, pop, push, empty, and clear

```cpp
#include<algorithm>
using std::copy;
#include<iterator>
using std::ostream_iterator;
#include<stdexcept>
using std::underflow_error;

#include "stack.h"

char Stack::top(){
  if (vec_.size() == 0)
    throw underflow_error("top, empty stack");
  return vec_.back();
}

void Stack::pop(){
  if (vec_.size() == 0)
    throw underflow_error("pop, empty stack");
  vec_.pop_back();
}

void Stack::push(char s){
    vec_.push_back(s);
}

bool Stack::empty(){
    return vec_.empty();
}

void Stack::clear(){
  vec_.clear();
}

ostream& operator<<(ostream &out, const Stack &s){
    // Print the stack
    out << "(bottom) ";
    copy(s.vec_.begin(), s.vec_.end(), ostream_iterator<char>(out, ","));
    out << " (top)";
    return out;
}
```

**Main Function to Run (main.cpp)**

```cpp
#include<iostream>
using std::cout; using std::endl; using std::cin;
#include<string>
using std::string;
#include<stdexcept>
using std::underflow_error;

#include "stack.h"

int main()

{
    // Practice with Basic Stack

    Stack stk = {'a','b','c','d','e'};

    cout << stk << endl;

    // Basic Stack Methods/Functions

    cout << "Top of the Stack: " << stk.top() << endl;

    stk.pop(); // Removes top value from the Stack

    stk.push('Z'); // Pushes another value onto the Stack

    cout << stk << endl;

    while (! stk.empty())
    {
        stk.pop();

    }

    cout << "After popping everything off the stack " << endl;
    cout << stk << endl;

    stk.push('D');
    stk.push('E');
    stk.push('V');
    stk.push('I');
    stk.push('N');
    
    cout << "After pushing items onto the stack: " << endl;

    cout << stk << endl;

    // Clear the stack

    stk.clear();

    cout << stk << endl;


    // Reverse a String

    string user_string = "", reverse_string = "";

    cout << "Input a string to reverse: ";
    getline(cin, user_string); // get line and put it into user_string

    Stack stk2;

    for (auto ch : user_string)
    {
        stk2.push(ch);
    } 

    cout << stk2 << endl;

    while (!stk2.empty())
    {
        stk2.pop();
    }


    cout << "Original String was: " << user_string << endl;
    cout << "Reversed String was: " << reverse_string << endl;


}
```

**Output:**

```cpp
(bottom) a,b,c,d,e, (top)
Top of the Stack: e
(bottom) a,b,c,d,Z, (top)
After popping everything off the stack 
(bottom)  (top)
After pushing items onto the stack: 
(bottom) D,E,V,I,N, (top)
(bottom)  (top)
Input a string to reverse: Devin Powers
(bottom) D,e,v,i,n, ,P,o,w,e,r,s, (top)
Original String was: Devin Powers
Reversed String was: 
```



## Bad Dynamic Memory Class



## Fixing the Dynamic Memory

**Header File (stack.h)**
```cpp

#ifndef STACK_H
#define STACK_H

#include<iostream>
using std::ostream;
#include<initializer_list>
using std::initializer_list;

class Stack{
private:
    // Attributes
    char *ary_ = nullptr;  // This will be an array (The keyword nullptr denotes the pointer literal)
    int sz_ = 0;            // Size of the Array
    int top_ = -1; 

public:
    // General Constructors to Initialize the Stack
    Stack()=default; // Default constructor, when you create an object!
    
    Stack(size_t sz); // Takes in the "Size" of the String which will be converted into an Array -> string.size()
    Stack(initializer_list<char>); // Takes in {'A','B','C'} and Creates/Initializes the stack
    
    Stack(const Stack &);   // copy Constructor
    ~Stack();               // destructor (easy)
    Stack& operator=(const Stack &); // Overloaded =
    
    // Memebers/Operations on Stack
    char top();
    void pop();
    void push(char);
    bool empty();
    bool full();
    void clear();

    // Operator Overloader
    friend ostream& operator<< (ostream&, const Stack &);
};

ostream& operator<< (ostream&, const Stack&);
#endif
```

**Functions File (stack.cpp)**

```cpp
#include<string>
using std::string;
#include<iterator>
using std::ostream_iterator;
#include<algorithm>
using std::copy;
#include<initializer_list>
using std::initializer_list;
#include<stdexcept>
using std::overflow_error; using std::underflow_error;
#include<iostream>
using std::cout; using std::endl;


#include "stack.h"

// Copy Constructor
Stack::Stack(const Stack &s){
  //
    cout << "Using the Copy Constructor  " << endl;
    sz_ = s.sz_;
    top_ = s.top_;
    ary_= new char[s.sz_];
    // ary_ = s.ary_   BAD IDEA, just copies the pointers!!!
    copy(s.ary_, s.ary_+s.sz_, ary_);
}

// Delete Memory
Stack::~Stack(){
    cout << "Deleting Memory " << endl;
    delete [] ary_;
}

// classic, but there's a better way!!! ( = ) Overloaded Operator
Stack& Stack::operator=(const Stack &s){

  cout << "Using the Equal to (=) Operator " << endl;

    if (this != &s){  // this and s are not the same pointer!
	delete [] ary_;
	sz_ = s.sz_;
	top_ = s.top_;
	// is constructor call needed??
	ary_= new char[s.sz_];
	copy(s.ary_, s.ary_+s.sz_, ary_);
    }
    return *this;
}

// Pass Stack as a size
Stack::Stack(size_t sz){
  cout << "Using the size_t dataype constructor " << endl;
  sz_ = sz;
  ary_ = new char[sz];
  top_ = -1;
}

// Pass Stack as a list of char
Stack::Stack(initializer_list<char> c){
  // I think this badboy just takes a list into the constructor and automatically adds them to the array
  cout << "Using the initializer_list Constructor " << endl;
  sz_ = c.size();
  ary_ = new char[sz_];
  size_t indx = 0;
  top_ = sz_ - 1;
      
  for (auto e : c)
    ary_[indx++] = e;
}

// Methods to Perform on the Stack Object

char Stack::top(){
  if (top_ < 0)
    throw underflow_error("top, empty stack");
  return ary_[top_];
}

void Stack::pop(){
  if (top_ < 0)
    throw underflow_error("pop, empty stack");
  --top_;
}

void Stack::push(char element){
  // cout << "sz:"<<sz_<<" top:"<<top_<<" e:"<<element<<" sub:"<< top_ + (sz_ - 1) << endl;
  if (top_ >= (sz_ - 1) )
    throw overflow_error("push, full stack");
  ary_[++top_] = element;
}

bool Stack::empty(){
  return top_ < 0;
}
  
bool Stack::full(){
  return top_ >= ( sz_ - 1);
}

void Stack::clear(){
  top_ = -1;
}

// Print out the Stack Object

ostream& operator<<(ostream &out, const Stack &s){
    out << "(bottom) ";
    copy(s.ary_, s.ary_ + s.top_+1,
	 ostream_iterator<char>(out, ","));
    out << " (top)";
    return out;
}
```


**Main File (main.cpp)**


```cpp

```


## Copy and Swap Idiom

## Templates and Classes

## Templated Friends

