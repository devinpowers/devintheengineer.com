---
layout: archive
permalink: /C++/operators_c++
title: "Operators in C++"
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

6 Types of Operators in C++

1. Arithmetic Operators
2. Assignment Operators
3. Relational Operators
4. Logical Operators
5. Bitwise Operators
6. Other Operators



Arithmetic Operator

basic adding, subtracting, multiplication, etc

example:

    #include <iostream>

    using namespace std;

    int main() {
        int d, b;

        d = 10;
        b = 2;

        cout << "d + b = " << (d + b) << endl;
        return 0;
    }


#### Increment and Decrement Operators

++ and -- increase and decreases the value by 1 


    #include <iostream>

    using namespace std;

    int main() {
        int a = 10;
        int b = 10;

        a++;
        b--;

        cout << "a incremented by 1: " << a << endl;
        cout << "b decremented by 1: " << b << endl;

        return 0;
    }


##### Assignment Operators



##### Relational Operators

==
!=


