---
layout: archive
permalink: /C++/c++_vectors
title: "Vectors "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

![inserting an Image](/images/C++/vectors/page1.jpg)
![inserting an Image](/images/C++/vectors/page2.jpg)



Lets Create a Vector



    #include <iostream>

    #include <vector>

    using namespace std;

    int main()

    {
        vector<int> data = {1, 2, 3};

        data.push_back(4);

        cout << "First Index: " << data[0] << endl;
        cout << "Second Index: " << data[1] << endl;
        cout << "Third Index: " << data[2] << endl;
        cout << "Fourth index: " << data[3] << endl;

    }


How would you retrieve the last element in a Vector?



    #include <iostream>

    #include <vector>

    using namespace std;

    int main()

    {
        vector<int> data = {1, 2, 3};

        data.push_back(4);

        cout <<data[data.size()-1] << endl;
        
    }

![inserting an Image](/images/C++/vectors/page3.jpg)


How to Remove the last element in the Vector?
Lets remove 3!

    #include <iostream>

    #include <vector>

    using namespace std;

    int main()

    {
        vector<int> data = {1, 2, 3};

        data.pop_back();

        cout <<data[data.size()-1] << endl;
        
    }

![inserting an Image](/images/C++/vectors/page4.jpg)

How do we pass Vectors to Functions?



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




