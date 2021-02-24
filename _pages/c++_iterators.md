---
layout: archive
permalink: /C++/c++_iterators
title: "Iterators in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

**Iterators are used to point to Memory Adresses of STL containers**, they're an __object__ designed to __traverse through a container__, which allows us __access to each element on the way.__

Different container may provide different kinds of iterators.

In the case of Maps, iterators "points" to the value of Pair of key:value

Iterators are nice because **we don't have to worry about the size of the containter** (like we do with lists, .size()) and we can effectively get access to every container as not all containers allow .at or [] to access elements!

What type is an iterator?

- an iterator type is **dependent on the container** that they point to!

#### Operators of Iterator:

1. begin() : This function is used to return the Beginning position of the container
2. end() : This function is used to return the afterend position of the container



![inserting an Image](/images/C++/iterators/Page1.jpg)

Example of an iterator:

```cpp

#include<iostream>
using std::cout; using std::endl;
#include <vector>
using std::vector;

int main(){

    vector <int> v ={1, 2, 3};

    vector <int >::iterator i; // declaring the iterator here

    for (i = v.begin(); i != v.end(); i++)
    {
        cout << *i << " ";
    }

}
```
Output:

```cpp
1 2 3
```


### There is 3 ways to iterate!

1.

```cpp
#include<iostream>
using std::cout; using std::endl;
#include <vector>
using std::vector;


int main(){

    vector <int> v ={1, 2, 3, 4, 5};

    for (int i = 0; i < static_cast<int>(v.size()); i++ ){
        cout << v[i] << endl;
    }
}
```
Output:
```cpp
1
2
3
4
5
```
2. 

```cpp
#include<iostream>
using std::cout; using std::endl;
#include <vector>
using std::vector;


int main(){

    vector <int> v ={1, 2, 3, 4, 5};

    for (auto element : v)
    {
        cout << element << endl;
    }
}
```
Output:
```cpp
1
2
3
4
5
```
3.

```cpp
#include<iostream>
using std::cout; using std::endl;
#include <vector>
using std::vector;


int main(){

    vector <int> v ={1, 2, 3, 4, 5};

    for (auto ptr = v.begin(); ptr != v.end(); ++ptr)
    {
        cout << *ptr << endl;
    }

}

```

Output:
```cpp
1
2
3
4
5
```








![inserting an Image](/images/C++/iterators/Page2.jpg)


![inserting an Image](/images/C++/iterators/Page3.jpg)

```cpp
#include<iostream>
using std::cout; using std::endl;
#include <vector>
using std::vector;


void print_vector(vector<int> vec)
{
    //prints vector out
    vector <int >::iterator i; // have to declare the iterator!!!
    for ( i = vec.begin(); i != vec.end(); i++ ){
        cout << *i << " ";
    }
}

int main(){

    vector <int> v ={1, 2, 3};

    vector <int >::iterator i; // declaring the iterator here

    for (i = v.begin(); i != v.end(); i++)
    {
        if ( i == v.begin() ) {

            i = v.insert(i, 5); // insert 5
        }
    }
    cout << "Vector after adding value: " << endl;
    print_vector(v);
    cout << endl;

    // lets delete a element using iterators

    for (i = v.begin(); i != v.end(); i++)
    {
        if ( i == v.begin() + 1 ) {

            i = v.erase(i);
    }
    }


    cout << "Vector after deleting a Value: " << endl;

    print_vector(v);

    cout << endl;

}

```

Output:

```cpp
Vector after adding value: 
5 1 2 3 
Vector after deleting a Value: 
5 2 3 
```

As you can see, we can easily and dynamically add and remove elements from the containers using iterator, if we tried to do the same without them, it would be very tedious and require shifting the elements everytime before we inserted and deleted!




What if I don't Declare an Iterator? (USe auto)
![inserting an Image](/images/C++/iterators/Page4.jpg)


```cpp

#include<iostream>
using std::cout; using std::endl;
#include <vector>
using std::vector;


int main(){

    vector <int> v ={1, 2, 3, 4, 5};

    for (auto itr = v.begin(); itr != v.end(); ++ itr)
    {
        cout << *itr << endl;
    }

}

```

Output:

```cpp
1
2
3
4
5
```

## For Each
![inserting an Image](/images/C++/iterators/Page5.jpg)

```cpp

#include<iostream>
using std::cout; using std::endl;
#include <vector>
using std::vector;


int main(){

    vector <int> v ={1, 2, 3, 4, 5};

    for (auto itr : v )
    {
        cout << itr << endl;
    }

}
```
Output:
```cpp
1
2
3
4
5
```


![inserting an Image](/images/C++/iterators/Page6.jpg)


## More on Reversing Iterators in C++

```cpp
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
```

Output

```cpp
5
4
3
2
1
```
### Vector to String Function with ostringstream using iterators!!!
![inserting an Image](/images/C++/iterators/Page7.jpg)

```cpp
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
```
Output

```cpp
Vector of Ints to String: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
Vector of Long to String: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
```

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


![inserting an Image](/images/C++/iterators/Page81.jpg)

## Iterating thru a Vector with a Pair as its Data type:

```cpp
#include<iostream>
using std::cout; using std::endl;
#include<string>
using std::string;
#include <vector>
using std::vector;
#include<utility>
using std::pair; using std::make_pair;
#include<sstream>
using std::ostringstream;

template <typename K, typename V >
string pair_to_string(pair<K,V> pair){
ostringstream oss;
oss << pair.first <<":"<<pair.second;
return oss.str();
}

int main()
{

    vector<pair<string, int>> vec1;

    vec1.push_back( make_pair("Devin", 25));
    vec1.push_back( make_pair("Abe", 24));
    vec1.push_back( make_pair("Luke", 56));

    vector<pair<string, int>>::iterator itr;

    for ( itr = vec1.begin(); itr != vec1.end(); itr++)
    {
        cout << pair_to_string(*itr) << endl;

    }
    

}

```

