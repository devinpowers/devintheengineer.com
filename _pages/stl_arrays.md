---
layout: archive
permalink: /C++/stl_arrays
title: "STL Arrays in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

Standard Template Library

![inserting an Image](/images/C++/stl/Page1.jpg)
![inserting an Image](/images/C++/stl/Page2.jpg)

How do we create an STL Array?

    #include <iostream>
    #include <array>

    using namespace std;


    int main()
    {
        array <int, 20 > data = {1,2,3};

        cout << data[0] << endl;
        cout << data[1] << endl;
        cout << data[2] << endl;
        cout << data[8] << endl;
    }

Output

    1
    2
    3
    0

Lets make a print_array function with a loop to print our STL Array


    #include <iostream>
    #include <array>

    using namespace std;


    void print_array( array<int,20> data)
    {
        for ( int i= 0; i < data.size(); i++)
        {
            cout << data[i] << "\t";

        }
        cout << "\n";
    }

    int main()
    {
        array <int, 20 > data = {1,2,3};

        print_array(data);
    }

Output

    1       2       3       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0

Can we just print (1,2, 3) ?

yes, we can pass in the size as a seperate argument


    #include <iostream>
    #include <array>

    using namespace std;


    void print_array( array<int,20> data, int size)
    {
        for ( int i= 0; i < size; i++)
        {
            cout << data[i] << "\t";

        }
        cout << "\n";
    }

    int main()
    {
        array <int, 20 > data = {1,2,3};


        print_array(data, 3);
    }

Output

    1       2       3

