---
layout: archive
permalink: /C++/c++_classes
title: " Classes in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---


## Object-Oriented Programming


- **OOP** is a view of how both data and functions that work with that data

- Organization of OPP is called a class (or struct)

A class (or struct) contains:

    1. Attributes (Data)

    2. Behaviours (Functions or methods) that operate on that data


**General OOP Principles:**

- Composition
- Abstraction
- Encapsulation
- Inheritance
- Polymorphism


![inserting an Image](/images/C++/classes/oop1.jpg)
![inserting an Image](/images/C++/classes/oop2.jpg)

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

More on Private and Public accesss

```cpp
#include <iostream> 
using std::cout; using std::endl;
#include <string>
using std::string;
  
class car { 

private:
    // private cannont change this number from the object
    long car_manufactoring = 98973131234134;

public: 
    int car_id; 
    double distance; 
  
    void distance_travelled(); 
  
    void display(int a, int b) 
    { 
        cout << "car id is=\t" << a << "\ndistance travelled =\t" << b + 5 << endl;
        cout << "Car Manufactoring number is (Private) : " << car_manufactoring << endl;
    } 
}; 
  
int main() 
{ 
    car c1; // Declare c1 of type car 
    c1.car_id = 321; 
    c1.distance = 12; 
    c1.display(321, 12); 

    return 0; 
} 

```

Output:

```cpp
car id is=      321
distance travelled =    17
Car Manufactoring number is (Private) : 98973131234134

```

![inserting an Image](/images/C++/classes/oop3.jpg)


## Constructors

3 Rules for Constructors:

1. No return type
2. Has the same name as the Class
3. Must be Public


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

Why Encapsulation?

- Better control of your data, because you or someone else can change part of the code without it affecting other parts
- Plus it adds an increase in the security of data

![inserting an Image](/images/C++/classes/encap1.jpg)

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

![inserting an Image](/images/C++/classes/encap2.jpg)


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

Lets do some more examples using setters and getters with the NBA!

![inserting an Image](/images/C++/classes/encap3.jpg)

```cpp


#include <iostream>
#include <string>
using std::string;
using std::cout;
using std::endl;


class NBA {        
private:

    string Name;
    string Team;
    int Number;
 
public:

    void SetName(string x)
    {
        Name = x;
    }
    
    string GetName(){
        return Name;
    }
    void SetTeam(string y){
        Team = y;
    }
    string GetTeam(){
        return Team;
    }

    void SetNumber(int z){
        Number = z;
    }
    int GetNumber(){
        return Number;
    }


    NBA(string x, string y, int z){

        Name = x;
        Team = y;
        Number = z;
    }


};


int main() {

   NBA player1 = NBA("STEPH CURRY", "Warriors", 35);

   cout << player1.GetName() << endl;
   cout << "Player 1 team: " << player1.GetTeam() << endl;
   cout << "Player 1 Number: " << player1.GetNumber() << endl;
   
   NBA player2 = NBA("Lebron James", "Lakers", 23);

   cout << "PLayer 2: " << player2.GetName() << endl;
   cout << "PLayer 2 Team: " << player2.GetTeam() << endl;
   cout << "Player 2 number: " << player2.GetNumber() << endl;

   // can also change any of the attributes using the Setters!

   player1.SetNumber(1);

   cout << "Steph Curry Changed his number from 35 to: " << player1.GetNumber() << endl;

}


```

Output:

```cpp

STEPH CURRY
Player 1 team: Warriors
Player 1 Number: 35
PLayer 2: Lebron James
PLayer 2 Team: Lakers
Player 2 number: 23
Steph Curry Changed his number from 35 to: 1

```


Output:

```cpp 
Devin is 25 years old! 
Devin works at: Bobs Construction Company
Devin works at: ADAC Automotive

```

### Abstraction

- hiding complex things behind things that are simple
- Think of using your smart phone and its different functions like (moving apps, camera, pressing buttons), we dont need to know the code that is going on after we perform one of these functions

