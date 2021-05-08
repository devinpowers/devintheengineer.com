---
layout: archive
permalink: /C++/streams
title: " Streams in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

![inserting an Image](/images/C++/streams/Page1.jpg)
![inserting an Image](/images/C++/streams/Page2.jpg)
![inserting an Image](/images/C++/streams/Page3.jpg)
![inserting an Image](/images/C++/streams/Page4.jpg)
![inserting an Image](/images/C++/streams/Page5.jpg)
![inserting an Image](/images/C++/streams/Page6.jpg)
![inserting an Image](/images/C++/streams/Page7.jpg)
![inserting an Image](/images/C++/streams/Page8.jpg)
![inserting an Image](/images/C++/streams/Page9.jpg)
![inserting an Image](/images/C++/streams/Page10.jpg)
![inserting an Image](/images/C++/streams/Page11.jpg)

## Examples

### Reading txt file using fstream

```cpp

#include <iostream>
#include <string>
#include <utility>
#include <fstream>
#include <algorithm>
using std::string; 
using std::ifstream; using std::cout; using std::endl; using std::to_string;
using std::invalid_argument;

// create custom data struture here



void ParseFileData(const string &fname){


    ifstream inFile(fname);   //ifstream is the txt file object?

    bool result;

    //error handling for no file found
    if(!inFile){
        throw std::invalid_argument("invalid argument DUDE!!");
    }

    if (inFile.is_open()){

        string username, command, server_name;

        while (inFile >> username >> command >> server_name ){ //each name/command one at a time

            if ( command != "join" && command != "leaving")
            {
                cout << "ERRORRRRR!!!" << endl;
            }
            // else tho
            if ( command == "join")
            {
                cout << "Joining:  " << username << " : " << server_name << endl;
                //result = //send to add connection
            }
            else if (command == "leaving"){

                cout << "Leaving " << username << " : " << server_name << endl;
            }

        }
        
    }
    inFile.close(); // close file

}

int main(){

    // send file to our function
    ParseFileData("file.txt");
}
```

**file.txt**

```cpp
devin join server1
kobe join server2
lebron join server1
kobe join server2
paul leaving server3
ryan leaving server3
tommas join server1
```
**Output:**

```cpp
Joining:  devin : server1
Joining:  kobe : server2
Joining:  lebron : server1
Joining:  kobe : server2
Leaving paul : server3
Leaving ryan : server3
Joining:  tommas : server1
```
