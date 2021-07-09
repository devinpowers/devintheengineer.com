---
layout: archive
permalink: /C++/C++_Labs/Lab9
title: "Lab 9 C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

**Header File (vector.h)**

```cpp
#ifndef VECTOR_H
#define VECTOR_H

#include<string>
using std::string;

struct MathVector{
  // data members, default public
  long x=0;
  long y=0;

  // 2 constructors
  // =default uses default values of data members (above).
  // no other work required. You're welcome!
  MathVector()=default;
  // you must write
  MathVector(long, long);

  // 4 function members you must write
  MathVector add(const MathVector&);
  MathVector mult(long);
  long mult(const MathVector&);
  double magnitude();
};

// a function! You must write
string vec_to_str(const MathVector&);

#endif
```

**Vector Functions File (vector.cpp)**


```cpp
#include<string>
#include<sstream>
#include<cmath>
using std::string;
using std::ostringstream;

#include "vector.h"

// Constructor for values
MathVector::MathVector(long x_value, long y_value){
	x = x_value;
	y = y_value;
}

// Add Vector (overload the add)
MathVector MathVector::add(const MathVector & other_vec){
	return(MathVector(x+other_vec.x,y+other_vec.y));
}

// Multiply Vector by scalars (overload multiply)
MathVector MathVector::mult(long scalar){
	return MathVector(x*scalar,y*scalar);
}

// Multiply Vector by another Vector
long MathVector::mult(const MathVector & vec){
	x*=vec.x;
	y*=vec.y;
	return x+y;
}

// Magnitude of a vector using Pythagorean Theorem
double MathVector::magnitude(){
	return(sqrt((x*x)+(y*y)));
}

// prints out the vector
string vec_to_str(const MathVector& v){
	ostringstream oss;
	oss << v.x << ":" << v.y;
	return oss.str();
}
```


Let's now have a main file to run

**Main File (main.cpp)**

```cpp
#include<string>
using std::string;
#include<iostream>
using std::endl;
using std::cout;

#include "lab09_vector.h"

int main(){

    MathVector v1;
    MathVector v2(3,2);
    MathVector v3(10,12);
    MathVector v4(9,2);
    MathVector v5(18,7);

    long a = 3;

    // Using the addition function to add two vectors
    v1 = v3.add(v2);
    cout << vec_to_str(v1) << endl;


    // Multiply Vector by a scaler

    v1 = v5.mult(a);

    cout << "Multiply by scalar output: " << vec_to_str(v1) << endl;


    cout <<vec_to_str(v3) << endl;

    // Multiply Vector by another Vector
    cout << v2.mult(v3) << endl;
    // Magnitude
    cout << v2.magnitude() << endl;

    // Vector to String
    cout << vec_to_str(v3) << endl;

}
```

**Output from the main.cpp File**

```cpp
Running the add vector functions 
13:14
Running the Multiply by scalar vector functions 
Multiply by scalar output: 54:21
10:12
Running the Multiply by andother Vector Function
54
using the magnitude function !!!
38.4187
10:12
```
