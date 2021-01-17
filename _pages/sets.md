---
layout: archive
permalink: /C++/sets
title: " Sets in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

Sets Represent Mathematical Sets, I have plently of notes on Sets in my Discrete Mathematical Section!!

- templated for one type (e.g. set of int, set of strings, set of long)
- They hold only one example of any element, if you add a duplicate of an existing element, it is ignored


Insert and Erase are Similar to Map;s

- Insert on a set retruns a pair
  - while the iterator points to the base type (int, double, string), not the pair
- When you erase, it erases all examples of the key (which is only one)
- Iterator on sets are constant, you can't change a key in place

# inserting into a set example

    #include<iostream>
    using std::cout; using std::endl;
    #include<iterator>
    using std::ostream_iterator;
    #include<set>
    using std::set;
    #include<string>
    using std::string;

    int main()
    {
        set<string> NBA;

        // insert method

        NBA.insert("Jordan");
        NBA.insert("Lebron");
        NBA.insert("Kobe");

        //declaring iterator to a set
        set<string>::iterator it;

        cout << "Elements of the set:     ";

        for (it = NBA.begin(); it != NBA.end(); it++)
        {
            cout << *it << ", ";
        }
        cout << endl;
    }

Output

    Elements of the set:     Jordan, Kobe, Lebron, 


### Removing an Element from a set Example


    NBA.erase("Jordan");

    cout << "After removing the GOAT:   ";
    
    for (it = NBA.begin(); it != NBA.end(); it++)
    {
        cout << *it << ", ";
    }
    cout << endl;



Output

    After removing the GOAT:   Kobe, Lebron,

Remember when we learned about sets in Discrete Mathmatics and about Union, intersection, etc? 

We can perform these on sets using generic Algorithms but for the Algorithms to work on the container, the container MUST BE sorted.

## Set Algorithms

- set_union
- set_intersection
- set_difference
- set_symmetric_difference



