---
layout: archive
permalink: /C++/c++_project4
title: "Project 4 in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---


This Project is using strings and working with Functions!!!!

Here we will encode a basic sequence of characters!!!

  #include<iostream>
  using std::cout; using std::cin; using std::endl;
  #include<iomanip>
  using std::setprecision;
  #include<string>
  using std::string;
  // global variable for count -> char code
  const string code = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";

  //
  // your functions here
  //
  string encode_sequence(string sequence, char encoder) {
    string result = "";
    if (sequence.length() <= 3) {
      //don't encode
      return sequence;
    }
    else {
      result.push_back(encoder);
      result.push_back(code.at(sequence.length() - 4));
        result.push_back(sequence.at(0));
    }
    return result;
  }

  int main()
  {
      string input; 
      char sep;

      cout << "Please Enter a String Sequence to Check: ";
      cin >> input;
      cout << "Please enter a character to seperate the code sequence: ";
      cin >> sep;

      cout << "The Encoded Sequence for the input: " << input << " is: " << encode_sequence (input, sep) << endl;
  }