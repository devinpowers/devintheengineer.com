---
layout: archive
permalink: /C++/c++_iterators
title: "Iterators in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

Iterators are used to point to Memory Adresses of STL containers, they're an object designed to traverse through a container, which allows us access to each element on the way.

Different container may provide different kinds of iterators.

In the case of Maps, iterators "points" to the value of Pair of key:value

Iterators are nice because we don't have to worry about the size of the containter (like we do with lists) and we can effectively get access to every container as not all containers allow .at or [] to access elements!


![inserting an Image](/images/C++/iterators/Page1.jpg)
![inserting an Image](/images/C++/iterators/Page2.jpg)
![inserting an Image](/images/C++/iterators/Page3.jpg)
![inserting an Image](/images/C++/iterators/Page4.jpg)
![inserting an Image](/images/C++/iterators/Page5.jpg)
![inserting an Image](/images/C++/iterators/Page6.jpg)
![inserting an Image](/images/C++/iterators/Page7.jpg)





## More on Reversing Iterators in C++


    #include<vector>
    using std::vector; 
    #include<iostream>
    using std::cout; using std::endl; 

    int main() 
    {
        vector<int> v = {1,2,3,4,5};

        for ( auto pos = v.rbegin(); pos != v.rend(); ++pos ){

                cout << *pos << endl;
        }
    }


Output

    5
    4
    3
    2
    1

### More on Iterators 

    #include<iostream>
    using std::cout; using std::endl;
    #include<vector>
    using std::vector;
    #include<string>
    using std::string;
    #include<sstream>
    using std::ostringstream;

    template<typename T>
    string vector_to_string ( const vector<T> & v) 
    {
        ostringstream oss;

        for (auto iter = v.cbegin(); iter != v.cend(); ++iter )
        {
            oss << *iter << ", ";
        }
        string results = oss.str();
        return results.substr(0, results.size() - 2);

    }



    int main()
    {    
        vector<int> v{ 1,2,3,4,5,6,7,8,9,10};

        vector<long> v2{ 1,2,3,4,5,6,7,8,9,10};

        cout << "Vector of Ints to String: " << vector_to_string (v) << endl;

        cout << "Vector of Long to String: " << vector_to_string (v2) << endl;

    }

Output

    Vector of Ints to String: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
    Vector of Long to String: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10


## add more on iterators using different containers like Maps and Lists


## Iterator using Maps

When you iterate through a map, you're iterating through pairs

A map iterator points to a pair

If you want to print the key of the pair via the iterator, we can do either:

- (*itr).first
- itr->first

The -> operator means a member of what the iterator points to

When iterating through pairs, the KEY is CONSTANT value, we can view but not change a key value via iteration

## Maps Containers use Bidirectional iterators

- Not a sequence (maps have an ordering, but not the order that the elements were inserted)

- Can advance iterator both forward and backward

- No random access via []

- no pointer arithmetic of itr < v.end()

- Instead use itr != v.end()

- Order of a Map elements is based on the key!

