---
layout: archive
permalink: /C++/functions_cpp
title: "Working with Functions in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

What is a function ? 

 - its the encapsulation of some calculation

 - We invoke a function and provide informatino in the form of arguments

 - The function receives the arguments as "parameters", and uses the parameters to make its calculation!

 - A value is returned by the function to the Caller!


 Functions are very useful to break down programs into smaller and more understable pieces

 - Functions should have one purpose and only one purpose ( a function abstracts one idea)
 - Should be generic, resuable, and readable



### Built-In Functions (Standard Library Functions)

Here's an example of using the built-in math function to calculate the 'pow' x raised to power (x^p)

```cpp
#include <cmath>
#include <iostream>
using std::cout;
using std::endl;

int main()
{
    cout << pow(10,2)<< endl;
}
```

Output:
```cpp
100
```

### User-Defined Functions

Calling a function is similar to Python with the ';'

Making our own functions! Void doesnt return anything, it used when were calling a function to print something! Here is an example:

```cpp
#include <iostream>

using std::cout;
using std::endl;

void greet(){

    cout << "Hi my name is Devin!" << endl;
}
int main()

{
    greet();
}
```
Output:

```cpp
Hi my name is Devin!
```


### Function Parameters

A function can be declared with parameters (arguments), a parameter is a value that is passed when declaring a function.

Example:

```cpp
#include <iostream>
#include <string>

using namespace std;

void print_name(string name)
{
    cout << name << endl;
}

int main()
{
    string name = "Devin";

    string name2 = "Paul";

    string name3 = "Jordan";

    print_name(name);

    print_name(name2);

    print_name(name3);

}
```
Output:

```cpp
Devin
Paul
Jordan
```


### Void Functions and Return Statements

Function that doesnt return any value is a void function, which is used to print!

example: Multiply two numbers


```cpp


#include <iostream>
#include <string>

#include<cmath>

using std::cout;
using std::endl;

int multiply(int a, int b)
{
    return (a * b);
}

int main()
{
  int sum;

  sum = multiply(100, 5);

  cout << "100 * 5 = " << sum << endl;

  return 0;

}
```

Output:

```cpp
100 * 5 = 500
```


## Scope

