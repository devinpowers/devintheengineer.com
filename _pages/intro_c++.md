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


#### Literals

Data used for representing “fixed”  values that can be used directly in the code we write

###### Integers


    #include <iostream>

    int main() {

    int practice = 0213;

    std::cout << practice << std::endl;

    return 0;
    }


Will return the value 139


###### Floating Points


    #include <iostream>

    int main() {

    double floating_point = -0.45E-5;

    std::cout << floating_point << std::endl;

    return 0;
    }

Will return -4.5e-06




###### Characters

single quotation marks



    #include <iostream>

    int main() {

    char char_example = 'W';

    std::cout << char_example << std::endl;

    return 0;
    }



###### Escape Sequences

Special meaning in C++, you can make a new line by using \n for a tab


###### String Literals






 







### Constants

Variables that cannot be changed 


    #include <iostream>


    int main() {

    const int light_speed = 299792458;

    light_speed = 2400;

    std::cout << light_speed << std::endl;

    return 0;
    }

## Data Types:

