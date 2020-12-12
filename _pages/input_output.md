---
layout: archive
permalink: /C++/input_output
title: "Input and Output in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---


Creating a file to output to (.txt)



    #include <iostream>
    #include <fstream>


    using namespace std;

    int main()
    {
        ofstream file;

        file.open("file_name.txt");  

        file.close();

    }

Other way to Open/Create a file:


    #include <iostream>
    #include <fstream>


    using namespace std;

    int main()
    {
        ofstream file ("file_name.txt");
        file.close();

    }


Lets have an example of writing to a txt file we created and use a vector with a for loop

    #include <iostream>
    #include <fstream>
    #include <vector>

    using namespace std;

    int main()
    {
        ofstream file ("hello.txt"); 

        vector <string> names;

        names.push_back("Devin");
        names.push_back("Lebron");
        names.push_back("Kobe");
        names.push_back("Jordan");

        for (string name : names )
        {
            file << name << endl;

        }

    }
