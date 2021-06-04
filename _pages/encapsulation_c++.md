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
    * So that it's a user-oriented way to access the functionality represented by our class
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
    * *Class designer*: Full access to everything
    * *Class user*: Only gets to use the interface the design provides


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
    Clock()=default;  // constructors
    Clock(int m, int h, string s) : minutes(m), hours(h), period(s) {}; // constructors
    Clock(string s);      // constructors
    void add_numbers(int);  // Method

  ```

Above, in the code (header) the user has access to the *public* and the designer has access to the *private* stuff!


**Whats the difference between a struc and a class?**

* With a struc, if you don't say otherwise, everything is assumed to be *public*, while class is the opposite and everything is assumed to be *private*!


### Const Member Functions

We have problems with our old code, since our attributes (minutes and hours) in our clock class is **private** now, we won't (as the user) be able to change them. The second problem is that our method calls (to print our clock to a string) won't work either, because it also cannot access private data members!


Lets address the 1st problem, in which the user can no longer access the private members of a class (including hours, minutes, and period)

How do we fix this issue?? 

**Accessor** - Member function used to retrieve the data of protected members.

**Mutators** - Member function used to edit the data of protected members.


**Note:** Accessor and Mutators are also known as **getters** and **setters**

* Which are used to *protect* your data, particulary when creating classes


**Note:** In C++ you cannot have a accessor method (getter) to have the same name as a data members, most people change the data members to have an "_" underscore at the back. (see example below)
Example:

nba.h (header file)

```cpp
#ifndef NBA_H
#define NBA_H

#include<string>
using std::string;
#include<vector>
using std::vector;

class NBA{

    private:
        string first_name_;  
        string last_name_;
        int number_ = 0;
        void adjust_nba(string, string, int);

    
    public:
    // constructors

        NBA() = default;
        NBA(string, string, int);
        explicit NBA(string s);

        // Getters
        string first_name() const { return first_name_;}
        string last_name() const {return last_name_;}
        int number() const { return number_;}

        // Setters
        void first_name(string);
        void last_name(string);
        void number(int);

        // Members
        void add_minutes(int);
        friend string nba_to_string(const NBA &);
        
};

string nba_to_string(const NBA &);
void split(const string &, vector<string> &, char);

#endif

```


**const at the end of a member function**

```cpp
int number() const { return number_;}
```

* This *const* means that the *this* pointer is a pointer to a constant thing
* You cannot change any aspect (any member) of what *this* points to in this method



## Friend Functions

* What is a friend function?
  * A friend function is a regular funciton that still has access to *private* member stuff

* You must declare the function as a friend in the class header
