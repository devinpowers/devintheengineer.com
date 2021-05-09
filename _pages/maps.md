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


**How does one Access the values?**

To access the values (which arecalled data memebers, not functions) you** use **.first** and **.second**

![inserting an Image](/images/C++/maps/pair1.jpg)

Here an example of Pairs below:

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

**Note:** We can't print a pair, instead you have to print the elements!

We use **ostringstrem** !

![inserting an Image](/images/C++/maps/pair2.jpg)

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


Another Example of **making pairs**
![inserting an Image](/images/C++/maps/pair3.jpg)


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


using NBA = pair<string,int>;  // Custom Data Type (pair as a Type!)

string pair_to_string(NBA p){
    ostringstream oss;
    oss << p.first <<":"<<p.second;
    return oss.str();
}


int main(){

    // Different ways to "Create Pairs"
    
    NBA pair_1("Jordan", 23);
    NBA pair_2("Paul", 3);

    pair<string, int> pair_3, pair_4, pair_5;

    pair_3 = make_pair("Kobe", 24);
    pair_4 = make_pair("Curry", 30);

    pair_5 = {"Lebron", 23};

    // Lets change pair 1
    cout << "Lets change pair 1: " << endl;
    pair_1.first = "Duncan";
    pair_2.second = 12;

    // Lets print 

    cout << "Pair 1: " << pair_to_string(pair_1) << endl;
    cout << "Pair 2: " << pair_to_string(pair_2) << endl;
    cout << "Pair 3: " << pair_to_string(pair_3) << endl;
    cout << "Pair 4: " << pair_to_string(pair_4) << endl;
    cout << "Pair 5: " << pair_to_string(pair_5) << endl;
}
```

**Output**

```cpp
Lets change pair 1: 
Pair 1: Duncan:23
Pair 2: Paul:12
Pair 3: Kobe:24
Pair 4: Curry:30
Pair 5: Lebron:23

```

#### More examples

##### Iterator Points to the Pair Example

* Using *iterators* to iterate through a map and print each *pair* out

```cpp
#include<iostream>
using std::cout; using std::endl;

#include<iterator>
using std::ostream_iterator;
#include<utility>
using std::pair; using std::make_pair;
#include<map>
using std::map;
#include<string>
using std::string;
#include<sstream>
using std::ostringstream;



template<typename K, typename V>
string pair_to_string(pair<K,V> p){
  ostringstream oss;
  oss << p.first <<":"<< p.second;
  return oss.str();
}


int main() {

    map<string, string> phone_book{ {"Devin", "555-2323"}, {"Bill", "555-1212"}, {"John", "555-1412"} }; // create map named phone_book
    map<string, string>::iterator iter;   // iterator

    // iter points to the pair
    cout << "Iter Points to the pair:" << endl;
    for (iter = phone_book.begin(); iter != phone_book.end(); ++iter){

    
      cout << pair_to_string( *iter ) << ", ";
    cout << "\n" << endl;
    }
    return 0;
}
```

**Output**

```cpp
Iter Points to the pair:
Bill:555-1212, 

Devin:555-2323, 

John:555-1412, 

```

#####  The element *is* the Pair Example

```cpp
#include<iostream>
using std::cout; using std::endl;

#include<iterator>
using std::ostream_iterator;
#include<utility>
using std::pair; using std::make_pair;
#include<map>
using std::map;
#include<string>
using std::string;
#include<sstream>
using std::ostringstream;



template<typename K, typename V>
string pair_to_string(pair<K,V> p){
  ostringstream oss;
  oss << p.first <<":"<< p.second;
  return oss.str();
}


int main() {

    map<string, string> phone_book{ {"Devin", "555-2323"}, {"Bill", "555-1212"}, {"John", "555-1412"} }; // create map named phone_book
    map<string, string>::iterator iter;   // iterator

    
   // element *is* the pair   (we  said the type was pair)
   cout << "Element is the pair: " << endl;
   for(pair<string,string> element : phone_book)     
   {
       cout << pair_to_string( element ) << ", ";

       cout << "\n" << endl;

   }

}
```

**Output**

```cpp
Element is the pair: 
Bill:555-1212, 

Devin:555-2323, 

