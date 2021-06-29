---
layout: archive
permalink: /C++/c++_overloaded
title: "C++ Overloaded Operators"
author_profile: true

header:
  image: "/images/tower3.jpeg"

toc: true
toc_label: "Table of Contents" 
---


When we think of operators we have like *, <, >, + 

* Allow to define/change behavior in operator

* Should be **minimal!!!!**

```cpp
#include<iostream>

using std::cout;
using std::endl;


struct Vector2
{
    float x, y;

    Vector2(float x, float y ) : x(x), y(y) {} // constructor


    Vector2 Add(const Vector2& other) const
    {
        return Vector2( x + other.x, y + other.y);
    }
    
    Vector2 operator+(const Vector2& other) const // writing the operator
    {
        Add(other);
    }

    Vector2 Multiply (const Vector2& other) const
    {
        return Vector2(x * other.x, y * other.y);
    }

    

    
};

int main()
{
    Vector2 position(4.0f, 4.0f);
    Vector2 speed(0.5f, 1.5f);
    Vector2 powerup(1.1f, 1.1f);

    Vector2 result = position.Add(speed.Multiply(powerup));

    Vector2 result = position + speed; // * powerup;


}
```