---
layout: archive
permalink: /C++/c++_vectors
title: "Vectors "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

Outside of the string class, all the STL containers are templated! Therefore the types they hold must be specified at compile time

vector<T> are sequential containers, which means they have order to their elements

for vectors: #include <vector>

Whats good about vectors?

Well they have fast random access, only fast to add/delete at the end

Plus they're dynammic! Which allows them to grow or shrink in size while they're running

vector<T> : Definition

```cpp
vector <double> temp;
vector <int> points;
vector <string> names;
```

The <> describe the type that will be used with the class!

Since they're Dynamic they grow with size. Some methods that reflect this are:

- size(): which tells use how much the container presently holds
- capacity: how much it could hold before it has to grow and manage memory

#### Lets start making some vectors!!

A vector of size and capacity zero:

```cpp

vector<int> vec;

```
Create a vector of capacity 5, size 5, with each initialized to the default value (0 for int)
```cpp

vector<int> vec(5);
```



#### Different vector<T> member functions

```cpp
v.capacity()  // How much the Vector can store before growing

v.size()   // Vectors current size

v.empty() // Returns True is size == 0

v.reserve(n) // Will grow the capacity of the vector to n size

v.push_back(value) // Append value to end of the Vector

v.pop_back() // Removes the last value in the Vector (no return like python)

v.size() // is useful because v.size() - 1 is the index of the last element in v

v.empty() // is equivalent to v.size() == 0

v.reserve() // Increases the Capacity of the Vector

```

Examples Below:

```cpp
#include <iostream>
using std::cout;using std::endl;

#include <vector>
using std::vector;

int main() {

    vector<int> v = {1, 2, 3, 4, 5};

    cout << "v.front(): " << v.front() << endl;

    cout << "v.back(): " << v.back() << endl;

    v.clear();

    cout << "Lets use v.size():  " << v.size() << endl;
    v.assign(2,10);

    cout << "Lets check the front and back of our vector" << endl;
    
    cout << "v.front(): " << v.front() << endl;

    cout << "v.back(): " << v.back() << endl;
}
```
Output:
```cpp
v.front(): 1
v.back(): 5
Lets use v.size():  0
Lets check the front and back of our vector
v.front(): 10
v.back(): 10
```





### Access front and back of a Vector

```cpp
v.front() // the element at the front of the vector

v.back() // the element at the back of the vector

```


How would you retrieve the last element in a Vector?

```cpp

#include <iostream>

#include <vector>

using namespace std;

int main()

{
    vector<int> data = {1, 2, 3};

    data.push_back(4);

    cout <<data[data.size()-1] << endl;
    
}
```


### How do we add and delete a element in a vector?

Use push_back method, which is the primary way to add to a vector 

Use pop_back method to access a vector from the end, it doesnt return the value, it just removes it!

If we want to check the value, we use .back()



### Operators

How can we access data values inside our vector(s)? 

- We can use either [index] or .at(index)

But we cannot use them to "append", in order to append we need to use push_back(item)


```cpp

#include <iostream>
using std::cout;
using std::endl;
#include <vector>
using std::vector;

int main()

{
    vector<int> data = {1, 2, 3};

    cout << data[1] << endl;  //accessing items
    cout << data.at(1) << endl;   

}
```

```cpp
#include <iostream>
using std::cout;
using std::endl;
#include <vector>
using std::vector;

int main()

{
    vector<int> data = {1, 2, 3};

    data.push_back(4);

    cout << "First Index: " << data[0] << endl;
    cout << "Second Index: " << data[1] << endl;
    cout << "Third Index: " << data[2] << endl;
    cout << "Fourth index: " << data[3] << endl;

}
```
Output:
```cpp
First Index: 1
Second Index: 2
Third Index: 3
Fourth index: 4
```

We can also copy one vector into another vector!

- by using assignment v1 == v2

Example:

```cpp
#include <iostream>
using std::cout;
using std::endl;
#include <vector>
using std::vector;


void print_vector(vector<int> vec)
{
    for (auto element : vec)
    {
        cout << element << endl;
    }
    
}
int main()

{
    vector<int> data = {1, 2, 3};

    vector<int> data2;

    data2 = data;

    print_vector(data);

    print_vector(data2);
}

```

Output:
```cpp
1
2
3
1
2
3
```


For printing Vectors, we can't just normally print, we need to iterate through them!

![inserting an Image](/images/C++/vectors/Page4.jpg)

How do we pass Vectors to Functions?


```cpp

#include <iostream>
using std::cout;
using std::endl;
#include <vector>
using std::vector;


void print_vector(vector<int> data)
{
    for (int i = 0; i < data.size(); i++ )
    {
        cout << data[i] << endl;

    }
}
int main()

{
    vector<int> data = {1, 2, 3};

    print_vector(data);
}

```
Output:

```cpp
1
2
3

```

Otherwise to Print the vector!

```cpp


#include <iostream>
using std::cout;
using std::endl;
#include <vector>
using std::vector;


void print_vector(vector<int> vec)
{
    for (auto element : vec)
    {
        cout << element << ", ";
    }
    cout << endl;
}
int main()

{
    vector<int> data = {1, 2, 3};

    print_vector(data);
}

```

Output:

```cpp
1, 2, 3, 
```





### Multidimensional Vectors (2-D)

![inserting an Image](/images/C++/vectors/Page5.jpg)

```cpp


#include <iostream>
using std::cout;
using std::endl;
#include <vector>
using std::vector;

int main()
{
    vector <vector<int>> grades =
    {
        {1,2,3},
        {4,5,6},
        {7,8,9}
    };

    for (int r = 0; r < 3; r++)
    {
        for ( int c = 0; c < 3; c++ )
        {
            cout << grades[r][c] << "\t";
        }
        cout << "\n";
    };  

}
```

Output

```cpp

1       2       3
4       5       6
7       8       9

```


### Range Based Loops


changing the vector using the & sign!
Example:

```cpp
#include <iostream>
using std::cout;
using std::endl;
#include <vector>
using std::vector;

int main()
{
    vector<int> my_ints { 1, 2, 3, 4, 5};

    for (auto element : my_ints){

        cout << element << " : ";
    }
    cout << endl;

    for (auto & x : my_ints){

        x += 2;
    }

    for (auto element : my_ints)
    {
        cout << element << " : ";
    }
    cout << endl;
   

}
```

Output:

```cpp
1 : 2 : 3 : 4 : 5 : 
3 : 4 : 5 : 6 : 7 :

```

