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

- For normal variables, memory is automatically allocated and deallocated, but for things like pointers -> int *p = new int[10], it's up to us as programmers to deallocate memory when no longer needed, if we don't then it causes memory leak.

- We can **manually perform** memory allocation 


### new and delete Keywords


**new**

```cpp
new type(init)
```
- the new operator denotes a request to allocate new memory of indicated type on Free Store (can optionally provide an init, not required)
- Return a *pointer* to the new memory

**Example of a pointer-variable**

```cpp
int *p = new int; // Request for memory with the new keyword
```

We can alocatre a block (an array) of memory

```cpp
int *p = new int[5] 
```

* This code above dynamically allocates memory for 5 integers continuously of type int and returns pointer to the first element in the sequence, which is assigned to p (a pointer).

```cpp
#include<iostream>
using std::cout; using std::endl; using std::cin;

// Dynamic Arrays

int main(){

  // Main purpose is to allocate memory size of allocation in Bytes

  int size;
  cout << "Please enter a Size of an Array: ";
  cin >> size;

  int * myArray = new int [size]; // size that we enter

  for (int i =0; i<size; i++)
  {
    cout << "Array[" << i << "]";
    cin >> myArray[i];
  }
  for (int i =0; i<size; i++)
  {
    // write out elements of our array
    cout << myArray[i] << "  ";
   
  }

}

```

**Output**

I wanted an Array or size 5, and then I input the following numbers: 6,9,7,3, and 12

```cpp
Please enter a Size of an Array: 5
Array[0]6
Array[1]9
Array[2]7
Array[3]3
Array[4]12
6  9  7  3  12 
```


**delete**

* Since it's our responsibity as a programmer to *deallocate* dynamically allocated memory, this is where we use the *delete* keyword

```cpp
delete pointer-variable; // release memory pointed by the pointer-variable
```
- Deletion of an object pointed to by the pointer, releases memory

Here is an example of deleting an array of *all* elements, the ptr points to the beginning of the memory array to be deleted

```cpp
delete [] ptr;
```
Lets deallocate the memory that we have allocated from the array:

```cpp
#include<iostream>
using std::cout; using std::endl; using std::cin;

// Dynamic Arrays

int main(){

  // Main purpose is to allocate memory size of allocation in Bytes

  int size;
  cout << "Please enter a Size of an Array: ";
  cin >> size;

  int * myArray = new int [size]; // size that we enter

  for (int i =0; i<size; i++)
  {
    cout << "Array[" << i << "]";
    cin >> myArray[i];
  }
  for (int i =0; i<size; i++)
  {
    // write out elements of our array
    cout << myArray[i] << "  ";
   
  }
  delete[] myArray; // delete the memory that we allocated for our array
  myArray = NULL; // point to nothing, good practice

}
```

**Note:** Each time you write new you must write delete 

**Growing Array Example**

```cpp
#include <iostream>
using std::cout; using std::endl;
#include <algorithm>
using std::copy;
#include <iterator>
using std::ostream_iterator;


void print_array(int * array, size_t size) {
    
    for (int i =0; i<size; i++)
    {
    // write out elements of our array
    cout << array[i] << "  ";
    }
    cout << endl;
    // Or
    // copy(array, array + size, ostream_iterator<int>(cout, " "));
}

void double_size(int * (&array), size_t & size) {
    // double the size of the array
    size_t new_size = size * 2; // Double Size
    int * array2 = new int[new_size]{};         // new Keyword Create new array
    copy(array, array + size, array2); // Copy elments of array1 to array2
    size = new_size;        // Update Size
    delete [] array;  // delete Keyword
    array = array2;         
}

int main() {
    const size_t size = 2;
    int * array = new int[size];
    array[0] = 9;
    array[1] = 7;
    cout << "Original Array: " << endl;
    print_array(array, size);

    size_t new_size = size + 1;
    int * array2 = new int[new_size]{};
    copy(array, array + size, array2); // Copy elements of array1 to array2

    // Never use array after this point, so delete
    delete [] array;

    cout << "Array after increasing the size by 1: " << endl;
    print_array(array2, new_size);
    cout << "Array after adding new element: " << endl;
    array2[2] = 3;
    print_array(array2, new_size);

    // Using Double function
    cout << "Double!" << endl;
    double_size(array2, new_size); 
    // Print out our doubled array:
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

![inserting an Image](/images/C++/arrays/array_point1.jpg)
![inserting an Image](/images/C++/arrays/array_point2.jpg)

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

* Let's make the array 1000! 

**Output**
```cpp
   10,    11,    12,    13,    14

lptr1:0
lptr2:1234567
MyClass default:l:0, i:0, s:default ctor
MyClass 3 param:l:123456, i:123, s:3param ctor
How big to make the array:1000
   10,    11,    12,    13,    14,    15,    16,    17,    18,    19
   20,    21,    22,    23,    24,    25,    26,    27,    28,    29
   30,    31,    32,    33,    34,    35,    36,    37,    38,    39
   40,    41,    42,    43,    44,    45,    46,    47,    48,    49
   50,    51,    52,    53,    54,    55,    56,    57,    58,    59
   60,    61,    62,    63,    64,    65,    66,    67,    68,    69
   70,    71,    72,    73,    74,    75,    76,    77,    78,    79
   80,    81,    82,    83,    84,    85,    86,    87,    88,    89
   90,    91,    92,    93,    94,    95,    96,    97,    98,    99
  100,   101,   102,   103,   104,   105,   106,   107,   108,   109
  110,   111,   112,   113,   114,   115,   116,   117,   118,   119
  120,   121,   122,   123,   124,   125,   126,   127,   128,   129
  130,   131,   132,   133,   134,   135,   136,   137,   138,   139
  140,   141,   142,   143,   144,   145,   146,   147,   148,   149
  150,   151,   152,   153,   154,   155,   156,   157,   158,   159
  160,   161,   162,   163,   164,   165,   166,   167,   168,   169
  170,   171,   172,   173,   174,   175,   176,   177,   178,   179
  180,   181,   182,   183,   184,   185,   186,   187,   188,   189
  190,   191,   192,   193,   194,   195,   196,   197,   198,   199
  200,   201,   202,   203,   204,   205,   206,   207,   208,   209
  210,   211,   212,   213,   214,   215,   216,   217,   218,   219
  220,   221,   222,   223,   224,   225,   226,   227,   228,   229
  230,   231,   232,   233,   234,   235,   236,   237,   238,   239
  240,   241,   242,   243,   244,   245,   246,   247,   248,   249
  250,   251,   252,   253,   254,   255,   256,   257,   258,   259
  260,   261,   262,   263,   264,   265,   266,   267,   268,   269
  270,   271,   272,   273,   274,   275,   276,   277,   278,   279
  280,   281,   282,   283,   284,   285,   286,   287,   288,   289
  290,   291,   292,   293,   294,   295,   296,   297,   298,   299
  300,   301,   302,   303,   304,   305,   306,   307,   308,   309
  310,   311,   312,   313,   314,   315,   316,   317,   318,   319
  320,   321,   322,   323,   324,   325,   326,   327,   328,   329
  330,   331,   332,   333,   334,   335,   336,   337,   338,   339
  340,   341,   342,   343,   344,   345,   346,   347,   348,   349
  350,   351,   352,   353,   354,   355,   356,   357,   358,   359
  360,   361,   362,   363,   364,   365,   366,   367,   368,   369
  370,   371,   372,   373,   374,   375,   376,   377,   378,   379
  380,   381,   382,   383,   384,   385,   386,   387,   388,   389
  390,   391,   392,   393,   394,   395,   396,   397,   398,   399
  400,   401,   402,   403,   404,   405,   406,   407,   408,   409
  410,   411,   412,   413,   414,   415,   416,   417,   418,   419
  420,   421,   422,   423,   424,   425,   426,   427,   428,   429
  430,   431,   432,   433,   434,   435,   436,   437,   438,   439
  440,   441,   442,   443,   444,   445,   446,   447,   448,   449
  450,   451,   452,   453,   454,   455,   456,   457,   458,   459
  460,   461,   462,   463,   464,   465,   466,   467,   468,   469
  470,   471,   472,   473,   474,   475,   476,   477,   478,   479
  480,   481,   482,   483,   484,   485,   486,   487,   488,   489
  490,   491,   492,   493,   494,   495,   496,   497,   498,   499
  500,   501,   502,   503,   504,   505,   506,   507,   508,   509
  510,   511,   512,   513,   514,   515,   516,   517,   518,   519
  520,   521,   522,   523,   524,   525,   526,   527,   528,   529
  530,   531,   532,   533,   534,   535,   536,   537,   538,   539
  540,   541,   542,   543,   544,   545,   546,   547,   548,   549
  550,   551,   552,   553,   554,   555,   556,   557,   558,   559
  560,   561,   562,   563,   564,   565,   566,   567,   568,   569
  570,   571,   572,   573,   574,   575,   576,   577,   578,   579
  580,   581,   582,   583,   584,   585,   586,   587,   588,   589
  590,   591,   592,   593,   594,   595,   596,   597,   598,   599
  600,   601,   602,   603,   604,   605,   606,   607,   608,   609
  610,   611,   612,   613,   614,   615,   616,   617,   618,   619
  620,   621,   622,   623,   624,   625,   626,   627,   628,   629
  630,   631,   632,   633,   634,   635,   636,   637,   638,   639
  640,   641,   642,   643,   644,   645,   646,   647,   648,   649
  650,   651,   652,   653,   654,   655,   656,   657,   658,   659
  660,   661,   662,   663,   664,   665,   666,   667,   668,   669
  670,   671,   672,   673,   674,   675,   676,   677,   678,   679
  680,   681,   682,   683,   684,   685,   686,   687,   688,   689
  690,   691,   692,   693,   694,   695,   696,   697,   698,   699
  700,   701,   702,   703,   704,   705,   706,   707,   708,   709
  710,   711,   712,   713,   714,   715,   716,   717,   718,   719
  720,   721,   722,   723,   724,   725,   726,   727,   728,   729
  730,   731,   732,   733,   734,   735,   736,   737,   738,   739
  740,   741,   742,   743,   744,   745,   746,   747,   748,   749
  750,   751,   752,   753,   754,   755,   756,   757,   758,   759
  760,   761,   762,   763,   764,   765,   766,   767,   768,   769
  770,   771,   772,   773,   774,   775,   776,   777,   778,   779
  780,   781,   782,   783,   784,   785,   786,   787,   788,   789
  790,   791,   792,   793,   794,   795,   796,   797,   798,   799
  800,   801,   802,   803,   804,   805,   806,   807,   808,   809
  810,   811,   812,   813,   814,   815,   816,   817,   818,   819
  820,   821,   822,   823,   824,   825,   826,   827,   828,   829
  830,   831,   832,   833,   834,   835,   836,   837,   838,   839
  840,   841,   842,   843,   844,   845,   846,   847,   848,   849
  850,   851,   852,   853,   854,   855,   856,   857,   858,   859
  860,   861,   862,   863,   864,   865,   866,   867,   868,   869
  870,   871,   872,   873,   874,   875,   876,   877,   878,   879
  880,   881,   882,   883,   884,   885,   886,   887,   888,   889
  890,   891,   892,   893,   894,   895,   896,   897,   898,   899
  900,   901,   902,   903,   904,   905,   906,   907,   908,   909
  910,   911,   912,   913,   914,   915,   916,   917,   918,   919
  920,   921,   922,   923,   924,   925,   926,   927,   928,   929
  930,   931,   932,   933,   934,   935,   936,   937,   938,   939
  940,   941,   942,   943,   944,   945,   946,   947,   948,   949
  950,   951,   952,   953,   954,   955,   956,   957,   958,   959
  960,   961,   962,   963,   964,   965,   966,   967,   968,   969
  970,   971,   972,   973,   974,   975,   976,   977,   978,   979
  980,   981,   982,   983,   984,   985,   986,   987,   988,   989
  990,   991,   992,   993,   994,   995,   996,   997,   998,   999
 1000,  1001,  1002,  1003,  1004,  1005,  1006,  1007,  1008,  1009

1:10
n-1:1009
Size:8
```

### Another Example

![inserting an Image](/images/C++/arrays/array_point3.jpg)

```cpp
#include<iostream>
using std::cout; using std::endl; using std::cin; using std::ostream;
#include<iomanip>
using std::setw;
#include<string>
using std::string;

void fill(int ary[], int size, int value)
{  // Fill Array with values
  for (int i=0; i<size; ++i)
  {
    ary[i] = value+i;
  }
}

ostream& dump (ostream& out, int ary[], int size, int width=5){
  //print array as a block
  for(int i=0; i < size; ++i){
    out << setw(width) << *(ary + i);    
    if (i%10 != 9 && i != size-1)
      out << ", ";
    else
      out << endl;
  }
  out << endl;
  return out;
}

int main (){
   // dynamic array
  int size;
  cout << "How Big to make the array:";
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

**Output:**

```cpp
How Big to make the array:100
   10,    11,    12,    13,    14,    15,    16,    17,    18,    19
   20,    21,    22,    23,    24,    25,    26,    27,    28,    29
   30,    31,    32,    33,    34,    35,    36,    37,    38,    39
   40,    41,    42,    43,    44,    45,    46,    47,    48,    49
   50,    51,    52,    53,    54,    55,    56,    57,    58,    59
   60,    61,    62,    63,    64,    65,    66,    67,    68,    69
   70,    71,    72,    73,    74,    75,    76,    77,    78,    79
   80,    81,    82,    83,    84,    85,    86,    87,    88,    89
   90,    91,    92,    93,    94,    95,    96,    97,    98,    99
  100,   101,   102,   103,   104,   105,   106,   107,   108,   109

1:10
n-1:109
Size:8
```


## Leaking Memory

* Memory leakage occurs in C++ when programmers allocates memory by using new keyword and forgets to deallocate the memory by using delete() function or delete[] operator. One of the most memory leakage occurs in C++ by using wrong delete operator. 

* It's on you to free/delete memory that you have acquired

* Can you avoid this? Yes by using STL containers

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