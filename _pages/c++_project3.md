---
layout: archive
permalink: /C++/c++_project3
title: "Project 3 in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

Project 3 in C++

!!!

Progress so Far:



  #include<iostream>

  using std::cout; using std::cin; using std::endl; using std::boolalpha;



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



  int main ()
  {
      long input;

      cout << "Please Enter a Number to check the Sum of Divisors: ";

      cin >> input;

      cout << "The sum of divisor of " << input << " is: " << divisor_sum(input) << endl;


      return 0;
  }

