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


Insert and Erase are Similar to Map's

- Insert on a set retruns a pair
  - while the iterator points to the base type (int, double, string), not the pair
- When you erase, it erases all examples of the key (which is only one)
- Iterator on sets are constant, you can't change a key in place

### Inserting into a set example

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



### Set Algorithm Examples

![inserting an Image](/images/C++/sets/Page1.jpg)
![inserting an Image](/images/C++/sets/Page2.jpg)
![inserting an Image](/images/C++/sets/Page3.jpg)
![inserting an Image](/images/C++/sets/Page4.jpg)
![inserting an Image](/images/C++/sets/Page5.jpg)
![inserting an Image](/images/C++/sets/Page6.jpg)



## other things to do with Sets


    #include<iostream>
    using std::cout; using std::endl;
    #include<set>
    using std::set;
    #include<vector>
    using std::vector;
    #include<iterator>
    using std::ostream_iterator;
    #include<algorithm>
    using std::set_union; using std::set_intersection;
    using std::set_difference;
    using std::set_symmetric_difference;
    using std::sort; using std::find;

    int main (){

        // Regular sets get sorted automatically in C++
        set<long> set1 = {5,3,1,4,2};
        set<long> set2 = {1,8,3,5,9};

        //print our set
        cout << "Set 1: ";
        for (auto element : set1 )
        {
            cout << element << ", ";
        }
        cout << endl;

        cout << "Set 2: ";
        for (auto element : set2)
        {
            cout << element << ", ";
        }
        cout << endl;
    
    }

Output

    Set 1: 1, 2, 3, 4, 5, 
    Set 2: 1, 3, 5, 8, 9,



### Using the .find() algorithm on a Set


    #include<iostream>
    using std::cout; using std::endl;
    #include<set>
    using std::set;
    #include<algorithm>
    using std::find;

    int main (){

        // Regular sets get sorted automatically in C++
        set<long> set1 = {5,3,1,4,2,6};   
        set<long> set2 = {1,8,3,5,9};

        set<long>::iterator iter, st;

        long search_for = 4;

        // iterator points to a position where 4 is
        iter = find(set1.begin(), set1.end(), search_for);

        cout << "The elements in the Set that come after " << search_for << " are: ";
        for (  st = iter; st != set1.end(); st++)
        {
            cout << *st << " ";
        }
        cout << endl;

    }

Output

    The elements in the Set that come after 4 are: 4 5 6 


## More