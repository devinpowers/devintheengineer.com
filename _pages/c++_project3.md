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


Will have more functions here:


