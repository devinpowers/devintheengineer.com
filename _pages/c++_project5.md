---
layout: archive
permalink: /C++/c++_project5
title: "Project 5 in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

Project 5 is Working on a 4-Square Cipher Using Strings and Functions in C++


    #include <iostream>
    using std::cout; using std::cin; using std::endl;
    #include<string>
    using std::string;



    const string alphabet = "abcdefghijklmnoprstuvwxyz"; //without 'q'

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

        // send key1 and key2 to create_encoding

        block1 = create_encoding(key1);
        block2 = create_encoding(key2);


        if (msg.length() % 2 != 0)
            {
                msg += "x";
            }


        for (int i = 0; i < msg.length(); i++)
        {
            // send to encode_digraph

            encode_message += encode_digraph( msg.substr(i,2), block1, block2) ;

            i++; // makes sure we skip iteration so we dont repeat a value
        }

        return encode_message;


    }




    int main() {


        cout << encode( "helloworld", "example", "keyword") <<endl;

    

    }
