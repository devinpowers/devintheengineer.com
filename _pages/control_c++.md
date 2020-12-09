---
layout: archive
permalink: /C++/control_c++
title: "Control in C++"
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---



- Insert Notes here for learning C++ Control Flow





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



Code for Using Not Equal Operator:

    #include <iostream>
    #include <string>

    using namespace std;


    int main () 
    {
        string answer = "Devin";
    
        string guess;

        cout << "Guess my name!: ";
        cin >> guess;


        if ( (guess != answer) )  
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


### Loops 

![inserting an Image](/images/C++/Control/Page1.jpg)


#### For Loops 

For Loop Code:

    #include <iostream>

    using namespace std;

    int main () 
    {
        for(int i =0; i < 10; i++ )
        {
            cout << i << endl;
        }
        return 0;
    }




#### While Loop


While Loop Code:

    #include <iostream>

    using namespace std;

    int main () 
    {
        int i = 0; // initization

        while (i < 10) // Condtion
        {
            cout << i << endl;

            i ++; // Update
        }

        return 0;
    }


While Loop Factorial Example:

    #include <iostream>

    using namespace std;

    int main () 
    {
        int fact = 5;
        int factorial = fact; // 5 * 4 * 3 * 2 * 1
        int i = factorial - 1;

        while( i > 1)
        {
            factorial *= i;
            i-- ;

        }

        cout << "Factorial of " << fact << " is: " << factorial << endl;

    }



#### Do While Loop

![inserting an Image](/images/C++/Control/dowhile.jpg)


Do While Loop Code for Guessing the Correct Password:

    #include <iostream>

    using namespace std;

    int main () 
    {
        string  password = "Hellotacos123";
        string guess;
        do 
        {
            cout << "Guess the password: ";
            cin >> guess;

        } while(guess != password);

        cout << "Exited out the 'Do While Loop' because you entered the Correct Password" << endl;

    }

