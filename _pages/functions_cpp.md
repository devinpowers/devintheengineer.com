---
layout: archive
permalink: /C++/functions_cpp
title: "Working with Functions in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---


FUNCTIONS IN C++

### Built-In Functions (Standard Library Functions)

Here's an example of using the built in math function to calculate the 'pow' x raised to power (x^p)

```cpp
#include <cmath>

using std::cout;
using std::endl;

int main()
{
    cout << pow(10,2)<< endl;
}
```


### User-Defined Functions

Calling a function is similar to Python with the ';'

Making our own functions!



Calling a Function example

```cpp
#include <iostream>

using std::cout;


void greet(){

    cout << "Hi my name is Devin!";
}
int main()

{
    greet();
}
```

### Function Parameters

A function can be declared with parameters (arguments), a parameter is a value that is passed when declaring a function.

example:

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



### Void Functions and Return Statements

function that doesnt return any value 

example: Multiply two numbers


```cpp
#include <iostream>
#include <string>

using namespace std;

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


## Function Prototype



Why use user-defined functions?

- reusable code
- divide tasks
- readabilty


