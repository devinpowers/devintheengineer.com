---
layout: archive
permalink: /C++/c++_algorithms
title: "Basic C++ Algorithms"
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---
#### Different Categories of Algorithms

- Non-modifying
    - Examples: find, find_if, search

- Modifying
    - Examples: copy, transform

- Removing (elements)

- Mutating (elements)
    - Sorting (elements order changes)
    - Examples: sort

- Operation on sorted collections
    - Examples: set_union, set_intersections, set_difference


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



## Find Algorithm



    #include<iostream>
    using std::cout; using std::endl;
    #include <vector> 
    using std::vector;
    #include <algorithm> 
    using std::find;

    int main () 
    { 
        vector<int> vec { 10, 20, 30, 40 }; 
        
        // Print Original Vector 
    cout << "Original vector :"; 
        for (int i=0; i<vec.size(); i++) 
        {
            cout << " " << vec[i]; 
        }
            
        cout << "\n"; 
        
        int search = 40; 
        // Iterator used to store the position of the searched element
        vector<int>::iterator it; 
        
        // find function call 
        it = find (vec.begin(), vec.end(), search); 

        if (it != vec.end()) 
        { 
            cout << "Element " << search <<" found at position : " ; 
            cout << it - vec.begin() << " (counting from zero) \n" ; 
        } 
        else
            cout << "Element not found.\n\n"; 
            
    } 

Output

    Original vector : 10 20 30 40
    Element 40 found at position : 3 (counting from zero) 



## Other stuff
