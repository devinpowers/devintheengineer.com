---
layout: archive
permalink: /C++/functions_cpp
title: "Working with Functions in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---




Multidimensional Array

print with nested for loop


    #include <iostream>


    using namespace std;


    int main()
    {
        int grades[][3] = {{1, 2, 3},{4, 5, 6}, {7, 8, 9}};

        for(int r = 0; r < 3; r++)
        {
            for( int c =0; c <3; c++)
            {
                cout << grades[r][c] << "\t";
            }
            cout << "\n";
        }

        
        
        return 0;
    }




Nested Vectors



    #include <iostream>
    #include <vector>

    using namespace std;


    int main()
    {   
        vector <vector<int>> grades =
        {
            {1, 2, 3},
            {4, 5, 6},
            {7, 8, 9}
            
        };


        for(int r = 0; r < 3; r++)
        {
            for( int c =0; c <3; c++)
            {
                cout << grades[r][c] << "\t";
            }
            cout << "\n";
        }

        
        
        return 0;
    }

