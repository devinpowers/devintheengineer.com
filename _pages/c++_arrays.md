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


### C-Style Array

* Heres the Syntax

```cpp
type array_name[capacity];
```
**type:** is any *type*
**array_name:** is an identifier
**capacity** is the number of slots (indexing starts at 0)
  - The size in memory of the array is the (type's size * capacity)


### Declaring an Array in C++


**Method 1:**

```cpp
int arr[4];
arr[0] = 20;
arr[1] = 30;
arr[2] = 40;
arr[3] = 50;
```

**Method 2:**

```cpp
int arr[] = {20, 30, 40, 50};
```

**Method 3:**

```cpp
int arr[4] = {20, 30, 40, 50};
```


### Accessing Array Elements