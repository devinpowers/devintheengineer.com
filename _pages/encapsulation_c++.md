---
layout: archive
permalink: /C++/encapsulation_c++
title: "C++ Encapsulation"
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---


### Notes on Encapsulation


#### Abstraction

* We want to provide an **interface** to our class
    * So that it's a user-oriented wat to access the functionality represented by our class
    * The methods we define are that interface

Abstraction is *hiding* the details of how a struc/class is implemented


##### Special Variable

* C++ will mark/remembers the calling object in a method call.

Example:

```cpp
NBA my_player;
my_player.add_number(23);
```
In the example above the member function **add_number**, the variable *this* points to **my_player**

* Note: on a method call, C++ will automatically bind a variable named *this* to the calling object
* *this* is a **POINTER!**


#### Protection

* We can save users from making mistakes, aka changing a value thats wrong by providing protection

**How??**

We can divide into two parts:
    * Class designer: Full access to everything
    * Class user: Only gets to use the interface the design provides


#### Public vs Private

* As part of the class declaration we can declare parts of the class *public* or *private*
    * **public**: parts of the class that can be used by everyone
    * **private** parts of the class to be used by *other* members of the class


Example:

 * would be in the header file

```cpp
class Clock{

 private:
    // Class members that follow are private (notice the colon :)
    int minutes;
    int hours;
    string period;


 public:
    // Class memebers that follow are public (notice the colon :)
    Clock()=default; 
    Clock(int m, int h, string s) : minutes(m), hours(h), period(s) {};
    Clock(string s);
    void add_numbers(int);

  ```


**Whats the difference bewteen a struc and a class?**

* With a struc, if you don't say otherwise, everything is assumed to be public, while class is the opposite and everything is assumed to be private!



### Const Member Functions

