---
layout: archive
permalink: /C++/c++_stack
title: "C++ Stack Data Structure"
author_profile: true

header:
  image: "/images/tower3.jpeg"

toc: true
toc_label: "Table of Contents" 
---



- Insert Stack Data structure notes here


**Header File (stack.h)**

```cpp

#ifndef STACK_H
#define STACK_H

#include<iostream>
using std::cout; using std::endl; using std::cin;
#include<string>
using std::string;


class Stack {
    private:
    
        int top;
        int size_ = 10;
        int * a = new int[size_];
    
    public:
    
        Stack() { top = -1; }
        bool push(int x);
        int pop();
        int peek();
        bool isEmpty();
        void clear();
};

#endif
```


**Functions File (stack.cpp)**

```cpp
#include<iostream>
using std::cout; using std::endl; using std::cin;
#include<string>
using std::string;

#include "stack.h"

bool Stack::push(int x)
{
    if (top >= (size_ - 1)) {
        cout << "Stack Overflow";
        return false;
    }
    else {
        a[++top] = x;
        cout << x << " pushed into stack\n";
        return true;
    }
}
 
int Stack::pop()
{
    if (top < 0) {
        cout << "Stack Underflow";
        return 0;
    }
    else {
        int x = a[top--];
        return x;
    }
}
int Stack::peek()
{
    if (top < 0) {
        cout << "Stack is Empty";
        return 0;
    }
    else {
        int x = a[top];
        return x;
    }
}
 
bool Stack::isEmpty()
{
    return (top < 0);
}

void Stack::clear()
{
  // clear the stack
  top = -1; 
}
```

**Main File (main.cpp)**

```cpp
#include<iostream>
using std::cout; using std::endl; using std::cin;
#include<string>
using std::string;
 
#include "stack.h"

int main()
{
    class Stack s;
    s.push(10);
    s.push(20);
    s.push(30);
    s.push(50);
    s.push(90);
    cout << s.pop() << " Popped from stack\n" << endl;
    //print all elements in stack :
    cout<<"Elements present in stack : ";
    while(!s.isEmpty())
    {
        // print top element in stack
        cout<<s.peek()<<" ";
        // remove top element in stack
        s.pop();
    }
    cout << endl;

    // Let's clear the stack

    s.clear();


    s.push(69);
    s.push(100);
    s.push(78);

    cout<<"Elements present in stack : ";
    while(!s.isEmpty())
    {
        // print top element in stack
        cout<<s.peek()<<" ";
        // remove top element in stack
        s.pop();
    }
    cout << endl;

 
    return 0;
}
```


**Example Output:**

* After compiled

```cpp
10 pushed into stack
20 pushed into stack
30 pushed into stack
50 pushed into stack
90 pushed into stack
90 Popped from stack

Elements present in stack : 50 30 20 10 
69 pushed into stack
100 pushed into stack
78 pushed into stack
Elements present in stack : 78 100 69 
```

![inserting an Image](/images/C++/stack/stack1.jpg)
![inserting an Image](/images/C++/stack/stack2.jpg)
![inserting an Image](/images/C++/stack/stack3.jpg)
![inserting an Image](/images/C++/stack/stack4.jpg)
