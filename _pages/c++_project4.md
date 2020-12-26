---
layout: archive
permalink: /C++/c++_project4
title: "Project 4 in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---


This Project is using strings and working with Functions!!!!

Here we will encode a basic sequence of characters


    #include<iostream>
    using std::cout;
    using std::cin;
    using std::endl;
    #include<iomanip>
    using std::setprecision;
    #include<string>
    using std::string;


    const string code = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";

    string encode_sequence(string sequence, char encoder) {
      string results = "";
      if (sequence.length() <= 3) {
        //don't encode
        return sequence;
      }
      else {
        results.push_back(encoder);                       // adds encoder to results string (:)
        results.push_back(code.at(sequence.length() - 4 ));  // Adds decimal reference from code string above ()
        results.push_back(sequence.at(0));
      }
      return results;
    }

    string encode ( string sequence, char encoder ){

        string final_encode = "";  // final answer

        string shorten_sequence = "";   // dynamic, will change

        for (int i = 0 ; i < sequence.length(); i++)
        {
            shorten_sequence += sequence[i];

            if (sequence[i] != sequence[i+1]){

                final_encode += encode_sequence( shorten_sequence, encoder);

                shorten_sequence = ""; // reset our shorten sequence variable to "" 
            }

        }
        return final_encode;

    }

    int main()
    {
        string sequence_check = "";
        char sep;
        int test;

        cout << "Please enter (1 or 2) to perform " << endl << "1. Encode a Sequence using one variable: " << endl << "2. Encode a Long sequence using multiple varibles: " << endl;

        cin >> test;

        switch (test)
        {
        case 1: {

            cout << "Please enter a Sequence to Check:  ";
            cin >> sequence_check;

            cout << "Please enter a character to sperate  the code Sequence: ";
            cin >> sep;

            cout << encode_sequence(sequence_check, sep) << endl;
        }
            break;
        
        case 2:
        {
          
            cout << "Please enter a Sequence to Check:  ";
            cin >> sequence_check;
            cout << "Please enter a character to sperate  the code Sequence: ";
            cin >> sep;

            cout << encode(sequence_check, sep) << endl;
        }
            break;
        }

        
    }