John:555-1412, 
```


## Maps

* Maps are ordered associative containers that include:

    * Map
    * Multimap
    * Set
    * Multiset 

I will just cover **Maps** on this page!


It's important to remember that a map is **not** a sequence. maps have an ordering, but it not the order that the elements were inserted into the map.


### Bidirectional Iterators

* Maps yield biderectional iterators ( can advance both forward and backwards)
* No random access via []
* No pointer arithmetic
* No itr < v.end(), although it allows itr != v.end()

* Maps automatically insert new elements such that they're ordered:

    * Each map element is a **pair**
    * (key, value) in that order
    * Order of map element is based on the key!
    * You can search for elements fast!


#### Initialization, Key 

* Add later!



### Insert into Map 3 Different ways!

* Use **insert**


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
#include<map>
using std::map;


int main(){

    map<string, int> m;

    string word_1 = "hello1";
    string word_2 = "hello2";
    string word_3 = "hello3";



    m.insert({word_1, 1});
    m.insert(make_pair(word_2,2));
    m.insert(pair<string, int>(word_3,3));


    cout << "KEY\tELEMENT\n";

    for (auto itr = m.begin(); itr != m.end(); ++itr) {
        cout << (*itr).first << '\t' << (*itr).second << '\n';
    }

}

```

**Output:**

```cpp
KEY     ELEMENT
hello1  1
hello2  2
hello3  3
```

**NBA Example**

![inserting an Image](/images/C++/maps/map1.jpg)




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

**Output:**

```cpp
KEY     ELEMENT
1       Lebron James
3       Steph Curry
8       Kobe Bryant
```




### Erase in Maps (3 ways)

* Erase at Key
* Erase



#### Erase at Key

![inserting an Image](/images/C++/maps/erase_key.jpg)


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

### Erase Given a position, using a find algorithm

![inserting an Image](/images/C++/maps/erase_position.jpg)


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

**Output**

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


### Erase by Range

![inserting an Image](/images/C++/maps/erase_range.jpg)


### Map Size, Empty and Clear in STL
![inserting an Image](/images/C++/maps/Page6.jpg)




#### Game of Thrones Example
![inserting an Image](/images/C++/maps/got.jpg)


## More Map Methods

* Lets work with iterating through a map that are **pairs**

* A map iteraotr points to a **pair**

* If you want to print the key of the pair via an iterator you can type either:

    * (*itr).first;
    * itr->first;

* The -> operator means a member of what the iterator points to

When we iterate throgh, we cannot change a key (its a const value)

### Working with Pairs and Map Examples:

![inserting an Image](/images/C++/maps/map_pairs1.jpg)


### Find Key in Map Example (+ count Example)

![inserting an Image](/images/C++/maps/find_key.jpg)

```cpp
#include<iostream>
using std::cout; using std::endl;
#include <map> 
using std::map;
#include<string>
using std::string;
 
int main()
{
 
    // Initialize container
    map<int, int> mp;
 
    // Insert elements in random order
    mp.insert({ 2, 30 });
    mp.insert({ 1, 40 });
    mp.insert({ 3, 20 });
    mp.insert({ 4, 50 });
    mp.insert({ 9, 90 });
 
    cout << "Elements from position of 3 in the map are : \n";
    cout << "KEY\tELEMENT\n";
 
    // find() function finds the position
    // at which 3 is present
    for (auto itr = mp.find(3); itr != mp.end(); itr++) {  // function from where it finds 3
       
        cout << itr->first << '\t' << itr->second << '\n';
    }
 
    return 0;
}
```

**Output**

```cpp
Elements from position of 3 in the map are : 
KEY     ELEMENT
3       20
4       50
9       90
```

### Search Map by Value

![inserting an Image](/images/C++/maps/search_value.jpg)

### Other
![inserting an Image](/images/C++/maps/other.jpg)




## Extra Map Stuff


### Working with Maps that Have a Set as a Value

![inserting an Image](/images/C++/maps/map_set.jpg)

### How to Print map< Data Type, set<Data Type>>

![inserting an Image](/images/C++/maps/print_map_set.jpg)



###  Printing Regualr and Printing use Iterators
![inserting an Image](/images/C++/maps/print_regular.jpg)

### Iteration with vector of Pairs
![inserting an Image](/images/C++/maps/iteration_print.jpg)



### Iteration with Maps
![inserting an Image](/images/C++/maps/iteration_maps.jpg)

![inserting an Image](/images/C++/maps/iterate2.jpg)
![inserting an Image](/images/C++/maps/iterate3.jpg)
![inserting an Image](/images/C++/maps/iterate4.jpg)
![inserting an Image](/images/C++/maps/iterate5.jpg)
![inserting an Image](/images/C++/maps/iterate6.jpg)



### Sort Vector

![inserting an Image](/images/C++/maps/sort_vector.jpg)
