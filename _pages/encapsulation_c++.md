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

* Note: on a method call, C++ will automatically bind a variable named *this* to the calling object (refer to the **add_minutes** method)
* *this* is a **POINTER!**


#### Protection

* We can save users from making mistakes, aka changing a value thats wrong by providing protection!

**How??**

We can divide into **two parts**:
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


Lets address the 1st problem, in which the user *can no longer access the private members of a class* (including hours, minutes, and period) (Changing the Attributes!)

How do we fix this issue?? 

**Accessor** - Member function used to retrieve the data of protected members.      (Getters)

**Mutators** - Member function used to edit the data of protected members.          (Setters)


**Note:** Accessor and Mutators are also known as **getters** and **setters**

* Which are used to *protect* your data, particulary when creating classes


**Note:** In C++ you cannot have a accessor method (getter) to have the *same name* as a data members, most people change the data members to have an "**_**" underscore at the back. (see example below)
Example:

nba.h (header file)

```cpp
#ifndef CLOCK_H
#define CLOCK_H

#include<string>
using std::string;
#include<vector>
using std::vector;

class Clock{
 private: 

  int minutes_ = 0;
  int hours_ = 0;
  string period_;
  // function member adjusts the clock for us
  void adjust_clock(int, int, string);

 public:
  // constructors
  Clock()=default;
  Clock(int, int, string);
  explicit Clock(string s);


  // getters (grab our attributes)
  int hours() const {return hours_;}
  int minutes() const {return minutes_;}
  string period() const {return period_;}      // Notice the underscores( _ )
  
  // setters
  void hours(int);
  void minutes(int);
  void period(string);
  
  // members
  void add_minutes(int);

  // friend function
  friend string clk_to_string(const Clock &);
};

string clk_to_string(const Clock &);
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

* You must declare the function as a friend in the class header, the class gives friendship to the function 

Example of the *friend* function defined:

```cpp
 // friend function
  friend string clk_to_string(const Clock &);

```

## "this" keyword

* Is only accessible to use through a member function and the function that belongs to a class which means it belongs to a class, so a method. Inside a method we can reference this and what this is a pointer to the current object instance that the method belongs to.

* pointer to a method 

Example


### Extra on Setters

* Setters allow you the opportunity to do more *sanity* checking:
  * Hour < 12 or minutes < 60 or "AM" or "PM"

For example below:

```cpp
Void Clock::adjust_clock(int mins, int hrs, string prd){

  minutes_ = minutes_+ mins;
  int hrs_remainder = minutes_ / 60;
  minutes_ %= 80;

  hours_ = hours_ + hrs + hrs_remainder;
  hours_ %= 12;

  if (prd != "AM" && prd != "PM")
    period_ = "AM";
  
  else
    period_ = prd;
}

```


After  we *set* we need to call the adjust_clock member function

How do we do this?

```cpp
this->adjust_clock()
(*this).adjust_clock()
adjust_clock() // easiest way!
```

## Full Clock Example Below:


**header file**

```cpp
#ifndef CLOCK_H
#define CLOCK_H

#include<string>
using std::string;
#include<vector>
using std::vector;

class Clock{
 private: 
  int minutes_ = 0;
  int hours_ = 0;
  string period_;
  // function member adjusts the clock for us
  void adjust_clock(int, int, string);

 public:
  // constructors
  Clock()=default; // Default constructor
  Clock(int, int, string);
  explicit Clock(string s);       // if we pass in one big long string


  // getters (grab our attributes)
  int hours() const {return hours_;}
  int minutes() const {return minutes_;}
  string period() const {return period_;}
  
  // setters
  void hours(int);
  void minutes(int);
  void period(string);
  
  // members
  void add_minutes(int);

  // friend function
  friend string clk_to_string(const Clock &);
};

string clk_to_string(const Clock &);
void split(const string &, vector<string> &, char);

#endif


```

**functions file**

```cpp
#include<string>
using std::string;
#include<sstream>
using std::ostringstream; using std::istringstream;
#include <iostream>
using std::endl; using std::cout;

