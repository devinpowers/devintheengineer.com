---
layout: archive
permalink: /C++/c++_vectors
title: "Working with Functions in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

Vectors

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
