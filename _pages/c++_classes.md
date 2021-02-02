---
layout: archive
permalink: /C++/c++_classes
title: " Classes in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---


## Basic Class 


Here is a basic Class

    #include <iostream>
    using std::cout; using std::endl;
    #include<string>
    using std::string;



    // represents Blueprint
    struct Employee{
        // inside the class we need to put attributes and behaviors
    public:
        string name;
        string company;
        int age;

        void Introduceyourself(){

            cout << "Hello my name is " << name << endl;
            cout << "I am "  << age << " years old." << endl;
            cout << "I work for " << company << endl;
        }

    };


    int main()
    {
        Employee employee1;
        employee1.name = "Devin";
        employee1.company = "ADAC";
        employee1.age = 100;
        
        employee1.Introduceyourself();


    }


Output

    Hello my name is Devin
    I am 100 years old.
    I work for ADAC



## constructors



    #include <iostream>
    using std::cout; using std::endl;
    #include<string>
    using std::string;



    // represents Blueprint
    struct Employee{
        // inside the class we need to put attributes and behaviors
    public:
        string Name;
        string Company;
        int Age;

        void Introduceyourself(){

            cout << "Hello my name is " << Name << endl;
            cout << "I am "  << Age << " years old." << endl;
            cout << "I work for " << Company << endl;
        }

        Employee(string name, string company, int age){

            Name = name;
            Company = company;
            Age = age;   
        }

    };


    int main()
    {
        Employee employee1 = Employee("Devin", "ADAC", 100);


        Employee employee2 = Employee("Kobe", "Lakers", 43);

        employee1.Introduceyourself();
        employee2.Introduceyourself();
        employee
    

    }