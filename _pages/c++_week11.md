---
layout: archive
permalink: /C++/c++_week11
title: "C++ Week 11 Stuff (extra)"
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

## Const in C++

* Can't change a *const* variable

```cpp
#include<iostream>
#include <string>

using std::cout;
using std::endl;

int main() {

    const int max_age = 90;

    // max_age = 23;  // Can't change a const variable

    cout << max_age << endl;
}
```
**Output:**

```cpp
90
```

What about with *pointers*?







### Const with Class and Methods


```cpp

#include<iostream>
#include <string>

using std::cout;
using std::endl;

class Entity
{
    private:
        int m_X, m_Y;
        int var;
    public:
        int GetX() const // promises not to touch anything in the function
        {
            return m_X;
        }
      
        void SetX(int x)
        {
            m_X = x;
        }
};

void PrintEntity(const Entity& e)
{
    cout << e.GetX() << endl;
}

int main(){
    
    Entity e;
    e.SetX(23);

    PrintEntity(e);

}

// Make sure to add const to method if it's not suppose to modify the class

```

**Output:**

```cpp
23
```


**Mutable Keyword**

```cpp

#include<iostream>
#include <string>

using std::cout;
using std::endl;

class Entity
{
    private:
        int m_X, m_Y;
        mutable int var;   // can modify 
    public:
        int GetX() const // promises not to touch anything in the function
        {
            var = 2;   // we can modify it 
            return m_X;
        }
        int GetX()
        {
            return m_X;
        }


        void SetX(int x)
        {
            m_X = x;
        }
};

void PrintEntity(const Entity& e)
{
    cout << e.GetX() << endl;
}

int main(){
    
    Entity e;

    e.SetX(23);

    PrintEntity(e);

}
```

**Output:**

```cpp
23
```
