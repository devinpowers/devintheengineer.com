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
        void grow_and_copy(); // Private Method to double our array if needed!

    public:

    // Constructors
    BiStack() = default; // Default
    BiStack( size_t initial_size, size_t max_size = 16);   // size_t will be a int like -> BiStack(4) 
    BiStack(initializer_list<ElementType>, size_t max_size = 16); // initializer_list will be a literal list like -> BiStack stack1 = {2,5,4,3,2,4,9}

    // Copy Constructor
    BiStack(const BiStack &s);
    // Deconstructor
    ~BiStack();
    // Overloaded = Operator
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

    bool empty1(); // Checks if Stack 1 is Empty
    bool empty2(); // Checks if Stack 2 is Empty

    friend ostream& operator<< <ElementType>(ostream&, const BiStack&); // Returns stream aka prints out!!
};

template<typename ElementType>
BiStack<ElementType>::BiStack(size_t initial_size, size_t max_size)
{
    // Size constructor that initializes the variables
    // BiStack stack2(8); <- Example using this constructor
    size_ = initial_size; // Which would be size 8 in our example
    max_size_ = max_size; // 16
    ary_ = new ElementType[size_]; // Creates new dynamically allocated array of size
    top1_ = -1; // Indexing 
    top2_ = size_; // Indexing 
} 

