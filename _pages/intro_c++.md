---
layout: archive
permalink: /C++/intro_c++
title: "Intro to C++ Concepts"
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

Variables
data types
basic input and output

type conversion

operators



Working with Variables in C++

    #include <iostream>

    int main()

    {
        int points = 5;

        std::cout << "I scored " << points << "points" << std::endl;

        return 0;
    }

Here the points value is return as 5.

You can change the value of the varible points

    #include <iostream>

    int main()

    {
        int points = 5;

        points = 10;

        std::cout << "I scored " << points << " points" << std::endl;

        return 0;
    }

Here the points value is returned as 10.


Literals

-	Data used for representing “fixed”  values that can be used directly in the code we write

1. Integers

2. Floating Points

3. Characters

4. Escape Sequences

5. String Literals






 







Constants

-	Variables that cannot be changed 


    #include <iostream>


    int main() {

    const int light_speed = 299792458;

    light_speed = 2400;

    std::cout << light_speed << std::endl;

    return 0;
    }

Data Types:

