---
layout: archive
permalink: /C++/c++_arrays
title: "C++ Arrays"
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

An **array** is a contiguous, fixed-size piece of memory
  * it cannot grow , cannot change size (set it when you're declaring it !!)
  * It's a sequence of elements

* One BIG CHUNK of MEMORY

* Note that arrays are **not** C++ Objects

![inserting an Image](/images/C++/arrays/array_c++.jpg)

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


**Now how do we find the size of the array? (number of element)**

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

* different ways to declare and initialize 

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


# Arrays and Pointers

* **NOTE** Arrays *DO NOT remember* their length when passed!

  * C++ is too sensitive to know the size of the array
  * If the compiler knows the size then it allows you to do things like for-each loops
  * If the compiler cannot know the size, it treats it like a pointer

* Arrays and Pointers are two *different things*

* Arrays have no methods, C++ does provide functions *begin()* and *end()* (if the compiler knows the array size) (they're **functions** NOT methods)
  * You can treat a pointer as an iterator if you want to run generic algorithms on an array

*  no begin or end method, but an **array pointer** IS an iterator

![inserting an Image](/images/C++/arrays/array_point1.jpg)


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

* Note that the *Front Pointer* points to the first index in the array, while the *Back Pointer* points to one index past the last. Hence in the following example image below:

* In this example we use the *sort()* and the *copy* algorithm on the array to 1. Sort the array in-order and 2. To *copy& and print the sorted array out.

![inserting an Image](/images/C++/arrays/array_point2.jpg)

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
    cout << "One Past End Pointer: " << pointer_array_back << endl;
    cout << "Back Value: " << *pointer_array_back << endl;

    // Array Pointer is an iterator

    sort(pointer_array_front, pointer_array_back);

    copy(pointer_array_front, pointer_array_back, ostream_iterator<int>(cout, ", "));

    cout << endl; 
}
```

**Output:**
```cpp
Front Pointer: 0x7ffeedc695d0
Front Value: 8
One Past End Pointer: 0x7ffeedc695e4
Back Value: 32766
4, 5, 6, 7, 8, 
```

* We can see where the address and the value that the *Front Pointer* is pointing too
* The last back pointer value is some random number -> 32766



**Example using begin() and end() functions with the  transform algorithm on the Array:**

* **Note:** begin() and end() functions (NOT METHODS) do work if the complier knows the size of the array


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

    transform(begin(arr), end(arr), ostream_iterator<int>(cout, ", "), [] (int x) {return x*2;});

    cout << endl;
}
```

**Output:**

```cpp
16, 10, 12, 14, 8, 
```


# Arrays and Functions


* There are **3 ways** to pass an array to a function, note that is's always a pointer or a reference and **NEVER** a copy


**First Way:**

- Pass array, it's implicity a pointer 

Syntax:
```cpp
int sum(int arr[], int size)
```

* [] indicates the parameter is an array
* int size is the *size* of the array
* It's a pointer!

```cpp
#include<iostream>
using std::cout; using std::endl;
#include<sstream>
using std::ostringstream;
#include<string>
using std::string;


int sum (int arr[], int size){
  int sum = 0;

  for(int  i=0; i<size; i++){
    sum += arr[i]; 
  }
  return sum;
}


int main() 
{
  
  int arr[]{8,5,6,7,4};
  int size = sizeof(arr) / sizeof(int);

  cout << sum(arr, size) << endl;
}
```

**Output:**

```cpp
30
```

**Second Way (directly as a pointer)**

Syntax:
```cpp
int sum(int *arr, int size)
```

- Passed in as a pointer

```cpp
#include<iostream>
using std::cout; using std::endl;
#include<sstream>
using std::ostringstream;
#include<string>
using std::string;

int sum (int *arr, int size){
  int sum = 0;

  for(int  i=0; i<size; i++){
    sum += arr[i];  // Same thing
    // sum += *(arr+1);
  }
  return sum;
}


int main() 
{
  
  int arr[]{8,5,6,7,4};
  int size = sizeof(arr) / sizeof(int);

  cout << sum(arr, size) << endl;

}
```

**Output:**

```cpp
30
```


**Third Way**

* If you set the size (somehow) in the function call itself, then the compiler can figure out how to do things like for-each loop

```cpp
#include<iostream>
using std::cout; using std::endl;
#include<string>
using std::string;

int sum (const int (&arr)[5]){
  int sum = 0;

  for (auto &element : arr )
  {
      sum += element;
  }
  return sum;
}


int main() 
{
  
  int arr[]{8,5,6,7,4};
  cout << sum(arr) << endl;

}
```

**Output:**

```cpp
30
```

**Lets Template the Size, so we don't have to indicate it!:**

```cpp
#include<iostream>
using std::cout; using std::endl;
#include<string>
using std::string;

// let template deduce size, we don't have to say!!

template<typename Type, size_t Size>
int sum (const Type (&arr)[Size]){
  Type sum = 0;

  cout << "Sizeof array (template size) : " << sizeof(arr) << endl;
  for (auto element : arr )
  {
      sum += element;
  }
  return sum;
}


int main() 
{
  
  int arr[]{8,5,6,7,4,20,3,69,15};
  cout << sum(arr) << endl;

}
```

**Output:**

```cpp
Sizeof array (template size) : 36
137
```


### Multidimensional Arrays

**Example of an Multidimensional Array**

* Need a *nested for loop* to iterate through

```cpp
#include <iostream>
using std::cout;
using std::endl;

int main()
{
    int grades[][3] = 
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

**Output:**

```cpp
1       2       3
4       5       6
7       8       9
```


## Dynamic Memory

**Run Time vs Compile Time**

- Where compile time is known at the time of running the compiler to make an executable, while run time is known when the user *actually* runs the exectuable

- STL Objects are the best, they know how to get more memory during *runtime*( think vectors, maps, etc.), while things like arrays, fixed-size non-object -> they're fixed size at compile time


- We can manually to perform memory allocation 

#### new and delete Keywords

**new**

```cpp
new type(init)
```
- Allocate new memory of indicated type (can optionally provide an init, not required)
- Return a *pointer* to the new memory

**delete**

```cpp
delete ptr
```
- Deletion of an object pointed to by ptr

```cpp
delete [] ptr;
```

- Deletion of an array of *all* elements, the ptr points to the beginning of the memory array to be deleted

**Growing Array Example**

```cpp
#include <iostream>
#include <algorithm>
#include <iterator>

// Dynamic Memory


void print_array(int * array, size_t size) {
    std::copy(array, array + size, std::ostream_iterator<int>(std::cout, " "));
    std::cout << std::endl;
}

void double_size(int * (&array), size_t & size) {
    size_t new_size = size * 2;
    int * array2 = new int[new_size]{};         // new Keyword
    std::copy(array, array + size, array2);
    size = new_size;
    delete [] array;  // delete Keyword
    array = array2;
}

int main() {
    const size_t size = 2;
    int * array = new int[size];
    array[0] = 9;
    array[1] = 7;
    print_array(array, size);

    size_t new_size = size + 1;
    int * array2 = new int[new_size]{};
    std::copy(array, array + size, array2);

    // Never use array after this point
    delete [] array;

    print_array(array2, new_size);
    array2[2] = 3;
    print_array(array2, new_size);

    std::cout << "Double!" << std::endl;
    double_size(array2, new_size);
    print_array(array2, new_size);

    delete [] array2;
}
```

**Output:**

```cpp
9 7 
9 7 0 
9 7 3 
Double!
9 7 3 0 0 0
```

**Dynamic Array Example**

```cpp
#include<iostream>
using std::cout; using std::endl; using std::cin; using std::ostream;
#include<iomanip>
using std::setw;
#include<string>
using std::string;

class MyClass{
private:
  long long_;
  int int_;
  string str_;
public:
  MyClass(): long_(0), int_(0), str_("default ctor") {};
  MyClass(long l, int i, string s): long_(l), int_(i), str_(s) {}; 
  friend ostream& operator<<(ostream&, const MyClass&);
};



ostream& operator<<(ostream &out, const MyClass &c){
  out << "l:"<< c.long_ << ", i:" << c.int_ << ", s:" << c.str_;
  return out;
}

void fill(int *ary, size_t sz, int val){
  for (size_t i=0; i<sz; ++i)
    ary[i] = val+i;
}

// print array as a block
ostream& dump (ostream& out, int ary[], size_t sz, size_t width=5){
  for(size_t i=0; i < sz; ++i){
    out << setw(width) << *(ary + i);
    if (i%10 != 9 && i != sz-1)
      out << ", ";
    else
      out << endl;
  }
  out << endl;
  return out;
}
	
int main (){
  size_t sz=5;
  int ary1[sz];
  fill(ary1, sz, 10);
  dump(cout, ary1, sz);  

  // basic new
  long *lptr1, *lptr2;
  MyClass *mcptr, *mcptr2;

  lptr1 = new long;   // uninitialized
  lptr2 = new long{1234567}; // initialized
  mcptr = new MyClass; // default constructor
  mcptr2 = new MyClass(123456, 123, "3param ctor");

  cout << "lptr1:"<< *lptr1 << endl;  
  cout << "lptr2:"<< *lptr2 << endl;
  cout << "MyClass default:"<< *mcptr << endl;
  cout << "MyClass 3 param:"<< *mcptr2 << endl;

  // delete them when done
  delete lptr1;
  delete lptr2;  
  delete mcptr;
  delete mcptr2;

  // dynamic array
  size_t size;
  cout << "How big to make the array:";
  cin >> size;
  // not an array type, only a pointer
  // long *ary = new long[size];   // not initialized
  int *ary = new int[size]{}; // initialize all!
  fill(ary, size, 10);
  dump(cout, ary, size);

  cout << "1:"<<ary[0]<<endl;
  cout << "n-1:"<<ary[size-1]<<endl;
  cout << "Size:"<<sizeof(ary)<<endl; //pointer,not array type!

  // if you make it, you must delete it. Note []
  delete [] ary;
}
```

**Output**

```cpp
   10,    11,    12,    13,    14

lptr1:0
lptr2:1234567
MyClass default:l:0, i:0, s:default ctor
MyClass 3 param:l:123456, i:123, s:3param ctor
How big to make the array:20
   10,    11,    12,    13,    14,    15,    16,    17,    18,    19
   20,    21,    22,    23,    24,    25,    26,    27,    28,    29

1:10
n-1:29
Size:8
```


## Leaking Memory

* Memory leakage occurs in C++ when programmers allocates memory by using new keyword and forgets to deallocate the memory by using delete() function or delete[] operator. One of the most memory leakage occurs in C++ by using wrong delete operator. 

**Leaking Memory Example**

```cpp
#include<cstddef>
using std::size_t;
#include<iostream>
using std::cout; using std::endl; using std::cin;
#include<string>
using std::string;

int main (){
  int reps = 1024;
  const size_t chunk = 1048576; // be careful!!!
  long last;
  string s;

  for(int i=0;i<reps;i++){
    long *ary = new long[chunk]; // leak memory here each iteration
    ary[0] = 1;
    for (size_t j=1; j < chunk; ++j)
      ary[j] = ary[j-1] + 1;
    last = ary[chunk-1];
  }
  cout << last << endl;
  cout << "A string please:";
  cin >> s;
}
```

**Output:**

```cpp

```



**Last Example**

```cpp
#include<iostream>
using std::cout; using std::endl; using std::ostream;

long* fn1(size_t sz, long start, long inc ){
  auto ptr =  new long[sz];
  ptr[0]=start;
  for(size_t i=1; i<sz; i++)
    ptr[i]=ptr[i-1]+inc;
  return ptr;
}

ostream& print(ostream& out, long ary[], size_t sz){
  for(size_t i=0;i<sz;i++){
    out << ary[i];
    if (i < sz-1)
      out << ", ";
  }
  out << endl;
  return out;
}

int main (){
  long *ptr_l;
  // double *ptr_d;
  size_t sz=10;
  ptr_l = fn1(sz, 100, 10);
  cout << ptr_l << endl;
  print(cout, ptr_l, 10) << endl;  
  // leak without this, even though allocated in fn1
  delete [] ptr_l;
}
```

**Output**

```cpp
0x7f9177c05980
100, 110, 120, 130, 140, 150, 160, 170, 180, 190
```