---
layout: archive
permalink: /C++/c++_arrays
title: "C++ Arrays"
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

An **array** is a contiguous, fixed-size piece of memory
  * it cannot grow , cannot change size
  * It's a sequence of elements

* One BIG CHUNK of MEMORY

* Note that arryas are **not** C++ Objects

### C-Style Array

* Heres the Syntax

```cpp
type array_name[capacity];
```
**type:** is any *type*
**array_name:** is an identifier
**capacity** is the number of slots (indexing starts at 0)
  - The size in memory of the array is the (type's size * capacity)


**Size of Array**

```cpp
#include <iostream>
using std::cout;
using std::endl;

int main() {

   int guesses[] = {12, 43, 23, 56, 69};

   int size = sizeof(guesses);

   cout << "Size of array (Number of Bits): " << size << endl;

}
```

**Output:**

```cpp
Size of array (Number of Bits): 20
```

* 20 bits ( 5#'s taking up 4 bits each)


**Now how do we find the size of the array?**

```cpp

#include <iostream>
using std::cout;
using std::endl;

int main() {

   int guesses[] = {12, 43, 23, 56, 69};

   int size = sizeof(guesses)/ sizeof(int);

   cout << "Size of array: " << size << endl;

}
```

**Output:**

```cpp
Size of array: 5
```




### Declaring and Initializing an Array in C++


**Method 1:**

```cpp
#include <iostream>
using std::endl;
using std::cout;

int main() {

  int arr[4];
  arr[0] = 20;
  arr[1] = 30;
  arr[2] = 40;
  arr[3] = 50;
}
```
- Initialize elements starts with the *leftmost* element 0, the remaining elements are initialized to zero

**Method 2:**

```cpp
#include <iostream>
using std::endl;
using std::cout;

int main() {

  int arr[] = {20, 30, 40, 50};
}
```

**Method 3:**

```cpp
#include <iostream>
using std::endl;
using std::cout;

int main() {
  int arr[4] = {20, 30, 40, 50};
}
```

### Accessing Array Elements

- How to print an Array

**Method using a While Loop:**

```cpp
#include <iostream>
using std::endl;
using std::cout;

int main(){
   int arr[] = {20, 30, 40, 50};
   int n=0;
  
   while(n<=3){
      cout<<arr[n]<<endl;
      n++;
   }
}
```
**Output:**

```cpp
20
30
40
50
```

**Note:** Iterators *cannot* be used on primitive type arrays, *only* on collections!


**Method accessing the index**

```cpp
#include <iostream>
using std::endl;
using std::cout;

int main(){
   int arr[] = {20, 30, 40, 50};

   cout << arr[0] << endl;
   // change index
   arr[0] = 1000;
   cout << arr[0] << endl;
   cout << arr[1] << endl;
   cout << arr[2] << endl;
   cout << arr[3] << endl; 
}
```

**Output:**

```cpp
20
1000
30
40
50
```

* Cool we just changed the element at index 0 by accessing it!



**What if we changed the size of our array to 10?**

```cpp
#include <iostream>
using std::cout;
using std::endl;

int main() {

   int guesses[10] = {12, 43, 23, 56, 69};

   int size = sizeof(guesses)/ sizeof(int);

   for ( int i = 0; i < size; i++ )
   {
      cout << guesses[i] << "\t";
   }

}
```

**Output:**

```cpp
12      43      23      56      69      0       0       0       0       0 
```

* Notice how, even though we didn't configure 10 numbers (int) in our array with a size 10 array, we have extra 0's at the end 


### Different Operations on Arrays

- Subscript
  * Assignment
- Arithmetic

```cpp
#include <iostream>
using std::endl;
using std::cout;

int main(){

  int ary[2]; // Array of 2 ints
  int ary[0] = 23; // Assignment

  ary[1] = ary[0] + 3; // Arithmetic
}
```

**Note:** The compiler can also determine the size

**Type** is very important, each array needs a type so the size of memory requested can be calculated (number of elements * size of type)
  * Therefore each array can only hold elements of the *same* type (there is some ways around this tho...)



### Another Example of an Array

```cpp
#include<iostream>
using std::cout; using std::endl;

int main(){
  const size_t size = 5;
  int ary1[size]{8,5,6,7,4};
  char ary2[]{'a', 'b', 'c', 'd'};  // fixed size, 4 chars
  long ary3[size]{}; // 0 initialized, each element initialized!
  long ary4[size];  // uninitialized, no work done.

  cout << "Indexes of Various Arrays: " << endl;
  cout << "Index 0 of ary1:"<<ary1[0]<<endl;
  cout << "Index 0 of ary2:"<<ary2[0]<<endl;  
  cout << "Index 4 of ary3:"<<ary3[4]<<endl;
  cout << "Index 0 of ary4:"<<ary4[0]<<endl;     // ?? not initialized
  // cout << "Index 10 of ary1:"<<ary1[10] << endl; // ?? past end

  for(size_t i=0; i<size; ++i)
    cout << "Index"<<i<<", value:"<<ary1[i] << endl;;

  // range based for, OK, const value of size
  for (auto element : ary1)
    cout << "int element:"<<element<<", ";
  cout << endl;

  for(auto element : ary2)
    cout << "char element:"<<element<<", ";
  cout << endl;

  // subscript assignment OK
  ary3[0]=1234;
  for(size_t j=1; j<size; j++)
    ary3[j] = ary3[j-1] * 2;

  for (size_t j=0; j<size; j++)
    cout << "Index"<<j<<", value:"<<ary3[j] << endl;
}
```

**Output:**

```cpp
Index 0 of ary1:8
Index 0 of ary2:a
Index 4 of ary3:0
Index 0 of ary4:4543734386
Index0, value:8
Index1, value:5
Index2, value:6
Index3, value:7
Index4, value:4
int element:8, int element:5, int element:6, int element:7, int element:4, 
char element:a, char element:b, char element:c, char element:d, 
Index0, value:1234
Index1, value:2468
Index2, value:4936
Index3, value:9872
Index4, value:19744
```


### Advantages of Arrays in C++

1. Random Access of elemtns using the array index []
2. East access to all the elements
3. Traversal through the array is easy using a loop
4. Can easily Sort


### Disadvantages of Arrays in C++

1. Allows for a *fixed* number of elements, which has to be decided at the time of declaring and array

2. Insertion and deletion of elements can be costly


## Arrays and Pointers

* **NOTE** Arrays DO NOT remember their length when passed!

  * C++ is too sensitive to know the size of the arrya
  * If the compiler knows the size then it allows you to do things like for-each loops
  * If the compiler cannot know the size, it treats it like a pointer

* Arrays and Pointers are two *different things*

* Arrays have no methods, C++ does provide functions *begin()* and *end()* (if the compiler knows the array size) (they're functions NOT methods)
  * You can treat a pointer as an iterator if you want to run generic algorithms on an arry

*  no begin or end method, but an **array pointer** IS an iterator

**Example using Pointer to iterate/print Array:**

```cpp
#include <iostream>
using std::cout;
using std::endl;

int main()
{
    const size_t size = 5;

    int arr[size]{8,5,6,7,4};
   
    for (int *i = arr; i < (arr+size); i++)
    {
        cout << "Element: " << *i << ", ";
    }
    cout << endl; // end line
}
```

**Output:**

```cpp
Element: 8, Element: 5, Element: 6, Element: 7, Element: 4, 
```



**Example using  sort() and copy() algorithms on the Array:**

😂

```cpp

#include <iostream>
using std::cout;
using std::endl;
#include<algorithm>
using std::copy; using std::sort; using std::transform;
#include<iterator>
using std::ostream_iterator; using std::begin; using std::end;

int main()
{
    const size_t size = 5;

    int arr[size]{8,5,6,7,4};

    int *pointer_array_front = arr;          
    int *pointer_array_back = arr+size;

    cout << "Front Pointer: " << pointer_array_front << endl;
    cout << "Front Value: " << *pointer_array_front << endl;
    cout << "1 Past End Pointer: " << pointer_array_back << endl;

    // Array Pointer is an iterator

    sort(pointer_array_front, pointer_array_back);

    copy(pointer_array_front, pointer_array_back, ostream_iterator<int>(cout, ", "));

    cout << endl; 
}
```

**Output:**
```cpp
Front Pointer: 0x7ffee8ad85d0
Front Value: 8
1 Past End Pointer: 0x7ffee8ad85e4
4, 5, 6, 7, 8, 
```



**Example using begin() and end() functions and sort(), copy(), and transform algorithms on the Array:**


## Arrays and Functions


* There are **3 ways** to pass an array to a function, note that is's always a pointer or a reference and **NEVER** a copy



**First Way:**

- Pass array

```cpp
int sum(int ary[])
```
* [] indicates the parameter is an array
* It's a pointer!
* No size info on the array, size is **required** to be passed 


**Second Way (directly as a pointer)**



**Third Way**


### Multidimensional Arrays




## Dynamic Memory

* Videos on

## Leaking Memory

* Videos on
