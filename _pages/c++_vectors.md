---
layout: archive
permalink: /C++/c++_vectors
title: "Vectors "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

![inserting an Image](/images/C++/vectors/Page1.jpg)
![inserting an Image](/images/C++/vectors/Page2.jpg)



Lets Create a Vector

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

![inserting an Image](/images/C++/vectors/Page3.jpg)


How to Remove the last element in the Vector?
Lets remove 3!

```cpp
#include <iostream>

#include <vector>

using namespace std;

int main()

{
    vector<int> data = {1, 2, 3};

    data.pop_back();

    cout <<data[data.size()-1] << endl;
    
}
```

![inserting an Image](/images/C++/vectors/Page4.jpg)

How do we pass Vectors to Functions?


```cpp
#include <iostream>

#include <vector>

using namespace std;

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

### Multidimensional Vectors

![inserting an Image](/images/C++/vectors/Page5.jpg)

```cpp
#include <iostream>
#include <vector>


using namespace std;

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