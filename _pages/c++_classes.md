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

A class contains:
    1. Attributes (Data)
    2. Behaviours (Functions or methods) that operate on that data


General OOP Principles:

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

### Abstraction

- hiding complex things behind things that are simple
- Think of using your smart phone and its different functions like (moving apps, camera, pressing buttons), we dont need to know the code that is going on after we perform one of these functions



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

```python
Jacob is preparing Math lesson
Jacob got promoted!! 


```

Poly

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

