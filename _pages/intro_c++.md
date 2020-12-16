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

![inserting an Image](/images/C++/basics/Page1.jpg)
![inserting an Image](/images/C++/basics/Page2.jpg)
![inserting an Image](/images/C++/basics/Page3.jpg)
![inserting an Image](/images/C++/basics/Page4.jpg)


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

![inserting an Image](/images/C++/basics/Page5.jpg)
![inserting an Image](/images/C++/basics/Page6.jpg)

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
![inserting an Image](/images/C++/basics/Page7.jpg)



    #include <iostream>


    int main() {

    const int light_speed = 299792458;

    light_speed = 2400;

    std::cout << light_speed << std::endl;

    return 0;
    }

## Data Types:

![inserting an Image](/images/C++/basics/Page8.jpg)
![inserting an Image](/images/C++/basics/Page9.jpg)
![inserting an Image](/images/C++/basics/Page10.jpg)
![inserting an Image](/images/C++/basics/Page11.jpg)
![inserting an Image](/images/C++/basics/Page12.jpg)
![inserting an Image](/images/C++/basics/Page13.jpg)
#### Integars


#### Float

#### Double

Example of a integar, float, and a double in C++


    #include <iostream>

    int main() {


    int salary = 89000;

    float area = 78.9;
    double volume = 134.242;


    std::cout <<"Example of a integer: "<< salary << std::endl;
    std::cout << "an Example of a float and double: " << area << " and " << volume <<std::endl;
    return 0;
    }


### Char


    #include <iostream>

    int main() {


    char char_practice = 'h';

    std::cout <<"Example of a Char: "<< char_practice << std::endl;
    
    return 0;
    }

### Bool

True or False

    #include <iostream>

    int main() {


    bool cond = false;

    std::cout <<"the Bool is: "<< cond << std::endl;
    
    return 0;
    }

Note, it will return 1 for true and 0 for anything else (including false)


### Void

The void keyword will indicate an absence of data which means "no value"



### Modify Data Types

There are 4 Type Modifiers in C++

1. signed
2. unsigned
3. short
4. long

Then we can modify the above modifiers:

- int
- double
- char



# Basic Input and Output in C++


