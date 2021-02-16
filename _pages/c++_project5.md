---
layout: archive
permalink: /C++/c++_project5
title: "Project 5 in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

Project 5 is Working on a 4-Square Cipher Using Strings and Functions in C++

File Directory:

1. functions.cpp
2. main.cpp
3. functions.h


Here is the functions.cpp file!

```cpp
#include<iostream>
using std::cout; using std::cin; using std::endl; using std::boolalpha;
#include<string>
using std::string; using std::to_string; using std::tolower;
#include<cmath>
#include <locale>
using std::tolower;


const string alphabet = "abcdefghijklmnoprstuvwxyz"; //without 'q'


string clean_string (string s)  // Function for "Cleaning the String!!"
{
    string clean_string = "";

    for ( int i = 0; i < s.length(); i++)
    {
        if (s[i] != ' ')
        {          
            clean_string += tolower(s[i]); // lowers and cleans string ifthere is a space!
        }
    }
    return clean_string;


}

string create_encoding(string key){

    string keyword = ""; // string that were returning 


    for (auto character : key) {

        if ( keyword.find(character) == -1)
        {
            keyword += character;
        }
    }

    // need to add the rest of the alphabet to the end!

    for (auto character : alphabet){

        if ( keyword.find(character) == -1 ){

            keyword += character;
        }
    }
    return keyword;

}

string encode_digraph(string dg, string block1, string block2){
    string result;

    /*
        string dg is a pair of letters passed to our function hre
        Example:  "he" returns "fy"

    */

    char first_letter = dg[0];
    char second_letter = dg[1];

        /*  Location information:
        row = index/5 (integer division)
        col = index %5
        index = row * 5 + col */
    

    int first_location = alphabet.find(first_letter);
    int first_row = first_location/5;
    int first_col = first_location%5;

    int second_location = alphabet.find(second_letter);
    int second_row = second_location/5;
    int second_col = second_location%5;

    //get new indexes from blocks
    int first_new_index = first_row * 5 + second_col;
    int second_new_index = second_row * 5 + first_col;


    result += block1[first_new_index];
    result += block2[second_new_index];

    return result;

}

string encode(string msg, string key1, string key2){

    string block1;
    string block2;
    string encode_message;
    // Lets clean the msg first

    string msg_clean;

    msg_clean = clean_string(msg);

    // send key1 and key2 to create_encoding

    block1 = create_encoding(key1);
    block2 = create_encoding(key2);


    if (msg_clean.length() % 2 != 0)
        {
            msg_clean += "x";
        }


    for (int i = 0; i < msg_clean.length(); i++)
    {
        // send to encode_digraph

        cout << "MSG CLEAN PAIR: " << msg_clean.substr(i,2) << endl;

        encode_message += encode_digraph( msg_clean.substr(i,2), block1, block2) ;

        i++; // makes sure we skip iteration so we dont repeat a value
    }

    return encode_message;


}

string decode_digraph(string dg, string block1, string block2)
{
    string results;

    char first_letter = dg[0];
    char second_letter = dg[1];
    // return index from blocks
    int index_1 = block1.find(first_letter);
    int index_2 = block2.find(second_letter);
    
    int first_row = index_1/5;
    int first_column = index_2 %5;

    int second_row = index_2/5;
    int second_column = index_1 %5;


    int first_location_index = (first_row * 5) + first_column;

    int second_location_index = (second_row * 5) + second_column;

    results += alphabet[first_location_index];
    results += alphabet[second_location_index];

    return results;

}


string decode (string msg, string key1, string key2)
{
    string result;

    // take 2 keywords and create_encoding so I can pass them to our decode_digraph functionm

    string block1 = create_encoding(key1);
    string block2 = create_encoding(key2);

    if (msg.length() % 2 != 0 )
    {
        msg += "x";
    }

    for (int a = 0; a < msg.length(); a++ )
    {

        result += decode_digraph(msg.substr(a,2),block1, block2);

        a++; // make sure we iteration by 2, so we don't repeat a value

    }

    return result;

}

```


main.cpp file

```python
#include<iostream>
using std::cout; using std::cin; using std::endl; using std::boolalpha;
#include<string>
using std::string; using std::to_string; using std::tolower;
#include<cmath>
#include <locale>
using std::tolower;
#include "functions.h"

int main(){

    //here is some function testing, not included in mimir submission

    //clean string
    string s = "Hello World I love C plus plus"; 
    cout << "The orginal Message : " << s << endl;
    cout << endl;
    /*
    string clean = clean_string(s);
    cout << clean << endl;
    */

    //create encoding
    
    //string result = create_encoding("example");
    /*
    // encode_digraph
    string first_keyword = create_encoding("example");
    string second_keyword = create_encoding("keyword");
    string result = encode_digraph("he", first_keyword, second_keyword);
    cout << result << endl;

    */

    /*
    // decode_digraph
    string first_keyword = create_encoding("example");
    string second_keyword = create_encoding("keyword");
    string result = decode_digraph("fy", first_keyword, second_keyword);
    cout << result << endl; 

    */


    string first_keyword = create_encoding("example");
    string second_keyword = create_encoding("keyword");

    string result = encode(s,first_keyword,second_keyword);

    cout << "Encode: " << result << endl;

    cout << endl;

    //now lets decode out result

    string decode_msg = "fyhghzhsjebigzaoofrsofrs";

    string result2 = decode(decode_msg, first_keyword, second_keyword);
    cout << "Decode: " <<result2 << endl;
    

    return 0;
}


```

Some output:

```python
The orginal Message : Hello World I love C plus plus

Encode: fyhghzhsjebigzaoofrsofrs

Decode: helloworldilovecplusplus

```


The header file - functions.h

```python
#ifndef PROJ05_FOURSQUARE
#define PROJ05_FOURSQUARE

#include<iostream>
using std::cout; using std::cin; using std::endl; using std::boolalpha;
#include<string>
using std::string; using std::to_string; using std::tolower;
#include<cmath>
#include <locale>
using std::tolower;

string clean_string(string s);
string create_encoding(string key);
string encode_digraph(string dg, string block1, string block2);
string decode_digraph(string dg, string block1, string block2);
string encode(string msg, string key1, string key2);
string decode(string msg, string key1, string key2);

#endif


```
