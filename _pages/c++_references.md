---
layout: archive
permalink: /C++/c++_references
title: "References in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

![inserting an Image](/images/C++/references/Page1.jpg)
![inserting an Image](/images/C++/references/Page2.jpg)
![inserting an Image](/images/C++/references/Page3.jpg)



    #include<iostream>
    using std::cout; using std::endl;


    void swap ( int &x, int & y){

    int temp = x;
    x = y;
    y = temp;

    }
    int main(){

    int x = 0;
    int y = 10;
    cout << "Before Swap: " << "X: " << x << " Y: " << y <<endl;
    swap (x,y);

    cout << "After Swap: " << "X: " << x << " Y: " << y <<endl;

    }

Output

    Before Swap: X: 0 Y: 10
    After Swap: X: 10 Y: 0



![inserting an Image](/images/C++/references/Page4.jpg)
![inserting an Image](/images/C++/references/Page5.jpg)


We can use the & Operator to find the address of the reference

    #include<iostream>
    using std::cout; using std::endl;


    int main(){

    int a = 10;
    int &b = a;

    int c = 100;
    b = c;

    cout << " Value of a: " << a << endl
        << " Value of b: " << b << endl
        << " Value of c: " << c << endl;


    cout << "Location of a: " << &a <<endl;
    cout << "Location of b: " << &b << endl;
    cout << "Location of c: " << &c << endl;
    }


Output

    Value of a: 100
    Value of b: 100
    Value of c: 100
    Location of a: 0x7ffee076272c
    Location of b: 0x7ffee076272c
    Location of c: 0x7ffee076271c

