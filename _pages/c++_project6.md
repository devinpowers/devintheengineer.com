---
layout: archive
permalink: /C++/c++_project6
title: "Project 6 in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---



Function 1
```cpp
#include<iostream>
using std::cout; using std::cin; using std::endl;
#include<vector>
using std::vector;
#include<string>
using std::string;

#include<sstream>
using std::ostringstream;



string vec_2_str ( const vector<long>& v)
{
    string string_returned;
    ostringstream oss;

    for(auto iter = v.cbegin(); iter != v.cend(); ++iter){

        oss << *iter << ", ";
    }
    string_returned = oss.str();
    return string_returned.substr(0, string_returned.size() - 2);
    

    // loop thru the vector and turn it into one big string for all the happy kids
    //"Each element in the string is "
}


int main(){

    cout << "Prac" << endl;
    // pass vector of long to vec_2_str

    vector<long> v{1,1,2,3,5,8,13,21,34,55,89,144,233,377,610};

    cout << vec_2_str(v) << endl;


}
```

Function 2
```cpp
#include<iostream>
using std::cout; using std::cin; using std::endl;
#include<vector>
using std::vector;
#include<string>
using std::string;


void print_vector (vector<long> vector)
{
    for (int i = 0; i < vector.size(); i++)
    {
        cout << vector[i] << "\t";
    }
}

// Function 2:
vector <long> gen_nstep_vector (long limit, long nstep)
{
    vector <long> vec{1,1}; // initial vector with 2 seed values 

    long n_element = 0;

    int adjust_nstep = nstep - 2;

    for ( int x = 1; x <= adjust_nstep; x++)
    {
    vec.push_back(vec.back()*2);
    }

    // finish up adding rest of the values to the Vector vec 

    while (n_element <= limit )
    {
        for (int n = vec.size() - nstep; n < vec.size(); n++ )
        {
            n_element += vec[n];
        }
        if (n_element <= limit)
        {
            //add to vec
            vec.push_back(n_element);
            //reset n_element
            n_element = 0;
        }
    }
    return vec;
}



int main(){

    vector <long> vector2; 
    

    vector2 = gen_nstep_vector(200, 3);

    //can we print our return vector?

    print_vector(vector2);


    
}
```


Function 3

```cpp
#include<iostream>
using std::cout; using std::cin; using std::endl;
#include<vector>
using std::vector; using std::
#include<string>
using std::string;


vector <long> gen_nstep_vector (long limit, long nstep)
{
    vector <long> vec{1,1}; // initial vector with 2 seed values 

    long n_element = 0;

    int adjust_nstep = nstep - 2;

    for ( int x = 1; x <= adjust_nstep; x++)
    {
    vec.push_back(vec.back()*2);
    }

    // finish up adding rest of the values to the Vector vec 

    while (n_element <= limit )
    {
        for (int n = vec.size() - nstep; n < vec.size(); n++ )
        {
            n_element += vec[n];
        }
        if (n_element <= limit)
        {
            //add to vec
            vec.push_back(n_element);
            //reset n_element
            n_element = 0;
        }
    }
    return vec;
}


string num_to_nstep_coding ( long num, long nstep )
{
    
    string b_string = "00000000000";  // hardcoded??
    vector <long> vec;

    vec = gen_nstep_vector (10, nstep)
    
    for ( int x = vec.size(); x > 0; x-- ){

        if (vec[x] <= num)
        {
            num -= vec[x];
            cout << "Number: " << num << endl;
            b_string.insert(x,"1");

        }
    
    }



    return b_string;
}



int main() {

    //call function
    cout << "Code: " << num_to_nstep_coding(100,2) << endl;

    return 0;
}
```

Function 4

