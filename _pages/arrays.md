---
layout: archive
permalink: /C++/arrays
title: "Arrays In C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---



Arrays are Statically Sized, when you code out the application, you have to input the number of spaces!

![inserting an Image](/images/C++/arrays/Page1.jpg)
![inserting an Image](/images/C++/arrays/Page2.jpg)

![inserting an Image](/images/C++/arrays/Page3.jpg)



Heres an example of an Array, and we will return the 3 index from it

    #include <iostream>

    using namespace std;

    int main()
    {

        int guesses[] = {10, 13, 23, 45, 78, 12, 10};

        cout << guesses[3] << endl;
    }

Output

    45

We can change any value in our array, here's an example of changing value at index 3:

    #include <iostream>

    using namespace std;

    int main()
    {
        int guesses[] = {10, 13, 23, 45, 78, 12, 10};

        cout << guesses[3] << endl;

        guesses[3] = 300;

        cout << guesses[3] << endl;

    }

Output

    45
    300

We can fill the Size of an Array and then insert into the array, here an example of doing that


    #include <iostream>

    using namespace std;

    int main()
    {
        int guesses[20];

        guesses[0] = 10;

        cout << guesses[0] << endl;

        cin >> guesses[0];

        cout << guesses[0] << endl;

    }


### Working with Loop and Arrays

![inserting an Image](/images/C++/arrays/Page4.jpg)
![inserting an Image](/images/C++/arrays/Page5.jpg)


How do we get the Size of an Array?



    #include <iostream>

    using namespace std;

    int main()
    {
        int guesses[] = {12, 43, 23, 43, 23};

        int size = sizeof(guesses)/ sizeof(int);

        cout << size << endl;

    }

Ouput

    5

Let's iterate through the array using a Loop!


    #include <iostream>

    using namespace std;

    int main()
    {
        int guesses[] = {12, 43, 23, 43, 23};

        int size = sizeof(guesses) / sizeof(int) ;

        for (int i = 0; i < size; i++ )
        {
            cout << guesses[i] << "\t";
        }

    }

Output

    12      43      23      43      23


What would happen if we changed the Size of the Array to 10?


    #include <iostream>

    using namespace std;

    int main()
    {
        int guesses[10] = {12, 43, 23, 43, 23};

        int size = sizeof(guesses) / sizeof(int) ;

        for (int i = 0; i < size; i++ )
        {
            cout << guesses[i] << "\t";
        }

    }

Output

    12      43      23      43      23      0       0       0       0       0 

There would be extras zeros at the end!

How do we fix this??

We can declare a number_element variable and iterate up to the size of it


    #include <iostream>

    using namespace std;

    int main()
    {
        int guesses[10] = {12, 43, 23, 43, 23};
        
        int number_elements = 5;

        int size = sizeof(guesses) / sizeof(int) ;

        for (int i = 0; i < number_elements; i++ )
        {
            cout << guesses[i] << "\t";
        }

    }

Output

    12      43      23      43      23



### Passing Arrays to Functions

Note that Arrays DO NOT remember their length when passed!

![inserting an Image](/images/C++/arrays/Page6.jpg)
![inserting an Image](/images/C++/arrays/Page7.jpg)

How do we fix/go about this issue?

We can pass in the Size of the Array as an Argument.


    #include <iostream>

    using namespace std;


    void print_array( int array[], int size )
    {
        for (int i = 0; i < size; i++ )
        {
            cout << array[i] << "\t";
        }
        cout << endl;
    }

    int main()
    {
        int guesses[] = {12, 43, 23, 43, 23};
        
        int size = sizeof(guesses) / sizeof(int);

        print_array(guesses, size);

    }


Output

    12      43      23      43      23


### Range Based For Loops

![inserting an Image](/images/C++/arrays/Page8.jpg)

iterate through a collection


    #include <iostream>

    using namespace std;

    int main()
    {
        int data[] = {1,2,3,4,5,6};

        for (int i = 0; i < 6; i++)
        {
            cout << data[i] << "\t";
        }
        cout << "\n";

    }

Output

    1       2       3       4       5       6


Using a For Range Loop:

Using std=c++11


    #include <iostream>

    using namespace std;

    int main()
    {
        int data[] = {1,2,3,4,5,6};

        for (int n : data)
        {
            cout << n << "\t";
        }
        cout << "\n";

    }

Ouput

    1       2       3       4       5       6


Can you for STL and Vectors as well!


# Multidimensional Arrays and Nested Vectors

![inserting an Image](/images/C++/arrays/Page9.jpg)


    #include <iostream>


    using namespace std;

    int main()
    {
        int grades[][3] = {{1,2,3},{4,5,6},{7,8,9}};

        for (int r = 0; r < 3; r++)
        {
            for ( int c = 0; c < 3; c++ )
            {
                cout << grades[r][c] << "\t";
            }
            cout << "\n";
        };    

    }

Output

    1       2       3
    4       5       6
    7       8       9
