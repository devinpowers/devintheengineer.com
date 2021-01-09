---
layout: archive
permalink: /C++/c++_project6
title: "Project 5 in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---


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

    vector<long> gen_nstep_vector(long limit, long nstep)
    {
        // pass in a nstep
        
    }


    int main(){

        cout << "Prac" << endl;
        // pass vector of long to vec_2_str

        vector<long> v{1,1,2,3,5,8,13,21,34,55,89,144,233,377,610};

        cout << vec_2_str(v) << endl;


    }