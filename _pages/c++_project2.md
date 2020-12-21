---
layout: archive
permalink: /C++/c++_project2
title: "Project 2 in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

Code for Project 2:

I should insert my notes to solve this problem here


    #include <iostream>

    using namespace std;


    int main()

    {
        //here some of our input values
        int input_number;

        int k_factor; 

        int sum = 0;

        cout <<  "Enter a number: ";

        cin >> input_number;

        cout << "Please enter a k value to check: ";

        cin >> k_factor;


        if (input_number < 6)
        {
        cout << "the Factor K is 0" << endl;
        }

        // otherwise we proceed

        for (int i = 2; i < input_number; i++ )
        {
        if (input_number % i== 0)
        {
            cout << "the Number " << i << " is Divisible in " << input_number  << endl;
            sum += i;
        }; 
        }

        for ( int b = 0; b <= k_factor; b++ )
        {
            if (((sum*b) + 1 ) == input_number )
            {
                cout << " The K factor for " << input_number << " is " << b << endl;
                break;

            }
        }

        return 0;


    }