---
layout: archive
permalink: /C++/arrays
title: "Arrays In C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---



Arrays are Statically Sized, when you code out the application, you have to input the number of spaces!

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



Using Arrays inside Functions
















If you want to share memory of the data between the print_vector and the main() function you can add the & sign:

    #include <iostream>
    #include <vector>

    using namespace std;

    void print_vector(vector<int> & data)
    {
        data.push_back(12);
        for(int i = 0; i < data.size(); i++)
        {
            cout << data[i] << "\t";
        }
        cout << "\n";
    }

    int main()
    {
        vector<int> data = {1, 2, 3};
        print_vector(data);
        print_vector(data);
        print_vector(data);
        print_vector(data);

    }


STL



Printing STL 


    #include <iostream>
    #include<array>

    using namespace std;


    void print_array( array<int,20> data)
    {
        for (int i = 0; i < data.size(); i++)
        {
            cout << data[i] << "\t";
        }
        cout << "\n";

    }

    int main()

    {
        array <int, 20 > data = {1, 2, 3};
        print_array(data);

    }

What if we don't want to print all the extra elements ( 17 0's)?

we can pass in an element indicating the size of the array we want printed


    #include <iostream>
    #include<array>

    using namespace std;


    void print_array( array<int,20> data, int size)
    {
        for (int i = 0; i < size; i++)
        {
            cout << data[i] << "\t";
        }
        cout << "\n";

    }

    int main()

    {
        array <int, 20 > data = {1, 2, 3};

        print_array(data, 3);

    }




Range Loop for iterating thru a collection


Using a Regualar Loop:

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


Using a For a Range Loop:


    #include <iostream>


    using namespace std;

    int main()
    {
        int data[] = {1,2,3,4,5,6};

        for(int n : data)
        {
            cout << n << "\t";


        }
        /*
        for (int i = 0; i < 6; i++)
        {
            cout << data[i] << "\t";
        
        }
        */
        cout << "\n";


    }