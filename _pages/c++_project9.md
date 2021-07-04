---
layout: archive
permalink: /C++/c++_project9
title: "Project 9 in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

* Representing a FSA -> Finite State Automation

![inserting an Image](/images/C++/Projects/project9/fsa.jpg)


**Header File (functions.h)**

```cpp
#ifndef FSA_H
#define FSA_H

#include<iostream>
using std::ostream;
#include<fstream>
using std::ifstream;
#include<map>
using std::map;
#include<string>
using std::string;

class FSA{
  
private:
  map<string, map<string, string>> table_;
  string state_;
  string start_;
  string finish_;

public:
  FSA()=default;
  FSA(string strt, string stp);
  FSA(ifstream&);
  bool exists_state(string);
  void add_state(string);
  void add_transition(string, string, string);
  string transitions_to_string(string);
  string next(string,string);
  bool run(string);
  friend ostream& operator<<(ostream&, FSA&);     // WHEN YOU call to print (cout) FSA, it calls this method
};

#endif
```


**Functions File (functions.cpp)**

```cpp
#include<iostream>
using std::ostream;
using std::boolalpha;
#include<sstream>
using std::ostringstream;
#include<fstream>
using std::ifstream;
#include<map>
using std::map;
#include<string>
using std::string;
#include<iostream>
using std::cout; using std::endl;
#include<utility>
using std::pair;
#include"functions.h"

// Constructors
FSA::FSA(string start, string stop)
{
    // Initilizer

    start_ = start;
    finish_ = stop;
    state_ = start; // current state you're in is the starting position
}

FSA::FSA(ifstream& fs){
    string start, stop, input;

    fs >> start >> stop;
    // set
    start_ = start;
    finish_ = stop;
    state_ = start;

    // now we need to get all the transitions in the file
    while (fs >> start >> input >> stop)
    {
        table_[start][input] = stop;
    }
}

// Member Functions to Work with 


bool FSA::exists_state(string s)
{
    // finds if the key is in the table

    if (table_.find(s) == table_.end()){
        // Key isn't in the table
        return false;
    }
    return true; // key is in the table
}


void FSA::add_state(string s){

    if (!exists_state(s)) {
        // if True, which exist_state function returns a false hence with the !
        // We add the string s as a key in our table
        table_[s];
    }
    // Else the key already exists and we throw a domain error
    else
    {
        string error_string = s + " already exists in our Map";
        throw std::domain_error(error_string); // throw the domain error

    }

}

void FSA::add_transition(string s1, string input, string s2)
{
    if (table_.find(s1) != table_.end())
    {
        // if the key (s1) is in the table, we add the transition
        table_[s1][input] = s2;

    }
    else
    {
        // The key isn't in the Map so we throw another Domain error
        string error_string = s1 + " doesn't exist in our map";
        throw std::domain_error(error_string);
    }


}

string FSA::transitions_to_string(string s)
 {
    // Returns a string off all the transitions associated with the state "s"
    // Otherwise it throws a domain_error if the state isn't in the table

    ostringstream os;
    string return_string;

    // if the key is in the table, lets add it to our string return_string;

    if (table_.find(s) != table_.end())
    {
        os << s << ":";
        for (pair<string, string> p: table_[s] )
        {
            os << " on " << p.first << " --> " << p.second << ",";
        }
        return_string = os.str(); // convert os to a string
        return_string = return_string.substr(0, return_string.size() -1 );
        return return_string;
    }
    else
    { 
      // Throw a domain error because the key does not exist!!!
       string error_string = s + " doesn't exist";
       throw std::domain_error(error_string); 
    }

}



string FSA::next (string s, string input)
{
    // Starting from state s and given an input, return the next state
    if (table_.find(s) != table_.end())
    {
        // if the key is in the table
        if (table_[s].find(input) != table_[s].end())
        {
            // then return the next order
            return table_[s][input];
        }
        else
        {
            // throw a domain error
            string error_string = s + " has no transition on the input " + input;
            throw std::domain_error(error_string);
        }
    }
    // throw the domain error
    else
    {
        string error_string = s + " Key doesn't exist";
        throw std::domain_error(error_string);
    }
}

bool FSA::run(string s)
{
    // starting from the start state, run the FSA and having consumed the input, return
    // if the final state is finish_state or not
    // Use the method next to help

    for (char c : s)
    {
        state_ = next(state_, string(1,c)); // get the next state
        cout << "Got to: " << state_ << " on a  " << c << endl; // outputs the path it took
    }
    return (state_ == finish_); 


}

// Friend Function heres
// When you run cout << FSA, this friend function will print out 

ostream& operator<<(ostream& out, FSA& fsa)
{
    // this function prints a representation of the FSA including the start, finish, and current state
    // including all the transitions

    out << "Start: " << fsa.start_ << ", Finish: " << fsa.finish_ << ", Present: " << fsa.state_ << endl;

    //print the table
    for (pair<string,map<string, string>> p : fsa.table_)
    {
        out << fsa.transitions_to_string(p.first) << endl;
    }

    return out;
}
```

