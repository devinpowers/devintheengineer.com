---
layout: archive
permalink: /C++/c++_constructors
title: " Constructors in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---


### Converting Constructor



**Example One**

![inserting an Image](/images/C++/constructors/Page1.jpg)

**nba.h** File:

```cpp
#ifndef NBA_H
#define NBA_H

#include<string>
using std::string;

struct NBA{

  string first_name = "First_Name";        
  string last_name = "Last_Name";
  int number = 0;

  NBA();
  NBA(string, string, int);


  void add_minutes(int);
};

string nba_to_string(const NBA &);

#endif
```


**nba.cpp** File

```cpp
#include<string>
using std::string;
#include<sstream>
using std::ostringstream; using std::istringstream;

#include "nba.h"

//Defaul constructor
NBA::NBA(){
  first_name = "first_name";
  last_name = "last_name";
  number = 0;
}

// Constructor of 3 Arguments

NBA::NBA(string first, string last, int num){

  first_name = first;
  last_name = last;
  number = num;

}

// add to minutes, correct hours if overflow
void NBA::add_minutes(int min){
  auto temp = number + min;
  if (temp >=60){
    number = temp % 60;
  }
  else
    number = temp;
}

// convert clock to string
string nba_to_string(const NBA &p){
  ostringstream oss;
  oss << "First Name:"<<p.first_name<<", Last Name:"
      <<p.last_name<<", Number:"<<p.number;
  return oss.str();
}

```

**main.cpp** File

```cpp
#include<iostream>
using std::cout; using std::endl;
#include<string>
using std::string;

#include "nba.h"

int main(){
    NBA player1; // Default constructor
    NBA player2("Steph", "Curry", 35); 

    
    cout << nba_to_string(player1)<<endl;
    cout << nba_to_string(player2)<<endl;
    
    player1.first_name = "Chris";
    player1.last_name = "Paul";
    player1.add_minutes(10);
    cout << nba_to_string(player1) << endl;

}
```

**Output**

    First Name:first_name, Last Name:last_name, Number:0
    First Name:Steph, Last Name:Curry, Number:35
    First Name:Chris, Last Name:Paul, Number:10



**Example 2**


![inserting an Image](/images/C++/constructors/Page2.jpg)
![inserting an Image](/images/C++/constructors/Page3.jpg)


**nba.h** File

```cpp
#ifndef NBA_H
#define NBA_H

#include<string>
using std::string;
#include<vector>
using std::vector;

struct NBA{

  string first_name = "First_Name";         // Default
  string last_name = "Last_Name";
  int number = 0;

  
  NBA()=default;
  NBA(string first, string last, int num) : first_name(first), last_name(last), number(num) {};

  NBA(string s);
  // explicit NBA(string s);  // no implicit conversion
  
  void add_minutes(int);
};

string nba_to_string(const NBA &);
void split(const string &, vector<string> &, char);

#endif
```

**nba.cpp** File

```cpp
#include<string>
using std::string;
#include<sstream>
using std::ostringstream; using std::istringstream;

#include "nba.h"

// string constructor
NBA::NBA(string s){
  // format is first_name:last_name:number
  vector<string> fields;
  split(s, fields, ':');
  first_name = fields[0];
  last_name = fields[1];
  number = stol(fields[2]);
}

// add to minutes, correct hours if overflow
void NBA::add_minutes(int min){
  auto temp = number + min;
  if (temp >=60){
    number = temp % 60;
  }
  else
    number = temp;
}

// convert clock to string
string nba_to_string(const NBA &p){
  ostringstream oss;
  oss << "First Name:"<<p.first_name<<", Last Name:"
      <<p.last_name<<", Number:"<<p.number;
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

**main.cpp** File

```cpp
#include<iostream>
using std::cout; using std::endl;
#include<string>
using std::string;

#include "nba.h"

int main(){
    NBA player1; // Default constructor
    NBA player2("Steph", "Curry", 35); // 3 arg constructor
    NBA player3("Lebron:James:23"); // string constructor
 
    
    cout << nba_to_string(player1)<<endl;
    cout << nba_to_string(player2)<<endl;
    cout << nba_to_string(player3)<<endl;
    
    player1.first_name = "Chris";
    player1.last_name = "Paul";
    player1.add_minutes(10);
    cout << nba_to_string(player1) << endl;

 

    string s="Devin:Powers:3";
    
    // implicit conversion
    cout << nba_to_string(s) << endl;
    // implicit conversion
    cout << nba_to_string(string("Tony:Parker:9"))<< endl; 
    // cannot, 2 conversions!
    // cout << nba_to_string("paul:pierce:34")); 
    cout << endl;
}
```

**Output**

    First Name:First_Name, Last Name:Last_Name, Number:0
    First Name:Steph, Last Name:Curry, Number:35
    First Name:Lebron, Last Name:James, Number:23
    First Name:Chris, Last Name:Paul, Number:10
    First Name:Devin, Last Name:Powers, Number:3
    First Name:Tony, Last Name:Parker, Number:9