// List Constructor
template<typename ElementType>
BiStack<ElementType>::BiStack(initializer_list<ElementType> list_, size_t max_size)
{
    // List Constructor Example -> {3,4,5,6,1,2,3,4}
    size_ = list_.size(); // Size of the initializer_list that we past in
    max_size_ = max_size; // which will be 16
    top1_ = -1; // Indexes
    top2_ = size_; // Indexes
    // Create new Array to hold our list items
    ary_ = new ElementType[size_]{};
    size_t index = 0;

    // Copy list elements into the array
    for (auto e : list_)
    {
        ary_[index++] = e;
    }
    // Update the top of Stack 1
    top1_ = index - 1;
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


// Assignment Operator
template<typename ElementType>
BiStack<ElementType>& BiStack<ElementType>::operator=(BiStack<ElementType> stack)
{
    swap(this->size_, stack.size_);
    swap(this->max_size_, stack.max_size_);
    
    swap(this->top1_, stack.top1_);
    swap(this->top2_, stack.top2_);
    
    swap(this->ary_, stack.ary_);
    
    return *this;
}


// Destructor

template <typename ElementType>
BiStack<ElementType>::~BiStack(){
    //Destructor
    delete [] ary_;
}

// Copy and Grow
template <typename ElementType>
void BiStack<ElementType>::grow_and_copy()
{
    ElementType *new_array;

    if (size_ == 0)
    {
        new_array = new ElementType[1]{};
        size_ =1;
        ary_ = new_array;
    }

    else
    {
        // We double the array in size without growing it past the max size
        if (size_*2 <= max_size_ )
        {
            // We create a new Array
            new_array = new ElementType[size_ * 2]{}; // New array constructor
            int new_array_size = size_*2;

            // Copy Elements from old array into the new array (tricky)
            copy(ary_, ary_ + top1_+1, new_array); // Front part of array

            int number_of_elements = size_ - top2_;
            for (int i = i; i <= number_of_elements; i++)
            {
                // insert elements in back of the array
                new_array[new_array_size - i] = ary_[size_ -i];
            }
            // Now we have to update Size and Tops in our New Array
            int difference = size_ - top2_;
            size_ *= 2;
            top2_ = size_ - difference;

            // Swap Arrays
            std::swap(new_array, ary_);
            // Prevent Memory Leake
            delete [] new_array;
        }
        // Else the array is already too big and we have to throw an error
        else
        {
            throw std::overflow_error("Stack is already past it's max!");
        }
    }

}

// OK now I have to just do push1 and push2 methods


template <typename ElementType>
void BiStack<ElementType>::push1(ElementType element)
{
    // If array is full, we can call the copy_and_grow method to try and grow the array
    if (top1_ == top2_ - 1)
    {
        grow_and_copy();
        ary_[++top1_] = element;
    }
    // Otherwise it's not full and we can add an element to the front
    else
    {
        ary_[++top1_] = element;
    }

}


template <typename ElementType>
void BiStack<ElementType>::push2(ElementType element)
{
    // If array is full, we can call the copy_and_grow method to try and grow the array
    if (top2_ == (top1_ + 1))
    {
        grow_and_copy();
        // ADDD??
    }
    // Otherwise it's not full and we can add an element to the front
    else
    {
        ary_[--top2_] = element;
    }
    
}



template <typename ElementType>
ElementType BiStack<ElementType>::top1()
{    // Similar to the Stack used in Week Examples

    if (top1_ < 0)
    {
        throw underflow_error("Top1, empty stack");
    }
    // Otherwise return the top element of top2()
    return ary_[top1_];
}


template <typename ElementType>
ElementType BiStack<ElementType>::top2()
{   
    if (top2_ == size_ )
    {
        throw underflow_error("Top2, empty stack");
    }
    // Otherwise return the top element of top2()
    return ary_[top2_];
}


template <typename ElementType>
size_t const BiStack<ElementType>::max()
{
    // Return a max size
    return max_size_;
}


template <typename ElementType>
size_t const BiStack<ElementType>::size()
{
    // Return the number of elements in stacks
    return top1_ +1 + (size_ - top2_);

}


template <typename ElementType>
size_t const BiStack<ElementType>::capacity()
{
    // Return the current size
    return size_;
}


template <typename ElementType>
void BiStack<ElementType>::pop1()
{   // "Pop" element from stack1
    if (top1_ < 0)
    {
        throw underflow_error("pop, empty stack");
    }
    // Update top index to remove element
    --top1_;

}

template <typename ElementType>
void BiStack<ElementType>::pop2()
{
    if (top2_ == size_)
    {
        throw underflow_error("pop, empty stack 2 ");
    }
    // Update top2 index to remove element
    ++top2_;
}

template <typename ElementType>
bool BiStack<ElementType>::empty1()
{
    // Checks if there are elements in stack 1
    return top1_ == -1;
}

template <typename ElementType>
bool BiStack<ElementType>::empty2()
{
    // Checks if there are elements in stack 2
    return top2_ == size_;
}

// Print out our BiStack

template <typename ElementType>
ostream& operator<<(ostream &out, const BiStack<ElementType> &stack)
{
    ostringstream oss;
    string outstring;

    // Lets print out the first stack1
    if (stack.top1_ != -1)
    {
        out << "Top1 index: " << stack.top1_ << endl;
    }
    else{
        out << "Top1 is Empty " << endl;
    }

    if (stack.top2_ != stack.size_)
    {
        out << "Top2 Index: " << stack.top2_ << endl;
    }
    else{
        // Else it's empty
        out << "Top2 is Empty" << endl;
    }

    // Let's print out the Size and Capacity of the BiStack
    out << "Size: " << stack.top1_+1 + (stack.size_ - stack.top2_) << endl;
    // Print out Capacity of the BiStack
    out << "Capacity of BiStack: " << stack.size_ << endl;

    // Let's now print the Array

    copy(stack.ary_, (stack.ary_ + stack.size_), ostream_iterator<ElementType>(oss, ","));

    outstring = oss.str(); // Convert oss to string
    outstring = outstring.substr(0, outstring.size() - 1);
    out << outstring;

    return out;

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


**Sample Output**

If you ran Number 9

```cpp
Using the Copy Constructor 
Top1 index: 6
Top2 is Empty
Size: 7
Capacity of BiStack: 12
1,2,3,4,5,6,100,0,0,0,0,0
Top1 index: 5
Top2 is Empty
Size: 6
Capacity of BiStack: 12
1,2,3,4,5,6,0,0,0,0,0,0
```

If you ran Number 5

```cpp
Top1 index: 6
Top2 is Empty
Size: 7
Capacity of BiStack: 12
1,2,3,4,5,6,100,0,0,0,0,0
```