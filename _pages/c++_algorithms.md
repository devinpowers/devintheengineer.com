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


**The Key to Algorithms are iterators**, because they work with **any container of any type** 

- every algorithm somehow utilizes iterators to perform tasks!



# Non-modifying

### Accumulate

- accumulate is to gather together or acquire increasing number of quantity of

**Syntax 1:** This function will return the sum of all the values between the first and last in the container!

```cpp
accumulate(first.begin(), last.end(), sum);
```
Where: first and last are the elements of whatever container that needs to be added, and sum is the initial value of the sum.

**Syntax 2:** This function will return the sum of all the values between the first and last in the container! 
```cpp
accumulate(first.begin(), last.end(), sum, my_function);
```
Where my_function (of any task) is performed on elements between the first and last in the container!


![inserting an Image](/images/C++/algorithms/accum1.jpg)

Example using accumulate on a vector or integars and a string:

**Form 1**
```cpp
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
```
Output
```cpp
The accumulation of vector 'Vect' is: 22
Adding a string up: HellomynameisDevin!
```


![inserting an Image](/images/C++/algorithms/accum2.jpg)

**Form 2**
```cpp
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
```

Output:

```cpp
The Sum is: 26
The Product is: 288
The Difference is : -26
```

More on Accumulate Algorithm:
![inserting an Image](/images/C++/algorithms/accum3.jpg)


## Lambdas

- inline functions that can best be used for short snippets of code that are not going to be reused and are not worth naming!

Basic Lambda Syntax:

[Capture]  (Parameters) -> returnType { Body };

Where:

Capture: globals (varibles) used in the function

Parameters: Parameters of the function

{ Body }: the function body

returnType: (optional not required)

![inserting an Image](/images/C++/algorithms/lambdas.jpg)


**Lambdas Example**

```cpp
#include<iostream>
using std::cout; using std::endl; 
#include<vector>
using std::vector;
#include<numeric>
using std::accumulate;


int main()
{
    vector <int > v ={ 1,2,3,4,5,6};

    int sum;

    sum = accumulate(v.begin(), v.end(), 0, 

    [] (const int& total, const int& value){
        cout << "Total: " << total << endl;
        cout << "Value: " << value << endl;

        return total + value + 2;
    }
    );
   
   cout << "The Sum of x+2 is: " << sum << endl;

}
```

Output:
```cpp
Total: 0
Value: 1
Total: 3
Value: 2
Total: 7
Value: 3
Total: 12
Value: 4
Total: 18
Value: 5
Total: 25
Value: 6
The Sum of x+2 is: 33
```




### Find Algorithm

- more non-modifying algorithms

What does find() Algorithm do?

- it finds the first element in range and returns an iterator point to that position!!

![inserting an Image](/images/C++/algorithms/find.jpg)


```cpp
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
```

Output

```cpp

Original vector : 10 20 30 40
Element 40 found at position : 3 (counting from zero) 

```

### Using find_if Algorithm


![inserting an Image](/images/C++/algorithms/find_if.jpg)

```cpp
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
```

Output:

```cpp
The first odd value is: 55
```

### Search Algorithm

![inserting an Image](/images/C++/algorithms/search.jpg)

```cpp
#include<iostream>
using std::cout; using std::endl;
#include <vector> 
using std::vector;
#include <algorithm> 
using std::search;



int main () 
{
    vector<int> vec { 0, 5, 10, 20, 30, 40, 56};

    vector<int> vec2 {20,30};

     // Declaring an iterator for storing the returning pointer
    vector<int>::iterator it;

    it = search (vec.begin(),vec.end(), vec2.begin(), vec2.end());

    if (it != vec.end() )
    {
        cout << "Vec2 is present at index: " << (it - vec.begin()) << endl;
    }
    else
    {
        cout << "Vec2 is not present in vec" << endl;
    }
    
}
```

Output:

```cpp
Vec2 is present at index: 3
```


# Modifying Algorithms


### Copy Algorithm

- One of the most useful algorithms!

![inserting an Image](/images/C++/algorithms/copy.jpg)


```cpp
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
```


Output

```cpp
The new vector elements entered using copy() : 1 8 2 3 1 3 10 
```


## Special Iterators!

- The Issue with Copy algorithm is that it requires that our destination container is large enough to hold what were copying. Theres two special kinds of iterators that allow us to get around this issue.
    - Insert iterator
    - Stream iterator

### Insert Iterator

- Depends on the container, a vector works best when we insert at the back
- Lists, sets insert at a particular position


## back_inserter for copying a Vector

![inserting an Image](/images/C++/algorithms/back.jpg)


```cpp
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
```


### Stream Iterator (ostream_iterator)

![inserting an Image](/images/C++/algorithms/ostream.jpg)


```cpp
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
```

Output

```cpp
1,8,2,3,1,3,10,12,67,90,100,82,
```

```cpp
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
```

Output

```cpp
Hello my name is Devin 
```


## Transform Algorithm

- 2 forms (Unary and Binary Operation)

- transforms range
![inserting an Image](/images/C++/algorithms/transform1.jpg)



#### Unary Operation

```cpp
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

```

Output

```cpp
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
```


Another Example

![inserting an Image](/images/C++/algorithms/transform2.jpg)


```cpp
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
```


Output

```cpp
10, 11, 13, 14, 15, 
```


# Add some more Algorithms later....

#### Binary Operation




# Sorting Algorithms


### sort

- Sorts elements in range


The transform function takes the pointer to the starting and ending position of a single input string and to the starting position of the output string.