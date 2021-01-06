---
layout: archive
permalink: /C++/c++_handle_errors
title: "Handling Errors in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

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