![inserting an Image](/images/C++/classes/abstraction1.jpg)


Here's a Contract
```cpp
#include <iostream>
using std::cout; using std::endl;
#include<string>
using std::string;


struct AbstractEmployee {
    // serve as a contract
    virtual void AskForPromotion() = 0;       

};


struct Employee: AbstractEmployee{

private:
    string Name;
    string Company;
    string Email;
    int Age;

public:
    
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
    
    void AskForPromotion(){
        // provide logic
        
        if (Age > 30){
            cout << Name << " got promoted!! " << endl;
        }
        else
        {
            cout << Name << " sorry NO promotion for you!" << endl;
        }
        
    }
};

int main()
{
    Employee employee1 = Employee("Devin", "ADAC", "powers88@msu.edu", 25);
    Employee employee2 = Employee("Bob", "Apple", "bob23@amazon.com", 67);

    employee1.AskForPromotion();
    employee2.AskForPromotion();
}
```



## Inheritance 

![inserting an Image](/images/C++/classes/inhert1.jpg)
![inserting an Image](/images/C++/classes/inhert2.jpg)


```cpp

#include <iostream>
using std::cout; using std::endl;
#include<string>
using std::string;


struct AbstractEmployee {
    // serve as a contract
    virtual void AskForPromotion() = 0;       

};


struct Employee: AbstractEmployee{

private:

    string Company;
    string Email;
    int Age;
protected:
    string Name;

public:
    
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
    
    void AskForPromotion(){
        // provide logic
        
        if (Age > 30){
            cout << Name << " got promoted!! " << endl;
        }
        else
        {
            cout << Name << " sorry NO promotion for you!" << endl;
        }
        
    }
};

struct Developer:public Employee {

public: 
    string  FavProgrammingLanguage;

    Developer(string name, string company, string email ,int age, string favProgrammingLanguage)

        :Employee(name, company, email, age)
    {
        FavProgrammingLanguage = favProgrammingLanguage;
    }
    void FixBug(){

        cout << Name << " Fixed bug using " << FavProgrammingLanguage << endl;

    }

    

};

int main()
{
    Employee employee1 = Employee("Devin", "ADAC", "powers88@msu.edu", 25);
    Employee employee2 = Employee("Bob", "Apple", "bob23@amazon.com", 67);

    // object for developer class
    Developer developer1 = Developer ("Kobe", "Lakers", "braynt@lakers", 34, "C++");

    developer1.FixBug();
    developer1.FixBug();
    developer1.FixBug();

    developer1.AskForPromotion();


}



```

Output:

```cpp

Kobe Fixed bug using C++
Kobe Fixed bug using C++
Kobe Fixed bug using C++
Kobe got promoted!! 

```


Adding on to our example of inheritance!

![inserting an Image](/images/C++/classes/inhert3.jpg)
![inserting an Image](/images/C++/classes/inhert4.jpg)



```cpp

#include <iostream>
using std::cout; using std::endl;
#include<string>
using std::string;


struct AbstractEmployee {
    // serve as a contract
    virtual void AskForPromotion() = 0;       

};


struct Employee: AbstractEmployee{

private:

    string Company;
    string Email;
    int Age;
protected:
    string Name;

public:
    
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
    
    void AskForPromotion(){
        // provide logic
        
        if (Age > 30){
            cout << Name << " got promoted!! " << endl;
        }
        else
        {
            cout << Name << " sorry NO promotion for you!" << endl;
        }
        
    }
};

struct Developer:public Employee {

public: 
    string  FavProgrammingLanguage;

    Developer(string name, string company, string email ,int age, string favProgrammingLanguage)

        :Employee(name, company, email, age)
    {
        FavProgrammingLanguage = favProgrammingLanguage;
    }
    void FixBug(){

        cout << Name << " Fixed bug using " << FavProgrammingLanguage << endl;

    }


};


struct Teacher: public Employee {

    string Subject;

    void PrepareLesson(){
        cout << Name << " is preparing " << Subject << " lesson" << endl;
    }
    Teacher(string name, string company, string email ,int age, string subject)

        :Employee(name, company, email, age)
    
    {
        Subject = subject;

    }


};

int main()
{
    Developer developer1 = Developer ("Kobe", "Lakers", "braynt@lakers", 34, "C++");

    Teacher t = Teacher("Jacob", "Cool School", "jack@school.com", 34, "Math");

    t.PrepareLesson();
    t.AskForPromotion();

}


```

