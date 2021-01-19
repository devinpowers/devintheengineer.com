---
layout: archive
permalink: /C++/c++_txt
title: " Working with txt files in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

This topic can sometimes confuse me so I have an example

![inserting an Image](/images/C++/txt/Page1.jpg)


Here is the txt file (file.txt)

        devin join server1
        kobe join server2
        lebron join server1
        kobe join server2
        paul leaving server3
        ryan leaving server3
        tommas join server1




Here is the code 


        #include <iostream>
        #include <string>
        #include <utility>
        #include <fstream>
        #include <algorithm>
        using std::string; 
        using std::ifstream; using std::cout; using std::endl; using std::to_string;
        using std::invalid_argument;

        // create custom data struture here



        void ParseFileData(const string &fname){


            ifstream inFile(fname);   //ifstream is the txt file object?

            bool result;

            //error handling for no file found
            if(!inFile){
                throw std::invalid_argument("invalid argument");
            }

            if (inFile.is_open()){

                string username, command, server_name;

                while (inFile >> username >> command >> server_name ){ //each name/command one at a time

                    if ( command != "join" && command != "leaving")
                    {
                        cout << "ERRORRRRR!!!" << endl;
                    }
                    // else tho
                    if ( command == "join")
                    {
                        cout << "Joining:  " << username << " : " << server_name << endl;
                        //result = //send to add connection
                    }
                    else if (command == "leaving"){

                        cout << "Leaving " << username << " : " << server_name << endl;
                    }

                }
                
            }
            inFile.close(); // close file

        }

        int main(){

            // send file to our function
            ParseFileData("file.txt");
        }


Output


        Joining:  devin : server1
        Joining:  kobe : server2
        Joining:  lebron : server1
        Joining:  kobe : server2
        Leaving paul : server3
        Leaving ryan : server3
        Joining:  tommas : server1


## Working ifstreams in C++

![inserting an Image](/images/C++/txt/Page2.jpg)


    #include<iostream>
    using std::cout; using std::endl;
    #include<string>
    using std::string;
    #include<fstream>
    using std::ifstream;
    #include<vector>
    using std::vector;


    int main(){

        ifstream in_file("file2.txt");

        vector <string> names;

        string input; // where the names are being stored temp

        while (in_file >> input )
        {
            cout << "Input: " << input << endl;
            names.push_back(input);
        }

        // lets print the names in the file
        for (auto input : names)
        {
            cout << input << endl; 
        }
    }

txt file used:

    Devin Bob Kim Carrie Calire Connie
    Kobe Barbra Annie Connor
    Chris
    William
    Dexter
    Harrison
    Charlie
    Noah
    Nick
    Jimmy
    James
    Eric


Output:

    Input: Devin
    Input: Bob
    Input: Kim
    Input: Carrie
    Input: Calire
    Input: Connie
    Input: Kobe
    Input: Barbra
    Input: Annie
    Input: Connor
    Input: Chris
    Input: William
    Input: Dexter
    Input: Harrison
    Input: Charlie
    Input: Noah
    Input: Nick
    Input: Jimmy
    Input: James
    Input: Eric
    Devin
    Bob
    Kim
    Carrie
    Calire
    Connie
    Kobe
    Barbra
    Annie
    Connor
    Chris
    William
    Dexter
    Harrison
    Charlie
    Noah
    Nick
    Jimmy
    James
    Eric




## Working with getline in C++

![inserting an Image](/images/C++/txt/Page3.jpg)



    #include<iostream>
    using std::cout; using std::endl;
    #include<string>
    using std::string;
    #include<fstream>
    using std::ifstream;
    #include<vector>
    using std::vector;


    int main(){

        ifstream in_file("file2.txt");

        vector <string> names;

        string line; // where the names are being stored temp

        while (getline(in_file, line))
        {
            cout << " Full Line: " <<  line << endl;
            names.push_back(line);
        }

        // lets print the names in the file
        for (auto name : names)
        {
            cout << name << endl; 
        }

    }


txt file:

    Devin Bob Kim Carrie Calire Connie
    Kobe Barbra Annie Connor
    Chris
    William
    Dexter
    Harrison
    Charlie
    Noah
    Nick
    Jimmy
    James
    Eric


Output:

    Full Line: Devin Bob Kim Carrie Calire Connie
    Full Line: Kobe Barbra Annie Connor
    Full Line: Chris
    Full Line: William
    Full Line: Dexter
    Full Line: Harrison
    Full Line: Charlie
    Full Line: Noah
    Full Line: Nick
    Full Line: Jimmy
    Full Line: James
    Full Line: Eric
    Full Line: 
    Devin Bob Kim Carrie Calire Connie
    Kobe Barbra Annie Connor
    Chris
    William
    Dexter
    Harrison
    Charlie
    Noah
    Nick
    Jimmy
    James
    Eric