#include "17.2-clock.h"

// adjust clock values to be "reasonable"
void Clock::adjust_clock(int mins, int hrs, string prd){
  cout << "Running This function " << endl;
  int hrs_remainder;
  minutes_ = minutes_ + mins;
  hrs_remainder = minutes_ / 60;
  minutes_ %= 60;

  hours_ = hours_ + hrs + hrs_remainder;
  hours_ %= 12;
  if (prd!="AM" && prd!="PM")
    period_ = "AM";
  else
    period_ = prd;
}

Clock::Clock(int mins, int hrs, string prd){
  minutes_= 0;
  hours_= 0;
  period_= "";
  adjust_clock(mins,hrs,prd);
  //this->adjust_clock(mins,hrs,prd);
  //(*this).adjust_clock;
}

Clock::Clock(string s){
  // format is hr:min:period_
  minutes_=0;
  hours_=0;
  period_="";
  vector<string> fields;
  split(s, fields, ':');
  auto hrs = stol(fields[0]);
  auto mins = stol(fields[1]);
  auto prd = fields[2];
  adjust_clock(mins,hrs,prd);
  //this->adjust_clock(mins,hrs,prd);
}

// setters
void Clock::hours(int val){
  adjust_clock(0, val, period_);
  //this->adjust_clock(0, val, period_);
}

void Clock::minutes(int val){
  adjust_clock(val, 0, period_);  
  // this->adjust_clock(val, 0, period_);
    
}

void Clock::period(string s){
  adjust_clock(0, 0, s);  
  // this->adjust_clock(0, 0, s);
}

// add to minutes, correct hours if overflow
void Clock::add_minutes(int min){
  adjust_clock(min, 0, period_);  
  // this->adjust_clock(min, 0, period_);
}

// convert clock to string
// declared a friend in header
string clk_to_string(const Clock &c){
  ostringstream oss;
  oss << "Hours:"<<c.hours_<<", Minutes:"
      <<c.minutes_<<", Period:"<<c.period_;
  return oss.str();
}

// split string based on sep, ref return of vector<string>
void split(const string &s, vector<string> &elems, char sep) {
    istringstream iss(s);
    string item;
    while(getline(iss, item, sep))
      elems.push_back(item);
}

```

**main.cpp file**

```cpp
#include<iostream>
using std::cout; using std::endl;
#include<string>
using std::string;

#include "17.2-clock.h"

int main(){
    Clock a_clk(121,24,"today");       
    cout << "3 param check:"<<clk_to_string(a_clk) << endl;
    
    Clock some_clk("24:121:today"); 
    cout << "string param check:"<<clk_to_string(some_clk) << endl;

    Clock test_clk(30,6,"PM");
    cout << clk_to_string(test_clk) << endl;
    test_clk.hours(24);
    cout << "Hours test:"<< clk_to_string(test_clk) << endl;

    test_clk.minutes(120);
    cout << "Mins test:"<< clk_to_string(test_clk) << endl;

    test_clk.period("today");
    cout << "Period test:"<<clk_to_string(test_clk) << endl;

    test_clk.add_minutes(40);

    cout << "Add test:"<<clk_to_string(test_clk) << endl;
    cout << " Shit" << endl;

    // More Testing

    Clock another_one;
    another_one.hours(23);
    another_one.minutes(34);
    another_one.period("PM");
    cout << "Testing: Another One::: " << clk_to_string(another_one) << endl;
    cout << "Lets see if the Getters work: " << another_one.hours() << endl;
}

```

**Output**

  Add test:Hours:9, Minutes:10, Period:AM
  Shit
  Running This function 
  Running This function 
  Running This function 
  Testing: Another One::: Hours:11, Minutes:34, Period:PM
  Lets see if the Getters work: 11



### Overloaded Operators

 * When you define a class, you can also define **overloaded operators**



    <iframe width="560" height="315"
src="https://www.youtube.com/watch?v=mS9755gF66w" 
frameborder="0" 
allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
allowfullscreen></iframe>