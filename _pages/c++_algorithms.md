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


# Non-modifying

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



### Find Algorithm


![inserting an Image](/images/C++/algorithms/find.jpg)



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



### Using find_if Algorithm


![inserting an Image](/images/C++/algorithms/find_if.jpg)

    #include<iostream>
    using std::cout; using std::endl; using std::boolalpha;
    #include <vector> 
    using std::vector;
    #include <algorithm> 
    using std::find_if;


    bool IsOdd( int i)
    {
        return i % 2;
    }

    int main () 
    {
        vector<int> vec { 10, 20, 30, 40, 55};

        vector<int>::iterator it;

        it = find_if(vec.begin(), vec.end(), IsOdd);

        cout << "The first odd value is: " << *it << endl;
    }

Output

    The first odd value is: 55


### Serach Algorithm


- add later


# Modifying Algorithms


### copy

![inserting an Image](/images/C++/algorithms/copy.jpg)



    #include<iostream>
    using std::cout; using std::endl; using std::boolalpha;
    #include <vector> 
    using std::vector;
    #include <algorithm> 
    using std::copy;

    int main() 
    { 
    vector<int> v1 = { 1, 8, 2, 3, 1, 3, 10 };
        
    vector<int> v2(7);
        
    copy(v1.begin(), v1.end(), v2.begin());
        
    // printing new vector
    cout << "The new vector elements entered using copy() : ";
    for(int i = 0; i < v2.size(); i++)
    {
        cout << v2[i] << " ";
    }
    cout << endl;

    } 

Output

    The new vector elements entered using copy() : 1 8 2 3 1 3 10 



## Special Iterators!

- The Issue with Copy algorithm is that it requires that our destination container is large enough to hold what were copying. Theres two special kinds of iterators that allow us to get around this issue.
    - Insert iterator
    - Stream iterator

### Insert Iterator

- Depends on the container, a vector works best when we insert at the back
- Lists, sets insert at a particular position


## back_inserter for copying a Vector

![inserting an Image](/images/C++/algorithms/back.jpg)



    #include<iostream>
    using std::cout; using std::endl; using std::boolalpha;
    #include <vector> 
    using std::vector;
    #include <algorithm> 
    using std::copy;
    #include<iterator>
    using std::back_inserter;

    int main() 
    { 
    vector<int> v1 = { 1, 8, 2, 3, 1, 3, 10, 12, 67, 90, 100, 82 };
        
    vector<int> v2;
        
    copy(v1.begin(), v1.end(),back_inserter(v2));
        
    // printing new vector
    cout << "The new vector elements entered using copy() : ";
    for(int i = 0; i < v2.size(); i++)
    {
        cout << v2[i] << " ";
    }
    cout << endl;

    } 



### Stream Iterator (ostream_iterator)

![inserting an Image](/images/C++/algorithms/ostream.jpg)



    #include<iostream>
    using std::cout; using std::endl; using std::boolalpha;
    #include <vector> 
    using std::vector;
    #include <algorithm> 
    using std::copy;
    #include<iterator>
    using std::ostream_iterator;

    int main() 
    { 

    vector<int> v1 = { 1, 8, 2, 3, 1, 3, 10, 12, 67, 90, 100, 82 };

    ostream_iterator<int> out(cout, ",");
            
    copy(v1.begin(), v1.end(), out);

    cout << endl;
        

    } 

Output

    1,8,2,3,1,3,10,12,67,90,100,82,



    #include<iostream>
    using std::cout; using std::endl;
    #include <vector> 
    using std::vector;
    #include<string>
    using std::string;
    #include <algorithm> 
    using std::copy;
    #include<iterator>
    using std::ostream_iterator;

    int main() 
    { 


    vector<string> v1 = { "Hello", "my", "name", "is", "Devin" };

    ostream_iterator<string> out(cout, " ");
            
    copy(v1.begin(), v1.end(), out);

    cout << endl;
        

    } 

Output

    Hello my name is Devin 


### transform

- transforms range
![inserting an Image](/images/C++/algorithms/transform1.jpg)



#### Unary Operation


    #include<iostream>
    using std::cout; using std::endl;
    #include <vector> 
    using std::vector;
    #include<string>
    using std::string;
    #include <algorithm> 
    using std::toupper;
    using std::transform;
    #include<iterator>
    using std::ostream_iterator;

    char upper(char ch)
    {
        return toupper(ch);
    }

    int main() 
    { 
        string s = "Devin Powers ";

        transform(s.begin(), s.end(), ostream_iterator<char> (cout, "\n"), upper);

    } 

Output

    D
    E
    V
    I
    N
    
    P
    O
    W
    E
    R
    S


Another Example

![inserting an Image](/images/C++/algorithms/transform2.jpg)



    #include<iostream>
    using std::cout; using std::endl;
    #include <vector> 
    using std::vector;
    #include<string>
    using std::string;
    #include <algorithm> 
    using std::toupper;
    using std::transform;

    int increment( int l)
    {
        return l+9;
    }

    int main() 
    { 
        vector<int> vec = {1,2,4,5,6};

        transform( vec.begin(), vec.end(), vec.begin(), increment);

        // print Vector!!

        for ( auto element : vec )
        {
            cout << element << ", ";
        }
    }

Output


    10, 11, 13, 14, 15, 


#### Binary Operation







# Sorting Algorithms


### sort

- Sorts elements in range
