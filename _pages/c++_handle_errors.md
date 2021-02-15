---
layout: archive
permalink: /C++/c++_handle_errors
title: "Handling Errors in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---
```cpp
#include<iostream>
using std::cout; using std::cin; using std::endl;

int main() {

    // handle errors

    double num1 = 0, num2 = 0;

    cout << "Enter Number 1: ";
    cin >> num1;

    cout << "Enter Number 2: ";
    cin >> num2;

    try{

        if(num2 == 0){
            throw "Divison by zero is not possible";
        }
        else{
            cout << "yes it will work" << endl;
            cout << "answer is: " << num1 / num2 << endl;       
        }
    }
    catch(const char exp)
    {
        cout << "Error: " << exp << "\n";
    }
}
```

![inserting an Image](/images/C++/errors/Page3.jpg)
![inserting an Image](/images/C++/errors/Page4.jpg)
![inserting an Image](/images/C++/errors/Page5.jpg)
![inserting an Image](/images/C++/errors/Page6.jpg)
![inserting an Image](/images/C++/errors/Page7.jpg)
![inserting an Image](/images/C++/errors/Page8.jpg)




more code

```cpp
#include<iostream>
using std::cout; using std::cin; using std::endl; using std::exception;


int main() {

    try {

        int age = 15;
        if (age >= 18) {
            cout << "Access granted - you're old enough! " << endl;
        }
        else{

            throw (age);
        }

    }
    catch (int myNum)
    {
        cout << "Access Denied, you must be at least 18 years old " << endl;

        cout << "your age is: " << myNum << endl;
    }


}
```

Handling Multiple "Catches

```cpp
#include<string>
using std::string;

#include<iostream>
using std::cout; using std::cin; using std::endl; using std::exception;


int main() {

    try {

        string name;

        name = "Devin";

        int age = 18;
    
        if (age >= 18) {
            cout << "Access granted - you're old enough! " << endl;
        }
        else{

            throw (age);
        }

        if (name == "Austin")
        {
            cout << "Hi Austin!!" << endl;
        }
        else{

            throw (name); // should send it to the correct catch 
        }


    }
    catch (int myNum)
    {
        cout << "Access Denied, you must be at least 18 years old " << endl;

        cout << "your age is: " << myNum << endl;
    }

    catch (string name_wrong)

    {
        cout << "The name is wrong! " << endl;
    }


}
```


![inserting an Image](/images/C++/errors/Page1.jpg)
![inserting an Image](/images/C++/errors/Page2.jpg)