Output

```cpp
Jacob is preparing Math lesson
Jacob got promoted!! 


```


Another Example of inheritance using the NBA:

```cpp
#include <iostream>
#include <string>
using std::string;
using std::cout;
using std::endl;


class NBA {        
private:

    string Team;
    int Number;

protected:
    string Name;
 
public:

    void SetName(string x)
    {
        Name = x;
    }
    
    string GetName(){
        return Name;
    }
    void SetTeam(string y){
        Team = y;
    }
    string GetTeam(){
        return Team;
    }

    void SetNumber(int z){
        Number = z;
    }
    int GetNumber(){
        return Number;
    }

    NBA(string x, string y, int z){

        Name = x;
        Team = y;
        Number = z;
    }

    void Introduce(){

        cout << "This is " << Name << endl;
        cout << "I play for the " << Team << endl;
        cout << "My number is: " << Number << endl;
    }

};

class Team: public NBA {

public:

    string League;

    // constructor:

    Team(string x, string y, int z, string league)

        :NBA(x,y,z)
    
    {
        League = league;

    }

    void speak(){

        // By making the attribute Name "protected" in NBA Class
        // We can access it otherwise it wouldnt work!!

        cout << Name << " plays in the " << League << endl;
    }


}; 


int main() {

    Team team1 = Team("Michael Jordan", "bulls", 23, "NBA");

    team1.Introduce();

    team1.speak();
}



```

Output:

```cpp
This is Michael Jordan
I play for the bulls
My number is: 23
Michael Jordan plays in the NBA

```





### Polymorphism

What is Polymorphism??


 
```cpp

#include <iostream>
using std::cout; using std::endl;
#include<string>
using std::string;


struct AbstractEmployee {
    // serve as a contract
    virtual void AskForPromotion() = 0;       

};


struct Employee: AbstractEmployee{

private:

    string Company;
    string Email;
    int Age;
protected:
    string Name;

public:
    
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
    
    void AskForPromotion(){

        // provide logic
        
        if (Age > 30){
            cout << Name << " got promoted!! " << endl;
        }
        else
        {
            cout << Name << " sorry NO promotion for you!" << endl;
        }
        
    }
    
    virtual void Work(){

        cout << Name << " is checking email, task backlog, performing tasks....." << endl;

    }
};

struct Developer:public Employee {

public: 
    string  FavProgrammingLanguage;

    Developer(string name, string company, string email ,int age, string favProgrammingLanguage)

        :Employee(name, company, email, age)
    {
        FavProgrammingLanguage = favProgrammingLanguage;
    }
    void FixBug(){

        cout << Name << " Fixed bug using " << FavProgrammingLanguage << endl;

    }

  /*  void Work() {
        cout << Name << " is writing " << FavProgrammingLanguage <<  "code " << endl;
    } */

};


struct Teacher: public Employee {

    string Subject;

    void PrepareLesson(){
        cout << Name << " is preparing " << Subject << " lesson" << endl;
    }
    Teacher(string name, string company, string email ,int age, string subject)

        :Employee(name, company, email, age)
    
    {
        Subject = subject;

    }

    void Work() {
        cout << Name << " is teaching " << Subject << endl;
    }

};

int main()      // the most common use of polymorphism is when a parent class reference is used to refer to a child class object
{

    Developer d = Developer ("Kobe", "Lakers", "braynt@lakers", 34, "C++");

    Teacher t = Teacher("Jacob", "Cool School", "jack@school.com", 34, "Math");

    Employee *e1 = &d; //hold reference to derived class

    Employee *e2 = &t;

    e1->Work();
    e2->Work();
}



```

