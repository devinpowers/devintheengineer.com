---
layout: archive
permalink: /C++/c++_data_structures/queue
title: "Queue Data Structure in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

What is a Queue?

* it's a *linear data structure* that serves as a container of objects that are inserted and removed according to the First-In, First-Out principle (FIFO)


* A Queue has 3 main operations: enqueue, dequeue, and peek!


**Queue Example using an Array Data Structure:**

* Enqueue: Inserts a new element at the rear of the queue
* Dequeue: Remove front element of the queue
* Peek: Returns the front element present in the queue without removing it
* IsEmpty: Checks if the queue is empty
* IsFull: Checks if the queue is full
* Size: Returns the total number of elements present in the queue


**Header File**

```cpp

#ifndef QUEUE_H
#define QUEUE_H

#include<iostream>
using std::cout;
using std::endl;
 
// Define the default capacity of a queue
#define SIZE 10
 
// A class to store a queue
class queue
{
    int *arr;       // array to store queue elements
    int capacity;   // maximum capacity of the queue
    int front;      // front points to the front element in the queue (if any)
    int rear;       // rear points to the last element in the queue
    int count;      // current size of the queue
     
public:
    queue(int size = SIZE);     // constructor
    ~queue();                   // destructor
 
    void dequeue();
    void enqueue(int x);
    int peek();
    int size();
    bool isEmpty();
    bool isFull();
};

#endif

```


**Function File**

```cpp

#include<iostream>
using std::cout;
using std::endl;
 
#include "q.h"
 
// Constructor to initialize a queue
queue::queue(int size)
{
    arr = new int[size];
    capacity = size;
    front = 0;
    rear = -1;
    count = 0;
}
 
// Destructor to free memory allocated to the queue
queue::~queue() {
    delete[] arr;
}
 
// Utility function to dequeue the front element
void queue::dequeue()
{
    // check for queue underflow
    if (isEmpty())
    {
        cout << "Underflow\nProgram Terminated\n";
        exit(EXIT_FAILURE);
    }
 
    cout << "Removing " << arr[front] << endl;
 
    front = (front + 1) % capacity;
    count--;
}
 
// Utility function to add an item to the queue
void queue::enqueue(int item)
{
    // check for queue overflow
    if (isFull())
    {
        cout << "Overflow\nProgram Terminated\n";
        exit(EXIT_FAILURE);
    }
 
    cout << "Inserting " << item << endl;
 
    rear = (rear + 1) % capacity;
    arr[rear] = item;
    count++;
}
 
// Utility function to return the front element of the queue
int queue::peek()
{
    if (isEmpty())
    {
        cout << "Underflow\nProgram Terminated\n";
        exit(EXIT_FAILURE);
    }
    return arr[front];
}
 
// Utility function to return the size of the queue
int queue::size() {
    return count;
}
 
// Utility function to check if the queue is empty or not
bool queue::isEmpty() {
    return (size() == 0);
}
 
// Utility function to check if the queue is full or not
bool queue::isFull() {
    return (size() == capacity);
}
```


**Main File**

```cpp

#include<iostream>
using std::cout;
using std::endl;

#include "q.h"

int main()
{
    // create a queue of capacity 5
    queue q(5);
 
    q.enqueue(1);
    q.enqueue(2);
    q.enqueue(3);
 
    cout << "The front element is " << q.peek() << endl;
    q.dequeue();
 
    q.enqueue(4);
 
    cout << "The queue size is " << q.size() << endl;
 
    q.dequeue();
    q.dequeue();
    q.dequeue();
 
    if (q.isEmpty()) {
        cout << "The queue is empty\n";
    }
    else {
        cout << "The queue is not empty\n";
    }
 
    return 0;
}
```