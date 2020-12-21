---
layout: archive
permalink: /C++/c++_project1
title: "Project 1 in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---


Code:

    #include <iostream>
    #include <cmath>
    #include <iomanip>

    using std::endl; using std::cin; using std::cout;


    using namespace std;

    int main()
    {
        long year; // input value from user
        double user_slope; // input value from user

        // Given Constants
        double slope = 0.01173;  
        double intercept = 34.3491;

        cout << "";
        cin >> year;

        cout << "";
        cin >> user_slope;

        double temp = slope * year + intercept;

        cout << fixed << setprecision(2) << temp << endl;
        // 

        // Year 2 and 3 Temp
        long year2 = round(((temp + 7) - intercept)/slope);

        cout << "Year 2: " << year2 << endl;

        long year3 = round(((temp + 7) - intercept)/user_slope);

        cout << "Year 3: " << year3 << endl;
        

    }