Ouput

```cpp
Kobe is checking email, task backlog, performing tasks.....
Jacob is teaching Math

```

Now..


```cpp
#include <iostream>
using std::cout; using std::endl;
#include<string>
using std::string;


struct AbstractEmployee {
    // serve as a contract
    virtual void AskForPromotion() = 0;       

};


struct Employee: AbstractEmployee{

private:

    string Company;
    string Email;
    int Age;
protected:
    string Name;

public:
    
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
    
    void AskForPromotion(){

        // provide logic
        
        if (Age > 30){
            cout << Name << " got promoted!! " << endl;
        }
        else
        {
            cout << Name << " sorry NO promotion for you!" << endl;
        }
        
    }
    
    virtual void Work(){

        cout << Name << " is checking email, task backlog, performing tasks....." << endl;

    }
};

struct Developer:public Employee {

public: 
    string  FavProgrammingLanguage;

    Developer(string name, string company, string email ,int age, string favProgrammingLanguage)

        :Employee(name, company, email, age)
    {
        FavProgrammingLanguage = favProgrammingLanguage;
    }
    void FixBug(){

        cout << Name << " Fixed bug using " << FavProgrammingLanguage << endl;

    }

    void Work() {
        cout << Name << " is writing " << FavProgrammingLanguage <<  "code " << endl;
    } 

};


struct Teacher: public Employee {

    string Subject;

    void PrepareLesson(){
        cout << Name << " is preparing " << Subject << " lesson" << endl;
    }
    Teacher(string name, string company, string email ,int age, string subject)

        :Employee(name, company, email, age)
    
    {
        Subject = subject;

    }

    void Work() {
        cout << Name << " is teaching " << Subject << endl;
    }

};

int main()      // the most common use of polymorphism is when a parent class reference is used to refer to a child class object
{

    Developer d = Developer ("Kobe", "Lakers", "braynt@lakers", 34, "C++");

    Teacher t = Teacher("Jacob", "Cool School", "jack@school.com", 34, "Math");

    Employee *e1 = &d; //hold reference to derived class

    Employee *e2 = &t;

    e1->Work();
    e2->Work();
}


```

Output:

```cpp
Kobe is writing C++code 
Jacob is teaching Math

```

### More on structure of Programs....

* Normally we place the *structure* definition in the header file and then any functions associated with the structure in an implementation file

For example:

**main.cpp** file:

```cpp

#include "clock.h"

int main(){

    Clock my_c;
    my_c.hours = 10; // change data attributes in our struc

    cout << my_c.hours << endl;
}

```
**clock.h** file:

```cpp

struct Clock {
    int minutes;
    int hours;
    string period;
};

```


### Constructors in C++

**Initializer List**

Example of the **Format**

```cpp
Clock(int m, int h, string s) : minutes(m), hours(h), period(s) {};
```

* The colon indicates what follows is a init list
* Each comma seperates phrases afterwards
* **The empty {} is required at the end**


### More on Classes and Their Setup


**clock.h** File

```cpp
#ifndef CLOCK_H
#define CLOCK_H

#include<string>
using std::string;

struct Clock {
  int minutes;
  int hours;
  string period;
};

string print_clk(const Clock &c);

#endif

```


**clock.cpp** File

* Here we pass a clock var to a function !
* We can put functions that work with our Clock (struc) or that are a part if Clock in a separate implementation file

```cpp
#include<string>
using std::string;
#include<sstream>
using std::ostringstream;

#include "clock.h"

// convert a clock to a string
string print_clk(const Clock& c){
  ostringstream oss;
  oss << "Hours:"<< c.hours <<", Minutes:"<< c.minutes <<", Period:"<< c.period;
  return oss.str();
}
```