**Main File (main.cpp)**

```cpp
#include<iostream>
using std::cout; using std::cin; using std::endl;
using std::ostream; using std::boolalpha;
#include<fstream>
using std::ifstream;
#include<map>
using std::map;
#include<deque>
using std::deque;
#include<string>
using std::string;
#include<sstream>
using std::istringstream;
#include<stdexcept>
using std::domain_error; using std::out_of_range;
#include<iterator>
using std::ostream_iterator;
#include<algorithm>
using std::copy; using std::find;

#include "functions.h"

int main () {
    int test_no;
    cin >> test_no;
    cout << boolalpha;
    
    switch (test_no){
            
        case 1:{
            FSA fsa;
            string state;
            cin >> state;
            try{
                fsa.add_state(state);
                cout << "added state:"<<state<<endl;
                // should throw
                fsa.add_state(state);
            }
            catch(domain_error &e){
                cout << e.what() <<endl;
            }
            cout << fsa.exists_state(state) << endl;
            cout << fsa.exists_state("X") << endl;
            break;
        }
            
        case 2:{
            FSA fsa;
            string from_s, input, to_s;
            cin >> from_s >> input >> to_s;
            try{
                fsa.add_state(from_s);
                fsa.add_transition(from_s, input, to_s);
                cout << "from "<<from_s << " to "<<input<<" on "
                <<input<<endl;
                
                // should throw
                fsa.add_transition("X", input, to_s);
            }
            catch(domain_error &e){
                cout << e.what() <<endl;
            }
            break;
        }
            
        case 3:{
            FSA fsa;
            string from_s, input, to_s;
            cin >> from_s >> input >> to_s;
            try{
                fsa.add_state(from_s);
                fsa.add_transition(from_s, input, to_s);
                cin >> from_s >> input >> to_s;
                fsa.add_transition(from_s, input, to_s);
                cout << fsa.transitions_to_string (from_s) << endl;
                
                // throw
                cout << fsa.transitions_to_string("X") << endl;
                
            }
            catch(domain_error &e){
                cout << e.what() <<endl;
            }
            break;
        }
            
        case 4:{
            string from_s, input, to_s;
            cin >> from_s >> input >> to_s;
            FSA fsa(from_s, to_s);
            fsa.add_state(from_s);
            fsa.add_transition(from_s, input, to_s);
            cin >> from_s >> input >> to_s;
            fsa.add_transition(from_s, input, to_s);
            
            cout << fsa << endl;
            break;
        }
            
        case 5:{
            string fname;
            cin >> fname;
            ifstream fin(fname);
            FSA fsa(fin);
            cout << fsa << endl;
            break;
        }
            
        case 6:{
            string fname;
            cin >> fname;
            ifstream fin(fname);
            FSA fsa(fin);
            string state;
            cin >> state;
            
            try{
                cout << fsa.next(state, "0") << endl;
                
                // should throw
                cout << fsa.next("X", "1") << endl;
            }
            catch(domain_error &e){
                cout << e.what() << endl;
            }
            break;
        }
            
        case 7:{
            string fname;
            cin >> fname;
            ifstream fin(fname);
            FSA fsa(fin);
            string state;
            cin >> state;
            
            try{
                cout << fsa.next(state, "0") << endl;
                
                // should throw
                cout << fsa.next(state, "X") << endl;
            }
            catch(domain_error &e){
                cout << e.what() << endl;
            }
            break;
        }
            
        case 8:{
            string fname;
            cin >> fname;
            ifstream fin(fname);
            FSA fsa(fin);
            string input;
            cin >> input;
            
            bool accept;
            accept = fsa.run(input);
            cout << endl<< "accepted?: "<<accept << endl;
            break;
        }
            
        case 9:{
            string fname;
            cin >> fname;
            ifstream fin(fname);
            FSA fsa(fin);
            string input;
            cin >> input;
            
            cout << fsa << endl;
            bool accept;
            accept = fsa.run(input);
            cout << endl<< "accepted?: "<<accept << endl;
            cout << fsa << endl;
            break;
        }
            
    } // of switch
} // of main;
```

### Notes on Project 9

![inserting an Image](/images/C++/Projects/project9/functions1.jpg)
![inserting an Image](/images/C++/Projects/project9/functions2.jpg)
![inserting an Image](/images/C++/Projects/project9/functions3.jpg)
![inserting an Image](/images/C++/Projects/project9/functions4.jpg)
