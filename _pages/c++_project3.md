---
layout: archive
permalink: /C++/c++_project3
title: "Project 3 in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

included in the header

    #include<iostream>

    using std::cout; using std::cin; using std::endl;


Greatest Common Divisor Function

    long gcd ( long number_1, long number_2)
    {
        // Greatest common divisor of two integers  function
        while (number_1 != number_2)
        {
            if (number_1 > number_2)
            {
                number_1 = number_1 - number_2;
            }
            else
            {
                number_2 = number_2 - number_1;
            }
            
        }
        return number_1;

    }

Least Common Divisor Function 

    long lcd ( long number_1, long number_2)
    {
        // least common multiple of two integers function
        long lcm_number;

        lcm_number = (number_1 * number_2)/(gcd(number_1, number_2));

        return lcm_number;
    }


Divisor Sum Function

    long divisor_sum (long number)
    {
        int sum = 0;

        for (int i = 1; i < number; i++ )
        {
            if (number % i == 0)
            {
                sum += i;

            }
        }
        sum += number;
        return sum;

    }

Is the integer a Solitary number function 


    bool is_solitary (long number)
    {
        // Checks if the gcd sum is equal to one, returns either True (1) or False(0)
        // Hence the return value is bool (boolean)
        long gcd_number_sum;

        gcd_number_sum = gcd(divisor_sum(number), number);

        return(gcd_number_sum == 1);


    }


Full Program Code here



    #include<iostream>

    using std::cout; using std::cin; using std::endl; using std::boolalpha;


    long gcd ( long number_1, long number_2)
    {
        // Greatest common divisor of two integers  function
        while (number_1 != number_2)
        {
            if (number_1 > number_2)
            {
                number_1 = number_1 - number_2;
            }
            else
            {
                number_2 = number_2 - number_1;
            }
            
        }
        return number_1;

    }


    long lcd ( long number_1, long number_2)
    {
        // least common multiple of two integers function
        long lcm_number;

        lcm_number = (number_1 * number_2)/(gcd(number_1, number_2));

        return lcm_number;
    }


    long divisor_sum (long number)
    {
        int sum = 0;

        for (int i = 1; i < number; i++ )
        {
            if (number % i == 0)
            {
                sum += i;

            }
        }
        sum += number;
        return sum;

    }

    bool is_solitary (long number)
    {
        // Checks if the gcd sum is equal to one, returns either True (1) or False(0)
        // Hence the return value is bool (boolean)
        long gcd_number_sum;

        gcd_number_sum = gcd(divisor_sum(number), number);

        return(gcd_number_sum == 1);


    }



    int main ()
    {
        int test_switch;

        cout << "Please Enter (1,2,3, or 4)" << endl;
        cout << "1. Find the GCD of two numbers"  << endl << "2. Find the LCD of two numbers"  << endl << "3. Find Divisor Sum" << endl << "4. Check if Number is Solitary" << endl;     

        cin >> test_switch;

        switch (test_switch){
        case 1: // gcd function
        {
            long number_1, number_2;
            cout << "Please Enter the first number: " <<endl;

            cin >> number_1;

            cout << "Please enter the second number: " << endl;
            cin >> number_2;

            cout << "The greatest Common Divisor between " << number_1 << " and " << number_2 << " is: "<< gcd(number_1, number_2) << endl;

            break;
        
        }
        case 2: // LCD
        {
            long number_1, number_2;
            cout << "Please Enter the first number: " <<endl;
            cin >> number_1;
            cout << "Please enter the second number: " << endl;

            cin >> number_2;
            cout << "The Least Common Divisor between " << number_1 << " and " << number_2 << " is: "<< gcd(number_1, number_2) << endl;

            break;
        }
        case 3: // Divisor Sum
        {
            long number;

            cout << "Please enter a number to check its divisor sum: " << endl;

            cin >> number;

            cout << "The Divisor Sum of " << number << " is " << divisor_sum(number) << endl;
            break;

        }
        case 4: // is solitary
        {
            long number;

            cout << "Please enter a number to check if it is Solitary: " << endl;
            cin >> number;

            if (is_solitary(number) == 1)
            {
                cout << "The number is Solitary" << endl;
            }
            else
            {
                cout << "the number is not Solitary" <<endl;
            }

            break;
        }
        }

        
    }