Output 

```cpp
Devin:25
Abe:24
Luke:56
```


## Iterating thru a Vector with a Pair as its Data type using first and second

Basic Problem

```cpp
#include<iostream>
using std::cout; using std::endl;
#include<string>
using std::string;
#include <vector>
using std::vector;
#include<utility>
using std::pair; using std::make_pair;


int main()
{

    vector<pair<string, int>> vec1;

    vec1.push_back( make_pair("Devin", 25));
    vec1.push_back( make_pair("Abe", 24));
    vec1.push_back( make_pair("Luke", 56));

    vector<pair<string, int>>::iterator itr;

    for ( itr = vec1.begin(); itr != vec1.end(); itr++)
    {
        cout << itr->first << " : " << itr->second << endl;

    }
    

}
```

Output

```cpp
Devin : 25
Abe : 24
Luke : 56
```
![inserting an Image](/images/C++/iterators/Page9.jpg)
![inserting an Image](/images/C++/iterators/Page10.jpg)
![inserting an Image](/images/C++/iterators/Page11.jpg)
![inserting an Image](/images/C++/iterators/Page12.jpg)
![inserting an Image](/images/C++/iterators/Page13.jpg)
![inserting an Image](/images/C++/iterators/Page14.jpg)




## Iterators and Maps!


```cpp
#include<iostream>
using std::cout; using std::endl;
#include<string>
using std::string;
#include <vector>
using std::vector;
#include<utility>
using std::pair; using std::make_pair;
#include<sstream>
using std::ostringstream;
#include<map>
using std::map;


template <typename K, typename V >
void print_map ( map<K,V>&  map)
{
    for (auto const& pair : map)
    {
        cout << pair.first << " : " << pair.second << endl;
    }
}


int main()
{
    map <string, string> map_0 = { {"Devin", "Powers"}, {"Luke", "Hirt"}};

    map <int, string> map_1 = { {3, "Devin"}, {1, "Luke"}, {4, "Abe"}};

    print_map(map_1);

    print_map(map_0);

}
```

Output

```cpp
1 : Luke
3 : Devin
4 : Abe
Devin : Powers
Luke : Hirt
```

### Iterating over a Map with Data Type values of string and Set

```cpp
#include<iostream>
using std::cout; using std::endl;
#include<string>
using std::string;
#include <vector>
using std::vector;
#include<utility>
using std::pair; using std::make_pair;
#include<sstream>
using std::ostringstream;
#include<map>
using std::map;
#include<set>
using std::set;


void print_map (  map <string, set<string>> map_passed)

{
    map <string, set<string>>::iterator itr;

    for (itr = map_passed.begin(); itr != map_passed.end(); itr++ )
    {
        cout << itr->first << " : ";

        for (auto itr2 = itr->second.begin(); itr2 != itr->second.end(); itr2++ )
        {
            cout << *itr2 << ", ";
        }
        cout << "\n";
    }
}




int main()
{
    map <string, set<string> > map_sets = {

        {"Server One", {"Devin","Luke", "Abe"}},
        {"Server Two", {"Noah", "Nick"}},
        {"Server Three", {"Jimmy"}}
        
        };

    print_map(map_sets);

}
```

Output 

```cpp
Server One : Abe, Devin, Luke, 
Server Three : Jimmy, 
Server Two : Nick, Noah, 
```

## We can do the same problem above without iterators!

```cpp
#include<iostream>
using std::cout; using std::endl;
#include<string>
using std::string;
#include <vector>
using std::vector;
#include<utility>
using std::pair; using std::make_pair;
#include<sstream>
using std::ostringstream;
#include<map>
using std::map;
#include<set>
using std::set;


void print_map (  map <string, set<string>> map_passed)

{
    for (auto pair : map_passed)
    {
        cout << pair.first << " : ";
        for (auto element : pair.second)
        {
            cout << element << ", ";
        }
        cout << "\n";
    }
}




int main()
{
    map <string, set<string> > map_sets = {

        {"Server One", {"Devin","Luke", "Abe"}},
        {"Server Two", {"Noah", "Nick"}},
        {"Server Three", {"Jimmy"}}
        
        };

    print_map(map_sets);

}
```
Output 

```cpp
Server One : Abe, Devin, Luke, 
Server Three : Jimmy, 
Server Two : Nick, Noah, 
```


## More Iterators over maps


```cpp
#include<iostream>
using std::cout; using std::endl;
#include<string>
using std::string;
#include <vector>
using std::vector;
#include<utility>
using std::pair; using std::make_pair;
#include<sstream>
using std::ostringstream;
#include<map>
using std::map;
#include<set>
using std::set;

template < typename K, typename V >

void print_map ( map <K, V>& map_passed)

{

    for ( auto x : map_passed)
    {
        cout << x.first << " : " << x.second << endl;
    }
        

}

int main()
{
    map <string,string > map_1 = {

        {"Server One", "Devin"},
        {"Server Two", "Noah"},
        {"Server Three", "Jimmy"}
    };

    map <int,string > map_2 = {

        { 1, "Devin"},
        { 2, "Noah"},
        { 3, "Jimmy"}
    };

    
    cout << "Print Map 1: " << endl; 
    print_map(map_1);

    cout << " Print Map 2: " << endl;
    print_map(map_2);
}
```

Output

```cpp
Print Map 1: 
Server One : Devin
Server Three : Jimmy
Server Two : Noah
Print Map 2: 
1 : Devin
2 : Noah
3 : Jimmy

```
