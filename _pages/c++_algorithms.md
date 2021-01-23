---
layout: archive
permalink: /C++/c++_algorithms
title: "Basic C++ Algorithms"
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---


### Accumulate

![inserting an Image](/images/C++/algorithms/Page1.jpg)

    
    #include<iostream>
    using std::cout; using std::endl; 
    #include<vector>
    using std::vector;
    #include<string>
    using std::string;
    #include<numeric>
    using std::accumulate;
    #include<functional>
    using std::multiplies; using std::minus; using std::plus;

    int main()
    {
        vector <int > vect_numbers ={ 1,2,3,4,5,6};
        vector <string> vect_string = {"Hello", "my", "name", "is", "Devin!"};

        string output_string;
        int output_numbers;

        output_numbers = accumulate(vect_numbers.begin(), vect_numbers.end(), 0);

        output_string = accumulate(vect_string.begin(), vect_string.end(), string(""));

        cout << "The accumulation of vector 'Vect' is: " <<  output_numbers << endl;

        cout << "Adding a string up: " << output_string << endl;

    }

Output
    The accumulation of vector 'Vect' is: 22
    Adding a string up: HellomynameisDevin!


![inserting an Image](/images/C++/algorithms/Page2.jpg)


    #include<iostream>
    using std::cout; using std::endl; 
    #include<vector>
    using std::vector;
    #include<string>
    using std::string;
    #include<numeric>
    using std::accumulate;
    #include<functional>
    using std::multiplies; using std::minus; using std::plus;

    int main()
    {
        vector <int > vect_numbers ={ 1,8,3,6,2,6};
        vector <string> vect_string = {"Hello", "my", "name", "is", "Devin!"};

        string output_string;
        int output_numbers;

        output_string = accumulate(vect_string.begin(), vect_string.end(), string(""));
        //cout << "Adding a string up: " << output_string << endl;

        output_numbers = accumulate(vect_numbers.begin(), vect_numbers.end(), 1 , multiplies<int>());


        cout << "The Sum is: " << accumulate(vect_numbers.begin(), vect_numbers.end(), 0 , plus<int>()) << endl;

        cout << "The Product is: " << accumulate(vect_numbers.begin(), vect_numbers.end()-1, 1 , multiplies<int>()) << endl;
        
        
        cout << "The Difference is : " << accumulate(vect_numbers.begin(), vect_numbers.end(), 0, minus<int>() ) << endl;
    }

Output

    The Sum is: 26
    The Product is: 288
    The Difference is : -26


