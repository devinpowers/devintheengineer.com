---
layout: archive
permalink: /C++/input_c++
title: "input and output c++ Concepts"
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

Input and Output in C++ Basics

Outputing anything using the cout


    #include <iostream>

    int main() {

    std::string name = "Devin";

    std::cout <<"My name is "<< name << std::endl;
    
    return 0;
    }

outputs: My name is Devin

How do you input into C++? 

You use cin



    #include <iostream>

    int main() {

    std::string name;

    std::cout << "Enter your name: ";

    std::cin >> name; //takes the input and stores it into our string we declared above

    std::cout <<"Your name is "<< name << std::endl;
    
    return 0;
    }


C++ can take Multiple Inputs


  #include <iostream>

  using namespace std;

  int main() {
      char a;
      int num;

      cout << "Enter a character and an integer: ";
      cin >> a >> num;

      cout << "Character: " << a << endl;
      cout << "Number: " << num << endl;

      return 0;
  }






