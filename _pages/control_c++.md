---
layout: archive
permalink: /C++/control_c++
title: "Control in C++"
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

Code For using the Or Operator:


    #include <iostream>
    #include <string>

    using namespace std;

    int main () 
    {
        string answer = "Devin";
        int age_answer = 24;

        string guess;
        cout << "Guess my name!: ";
        cin >> guess;

        int age_guess;
        cout << "Guess my Age: ";
        cin >> age_guess;


        if (guess == answer || age_guess == age_answer )  
        {

            cout << "Correct, you guessed it right!\n";
        }


        else
        {
            cout << "You entered both the age and name incorrectly\n! ";
        }

        return 0;

    }











Code for using the Not Operator:

    #include <iostream>
    #include <string>

    using namespace std;


    int main () 
    {
        string answer = "Devin";
    
        string guess;

        cout << "Guess my name!: ";
        cin >> guess;


        if ( !(guess == answer) )  
        {

            cout << "You got the Wrong Name Sir!\n";
            cout << "The name you entered was: " << guess << endl;
        }

        else
        {
            cout << "You entered the Right name Devin!\n";
        }
        

        return 0;
    }



