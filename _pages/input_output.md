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

