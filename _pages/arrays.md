---
layout: archive
permalink: /C++/arrays
title: "Arrays In C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---


Common Arrays in C++

Array example with already knowing the input:


    #include <iostream>

    using namespace std;

    int main()
    {
        int guesses[] = {10, 13, 23, 45, 78, 12, 10};

        cout << guesses[3] << endl;

        guesses[3] = 300;

        cout << guesses[3] << endl;

    }

Array Example without knowing the "Size":


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


More on Arrays:


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


Using Arrays inside Functions










Vectors in C++


    #include <iostream>
    #include <vector>

    using namespace std;

    int main()
    {

        vector<int> data = {1, 2, 3};

        data.push_back(4);

        cout << data[3] << endl;

    }

