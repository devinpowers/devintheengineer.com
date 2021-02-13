---
layout: archive
permalink: /C++/c++_classes
title: " Classes in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---


## Object-Oriented Programming

![inserting an Image](/images/C++/OOP/OPP1.jpg)
![inserting an Image](/images/C++/OOP/OPP2.jpg)
![inserting an Image](/images/C++/OOP/OPP3.jpg)
![inserting an Image](/images/C++/OOP/OPP4.jpg)
![inserting an Image](/images/C++/OOP/OPP5.jpg)



- OOP is a view of how both data and functions that work with that data

- Organization of OPP is called a class (or struct)

A class contains:
    1. Attributes (Data)
    2. Behaviours (Functions or methods) that operate on that data


General OOP Principles:

- Composition
- Abstraction
- Encapsulation
- Inheritance
- Polymorphism


Here is a basic Class

```cpp

#include <iostream>
using std::cout; using std::endl;
#include<string>
using std::string;

struct Employee{

public:
    // attributes
    string Name;
    string Company;
    string Email;
    int Age;

    void IntroduceYourself()
    {
        cout << "Hi, My name is " << Name << endl;
        cout << "I work for " << Company << endl;
        cout << "I am " << Age << " years old" << endl;
        cout << "My email address is: " << Email << endl;

    }
};

int main()
{
    Employee employee1;
    employee1.Name = "Devin";
    employee1.Company = "ADAC";
    employee1.Email = "powers88@msu.edu";
    employee1.Age = 25;

    // invoke function

    employee1.IntroduceYourself();

}

```

Output

```cpp

Hi, My name is Devin
I work for ADAC
I am 25 years old
My email address is: powers88@msu.edu

```



## constructors
```cpp

#include <iostream>
using std::cout; using std::endl;
#include<string>
using std::string;

struct Employee{

public:
    // attributes
    string Name;
    string Company;
    string Email;
    int Age;

    void IntroduceYourself()
    {
        cout << "Hi, My name is " << Name << endl;
        cout << "I work for " << Company << endl;
        cout << "I am " << Age << " years old" << endl;
        cout << "My email address is: " << Email << endl;

    }
    Employee(string name, string company, string email, int age){

        Name = name;
        Company = company;
        Email = email;
        Age = age;   
        }
};

int main()
{
    Employee employee1 = Employee("Devin", "ADAC", "powers88@msu.edu", 25);

    employee1.IntroduceYourself();

    Employee employee2 = Employee("Bob", "Apple", "bob23@amazon.com", 67);

    employee2.IntroduceYourself();

}

```
Output:

```cpp
Hi, My name is Devin
I work for ADAC
I am 25 years old
My email address is: powers88@msu.edu
Hi, My name is Bob
I work for Apple
I am 67 years old
My email address is: bob23@amazon.com

```


## Encapsulation

- Protecting our data

- Using Getters and Setters
```cpp

#include <iostream>
using std::cout; using std::endl;
#include<string>
using std::string;

struct Employee{

private:
    string Name;
    string Company;
    string Email;
    int Age;

public:
    //setter
    void setName(string name) { //setter
        Name = name;
    }
    string getName(){ //getter
        return Name;
    }
    void setCompany(string company){
        Company = company;
    }
    string getCompany(){
        return Company;
    }
    void setEmail(string email){
        Email = email;
    }
    string getEmail(){
        return Email;
    }
    void setAge(int age){
        Age = age;
    }
    int getAge(){
        return Age;
    }

    void IntroduceYourself()
    {
        cout << "Hi, My name is " << Name << endl;
        cout << "I work for " << Company << endl;
        cout << "I am " << Age << " years old" << endl;
        cout << "My email address is: " << Email << endl;

    }
    Employee(string name, string company, string email, int age){

        Name = name;
        Company = company;
        Email = email;
        Age = age;   
        }
};

int main()
{
    Employee employee1 = Employee("Devin", "ADAC", "powers88@msu.edu", 25);
    //employee1.IntroduceYourself();

    //Employee employee2 = Employee("Bob", "Apple", "bob23@amazon.com", 67);
    //employee2.IntroduceYourself();

    employee1.setAge(39);

    cout << employee1.getName() << " is " << employee1.getAge() << " years old! "<< endl;

}

```

Output:

```cpp 
Devin is 39 years old! 
```


Lets add some Validation Rules to our Setters!

- Added some rules for age and company name

```cpp

#include <iostream>
using std::cout; using std::endl;
#include<string>
using std::string;

struct Employee{

private:
    string Name;
    string Company;
    string Email;
    int Age;

public:
    //setter
    void setName(string name) { //setter
        Name = name;
    }
    string getName(){ //getter
        return Name;
    }
    void setCompany(string company){

        if (company == "ADAC"){

            Company = "ADAC Automotive";
        }
        else {

            Company = company;
        }
       
    }
    string getCompany(){
        return Company;
    }
    void setEmail(string email){
        Email = email;
    }
    string getEmail(){
        return Email;
    }
    void setAge(int age){
        
        if (age >= 18){
            Age = age;
        }
        
    }
    int getAge(){
        return Age;
    }

    void IntroduceYourself()
    {
        cout << "Hi, My name is " << Name << endl;
        cout << "I work for " << Company << endl;
        cout << "I am " << Age << " years old" << endl;
        cout << "My email address is: " << Email << endl;

    }
    Employee(string name, string company, string email, int age){

        Name = name;
        Company = company;
        Email = email;
        Age = age;   
        }
};

int main()
{
    Employee employee1 = Employee("Devin", "ADAC", "powers88@msu.edu", 25);
    //employee1.IntroduceYourself();

    //Employee employee2 = Employee("Bob", "Apple", "bob23@amazon.com", 67);
    //employee2.IntroduceYourself();

    employee1.setAge(12);
    employee1.setCompany("Bobs Construction Company");

    cout << employee1.getName() << " is " << employee1.getAge() << " years old! "<< endl;

    cout << employee1.getName() << " works at: " << employee1.getCompany() << endl;

    employee1.setCompany("ADAC");
    // after changing the Companies name:
    cout << employee1.getName() << " works at: " << employee1.getCompany() << endl;


}

```

Output:

```cpp 
Devin is 25 years old! 
Devin works at: Bobs Construction Company
Devin works at: ADAC Automotive

```

