---
layout: archive
permalink: /C++/c++_classes
title: " Classes in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---


## Object-Oriented Programming


- OOP is a view of how both data and functions that work with that data

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

