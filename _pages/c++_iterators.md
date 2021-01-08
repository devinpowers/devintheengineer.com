---
layout: archive
permalink: /C++/c++_iterators
title: "Iterators in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---


An example of using iterators, Vectors, and Functions together

    #include<iostream>
    using std::cout; using std::endl; 
    #include<vector>
    using std::vector;
    #include<string>
    using std::string;
    #include<sstream>
    using std::ostringstream;

    template<typename T>
    string vec_to_string(const vector<T>& v){
    ostringstream oss;
    for(auto iter=v.cbegin(); iter!=v.cend(); ++iter){
        oss << *iter << ", ";
        // *iter = *iter + 1; // can't, it's low-level const
    }
    string result = oss.str();

    return result.substr(0, result.size() - 2 );
    }

    template<typename T>
    vector<T> rev_vector(vector<T>& v){
    vector<T> result;
    for(auto iter=v.rbegin(); iter!=v.rend(); ++iter)
        result.push_back(*iter);

    return result;
    }
        

    int main (){
    vector<long> v{1,2,3,4,5,6,7,8,9,10};
    string s = "abcd1234";  

    cout << "initial:\n" << vec_to_string(v) << endl;
    
    //rev = rev_vector(v);

    auto rev = rev_vector(v);
    cout << "reversed vector\n" <<  vec_to_string(rev) << endl;

    }