**Note:** Clock is a type just like int or string, so we can make references and pointers to it just like we could for any other type!!

```cpp
#include<iostream>
#include<string>

#include "clock.h"

using std::cout; using std::endl;
using std::string;

int main (){
  Clock clk1, clk2;
  
  clk1.hours = 10;
  clk2.hours = 1;
  cout << clk1.hours <<":"<< clk2.hours << endl;
  clk1.minutes = 20;
  clk1.period = "AM";
  
  Clock &ref_c = clk1;  //reference to clock !
  Clock *ptr_c = &clk1; // pointer to clock!
  ref_c.minutes = 10;
  ptr_c->period = "PM";
  
  // Call function to print our clock structure !!
  cout << "clk1:" << print_clk(clk1) << endl;
}

```

#### Methods

* We can also have methods, which are called using a . (dot operator) in the context of an object
 * example: **object.do_something();**
 * Here we called the method **do_something()** in the context of the *object* variable of type __.
 
* Methods are specific to the struc/class/type they are associated with
* Methods have some special properties:
    * Called in context of an object
    * Special Privileges
* We declare methods inside of the struc block, it indicates that it is part of the struct


#### How is Calling Objects passed?

* Remember in Python, the first parameter to every method was the calling object, we always called it *self*

* In C++ , there is no "first parameter" in every method, instead C++ creates a special variable name *this* which is used in a method call.




## Classes Part 2

**What is a constructor?**

*   Specials methods that are responsible for creating/initializing a user defined struc/class
*   Seen in Python
*   More like initializers, part of a **pipeline** that allow us to initialize elements of data struct

[ " insert Pipeline photo "]

*   If we don't provide a constructor, C++ will provide one, the synthesized constructor will initailize each data member to its default value

* Unlike Python, constructor **can be overloaded** based on parameters



**Calling the Constructor**



### Synthetic Default Constructor and Initializer Lists

* If we define **any** constructor, then C++ no longer provides any synthesized default constructor

    * When we define a constructor, it's up to use to provide all the constructors necessary for the class
    * If you want to use the default constructor, you just set the *name* of the **name_struc() = default**


### Initializer List

* Shortcut to setting data members directly!


**Format**

    NBA(string first, string last, int num) : first_name(first), last_name(last), number(num) {};

**Note**: the empyy {} is required at the end!

* Order depends on declaration, the order of initialization of the data member from an initialization list goes in the **order of declaration** in the class, not the order of the parameter in the initializer constructor


* Note: You can put the constructor in the .h or the .cpp (functions) file

```cpp
#include<iostream>
using std::cout;
using std::endl;

#include<string>
using std::string;


struct NBA {

public:
    string first_name = "First_Name";         // Default
    string last_name = "Last_Name";
    int number = 0;

    NBA() = default; // <-- Default Constructor

    NBA(string first, string last, int num) : first_name(first), last_name(last), number(num) {};

};

```


We can **test** the code above

```cpp

int main() {

    NBA player("Devin", "Powers", 3);

    NBA player2; // Default;

    cout << player.first_name << endl;
    cout << player.last_name << endl;
    cout << player.number << endl;


    cout << player2.first_name << endl;
    cout << player2.last_name << endl;
    cout << player2.number << endl;

}
```

**Output**:

```cpp
Devin
Powers
3
First_Name
Last_Name
0
```


### Advertising vs Implementation

* You try to keep the implementation out of the header when possible

* The header is the **ad** for the class. This is **what** the class does
* The implementation file is **how** the class does what is advertised


## Converting Constructor

* Two sense of cast

    * **to**-casting: A cast known type to a new variable of your class type
    * **from**-casting: A cast to a variable of your class type that is a known type

* If you write a constructor with a single parameter, then that constitutes a converting constructor
    *When C++ sees a type that, when passed to a constructor, creates the required type, it will call that constructor and do the conversion
