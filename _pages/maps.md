---
permalink: /C++/maps
title: " Maps in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"

toc: true
toc_label: "Table of Contents" 
  
---

Inserting, Deleting and other Methods in Map Data Structures

## Pairs

* Working with Pairs in C++, Different examples below

* The Library to Include for **Pair Type** is #include<utility>

    * Which Includes:

        * **pair**
        * **make_pair**

* The **Pair Type** holds **exactly** two values, it's templated on the two values

* **pair<string, int > word_count;**




```cpp
#include<iostream>
using std::cout; using std::endl;
#include<string>
using std::string;
#include<utility>
using std::pair; using std::make_pair;

int main(){

    // initialize a pair

    pair <int, string > a;
    pair <int, string > b;

    // lets use the make_pair function

    a = make_pair( 3, "Chris Paul");
    b = make_pair( 23, "Michael Jordan");

    // printting out the first and second values of the pairs

    cout << "a: " << a.first << " , " << a.second << endl;
    cout << "b: " << b.first << " , " << b.second << endl;

    return 0;

}

```

Output
```cpp
a: 3 , Chris Paul
b: 23 , Michael Jordan
```

Another Example

```cpp
#include<iostream>
using std::cout; using std::endl;
#include<string>
using std::string;
#include<vector>
using std::vector;
#include<utility>
using std::pair; using std::make_pair;
#include<sstream>
using std::ostringstream;
#include<iterator>
using std::ostream_iterator;
#include<algorithm>
using std::transform;


using NBA = pair<string,int>; 


string pair_to_string(NBA p){
ostringstream oss;
oss << p.first <<":"<<p.second;
return oss.str();
}


int main(){


    vector<NBA> v(3, NBA("Griffin", 23));

    v.push_back(make_pair("Pippin", 33));
    v.push_back(make_pair("Billups", 1));
    v.push_back(make_pair("Wallace", 3));

    // can print with normal pair_to_string

    transform (v.begin(), v.end(), ostream_iterator<string>(cout, ", "), pair_to_string );
    
    cout << endl;


}
```


Output

```cpp
Griffin:23, Griffin:23, Griffin:23, Pippin:33, Billups:1, Wallace:3, 
```


## Maps

Insert into Map 3 Different ways!

```cpp
#include<iostream>
using std::cout; using std::endl;
#include <map> 
using std::map;
#include<string>
using std::string;
#include<utility>
using std::pair; using std::make_pair;

int main() 
{ 
    
    map <int, string > nba;

    // insert elements into the nba map 3 different ways!!

    nba.insert({1, "Lebron James"});
    
    nba.insert(make_pair(3,"Steph Curry"));

    nba.insert(pair<int, string>(8, "Kobe Bryant"));


    //print out our map 

    cout << "KEY\tELEMENT\n";

    for (auto itr = nba.begin(); itr != nba.end(); ++itr) {
        cout << (*itr).first << '\t' << (*itr).second << '\n';

    }
} 

```







Erase in Maps

```cpp
#include<iostream>
using std::cout; using std::endl;
#include <map> 
using std::map;
#include<string>
using std::string;

int main()
{

    // initialize the Map container
    map<int, string> mp;

    // inserting into the Container
    mp.insert({ 2, "Lebron" });
    mp.insert({ 1, "Wade" });
    mp.insert({ 4, "Jordan" });
    mp.insert({ 5, "Durant" });
    mp.insert({ 3, "Curry" });


    // prints the elements
    cout << "The map before using erase() is : \n";

    cout << "KEY\tELEMENT\n";

    for (auto itr = mp.begin(); itr != mp.end(); ++itr) {
        cout << (*itr).first << '\t' << (*itr).second << '\n';
    }

    // Lets Erase some Keys in our Map
    mp.erase(1);
    mp.erase(3);

    // prints the elements
    cout << "\nThe map after applying erase() function is : \n";
    cout << "KEY\tELEMENT\n";
    for (auto itr = mp.begin(); itr != mp.end(); ++itr) {

        cout << (*itr).first << '\t' << (*itr).second << '\n';

    }

}
```


output

```cpp

The map before using erase() is : 
KEY     ELEMENT
1       Wade
2       Lebron
3       Curry
4       Jordan
5       Durant

The map after applying erase() function is : 
KEY     ELEMENT
2       Lebron
4       Jordan
5       Durant

```

Erase Given a position, using a find algorithm

```cpp
#include<iostream>
using std::cout; using std::endl;
#include <map> 
using std::map;
#include<string>
using std::string;

int main()
{

    // initialize the Map container
    map<int, string> mp;

    // inserting into the Container using NBA Players
    mp.insert({ 2, "Lebron" });
    mp.insert({ 1, "Wade" });
    mp.insert({ 4, "Jordan" });
    mp.insert({ 5, "Durant" });
    mp.insert({ 3, "Curry" });

    // prints the elements
    cout << "The map before using erase() is : \n";
    cout << "KEY\tELEMENT\n";
    for (auto itr = mp.begin(); itr != mp.end(); ++itr) {
        cout << (*itr).first << '\t' << (*itr).second << '\n';
    }

    // function to erase given position
    auto it = mp.find(1);
    mp.erase(it);

    auto it1 = mp.find(3);
    mp.erase(it1);

    // prints the elements
    cout << "\nThe map after applying erase() is : \n";
    cout << "KEY\tELEMENT\n";

    for (auto itr = mp.begin(); itr != mp.end(); ++itr) {
        cout << (*itr).first << '\t' << (*itr).second << '\n';
    }
    return 0;
}
```

Output

```cpp
The map before using erase() is : 
KEY     ELEMENT
1       Wade
2       Lebron
3       Curry
4       Jordan
5       Durant

The map after applying erase() is : 
KEY     ELEMENT
2       Lebron
4       Jordan
5       Durant
```



![inserting an Image](/images/C++/maps/Page1.jpg)
![inserting an Image](/images/C++/maps/Page2.jpg)
![inserting an Image](/images/C++/maps/Page3.jpg)
![inserting an Image](/images/C++/maps/Page4.jpg)
![inserting an Image](/images/C++/maps/Page5.jpg)
![inserting an Image](/images/C++/maps/Page6.jpg)
![inserting an Image](/images/C++/maps/Page7.jpg)
![inserting an Image](/images/C++/maps/Page8.jpg)
![inserting an Image](/images/C++/maps/Page9.jpg)
![inserting an Image](/images/C++/maps/Page10.jpg)
![inserting an Image](/images/C++/maps/Page11.jpg)
![inserting an Image](/images/C++/maps/Page12.jpg)
![inserting an Image](/images/C++/maps/Page13.jpg)
![inserting an Image](/images/C++/maps/Page14.jpg)




