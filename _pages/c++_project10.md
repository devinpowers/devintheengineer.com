---
layout: archive
permalink: /C++/c++_project10
title: "Project 10 in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---


**Header File (bistack.h)**

* includes both the declaration and defintion of the BiStack Class


```cpp
#ifndef BISTACK_H
#define BISTACK_H

#include<iostream>
using std::ostream;
using std::cout; using std::endl;
#include<string>
using std::string; using std::to_string;
#include<iterator>
using std::ostream_iterator;
#include<sstream>
using std::ostringstream;
#include<algorithm>
using std::copy;
using std::swap;
#include<initializer_list>
using std::initializer_list;

// Declarations
template<typename ElementType>
class BiStack;

template<typename ElementType>
ostream& operator<<(ostream& out, const BiStack<ElementType> &s);


// Definitions
template<typename ElementType>
class BiStack{
    // Attributes
    private:
        ElementType *ary_ = nullptr;   // the array of type ElementType (templated)
        int size_ = 4; // Size of Array
        int max_size_ = 16;
        int top1_ = -1;
        int top2_ = size_;
        void grow_and_copy();

    public:

    // Constructors
    BiStack() = default;
    BiStack( size_t initial_size, size_t max_size = 16);
    BiStack(initializer_list<ElementType>, size_t max_size = 16);

    // Copy Constructor
    BiStack(const BiStack &s);
    // Deconstructor
    ~BiStack();
    // Overloaded =
    BiStack& operator=(BiStack);

    // Methods

    ElementType top1();
    ElementType top2();

    const size_t size();
    const size_t max();
    const size_t capacity();

    void pop1();
    void pop2();
    
    void push1(ElementType);
    void push2(ElementType);

    bool empty1();
    bool empty2();

    friend ostream& operator<< <ElementType>(ostream&, const BiStack&);
};

template<typename ElementType>
BiStack<ElementType>::BiStack(size_t initial_size, size_t max_size)
{
    // Size constructor that initializes the variables
    size_ = initial_size;
    max_size_ = max_size;
    ary_ = new ElementType[size_]; // Creates new dynamically allocated array of size
    top1_ = -1;
    top2_ = size_;
  
}

template<typename ElementType>
BiStack<ElementType>::BiStack(initializer_list<ElementType> list_, size_t max_size)
{
    // List Constructor Example -> {3,4,5,6,1,2,3,4}
    size_ = list_size();
    max_size_ =max_size;
    top1_ = -1;
    top2_ = size_;
    // Create new Array to hold our list items
    ary_ = new ElementType[size_]{};
    size_ index = 0;

    for (auto e : list_)
    {
        ary_[index++] = e;
    }
    // Update the top of Stack 1
    top1_ = index =1;
}

// The Copy Constructor

template<typename ElementType>
BiStack<ElementType>::BiStack(const BiStack<ElementType> &s)
{
    cout << "Using the Copy Constructor " << endl;
    size_ = s.size_;
    max_size_ = s.max_size_;

    top1_ = s.top1_;
    top2_ = s.top2_;

    ary_ = new ElementType[s.size_];
    copy(s.ary_, s.ary_+s.size_, ary_); // Copy Elements from array to new construtor
}





#endif

```

**Main File to Run (main.cpp)**


```cpp
#include<iostream>
using std::cout; using std::cin; using std::endl;
using std::boolalpha;
#include<stdexcept>
using std::overflow_error; using std::underflow_error;


#include "class-10.h"

int main (){
  int test_no;
  cin >> test_no;
  cout << boolalpha;

  switch(test_no){

  case 1: {
    BiStack<long> b;
    cout << b.capacity() << endl;
    cout << b.size() << endl;
    cout << b.max() << endl;
    break;
  }

  case 2:{
    BiStack<long> b{1,2,3,4,5,6};
    cout << b.capacity() << endl;
    cout << b.size() << endl;
    cout << b.max() << endl;
    break;
  }

  case 3:{
    BiStack<long> b{1,2,3,4,5,6};
    cout << b << endl;
    break;
  }

  case 4:{
    BiStack<long> b{1,2,3,4,5,6};
    cout << b.empty1() << endl;
    cout << b.empty2() << endl;
    break;
  }
    
  case 5:{
    BiStack<long> b{1,2,3,4,5,6};
    b.push2(200);
    b.push1(100);
    cout << b << endl;
    break;
  }

  case 6:{
    BiStack<long> b{1,2,3,4,5,6};
    b.push2(200);
    b.push1(100);
    cout << b.top1() << endl;
    cout << b.top2() << endl;
    break;
  }

  case 7:{
    BiStack<long> b{1,2,3,4,5,6};
    try{
      cout << b.top1() << endl;
      cout << b.top2() << endl; // should throw
    }
    catch (underflow_error &e){
      cout << e.what() << endl;
    }
    break;
  }

  case 8:{
    BiStack<long> b{1,2,3,4,5,6};
    try{
      b.pop1();
      cout << b << endl;
      b.pop2(); // should throw
    }
     catch (underflow_error &e){
      cout << e.what() << endl;
    }
    break;
  }

  case 9:{
    BiStack<long> b1{1,2,3,4,5,6};
    BiStack<long> b2(b1);
    b1.push1(100);
    b2.push2(200);
    cout << b1 << endl;
    cout << b2 << endl;
    break;
  }

  case 10:{
    BiStack<long> b1{1,2,3,4,5,6};
    BiStack<long> b2;
    b2 = b1;
    b1.push1(100);
    b2.push2(200);
    cout << b1 << endl;
    cout << b2 << endl;
    break;
  }

  case 11:{
    BiStack<char> b(4);
    b.push1('a');
    b.push1('b');
    b.push2('y');
    b.push2('z');    
    cout << b << endl;
    for (int i=0; i< 5; ++i)
      b.push1(static_cast<char>('h'+i));
    cout << b << endl;
    break;
  }

  case 12:{
    BiStack<char> b(4,8);
    b.push1('a');
    b.push1('b');
    b.push2('y');
    b.push2('z');    
    cout << b << endl;

    // loop should exceed max and throw
    try{
      for (int i=0; i< 5; ++i)
	b.push1(static_cast<char>('h'+i));
      cout << b << endl;
    }
    catch(overflow_error &e){
      cout << e.what() << endl;
    }
    break;
  }
  }
}
      
```
