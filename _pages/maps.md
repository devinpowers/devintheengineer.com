---
layout: archive
permalink: /C++/maps
title: " Maps in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---

Inserting, Deleting and other Methods in Map Data Structures


Insert into Map 3 Different ways!


    #include<iostream>
    using std::cout; using std::endl;
    #include <map> 
    using std::map;
    #include<string>
    using std::string;
    #include<utility>
    using std::pair; using std::make_pair;

    int main() 
    { 
      
        map <int, string > nba;

        // insert elements into the nba map 3 different ways!!

        nba.insert({1, "Lebron James"});
        
        nba.insert(make_pair(3,"Steph Curry"));

        nba.insert(pair<int, string>(8, "Kobe Bryant"));


        //print out our map 

        cout << "KEY\tELEMENT\n";

        for (auto itr = nba.begin(); itr != nba.end(); ++itr) {
            cout << (*itr).first << '\t' << (*itr).second << '\n';

        }
    } 







Erase in Maps

    #include<iostream>
    using std::cout; using std::endl;
    #include <map> 
    using std::map;
    #include<string>
    using std::string;

    int main()
    {
    
        // initialize the Map container
        map<int, string> mp;

        // inserting into the Container
        mp.insert({ 2, "Lebron" });
        mp.insert({ 1, "Wade" });
        mp.insert({ 4, "Jordan" });
        mp.insert({ 5, "Durant" });
        mp.insert({ 3, "Curry" });

    
        // prints the elements
        cout << "The map before using erase() is : \n";

        cout << "KEY\tELEMENT\n";

        for (auto itr = mp.begin(); itr != mp.end(); ++itr) {
            cout << (*itr).first << '\t' << (*itr).second << '\n';
        }
    
        // Lets Erase some Keys in our Map
        mp.erase(1);
        mp.erase(3);
    
        // prints the elements
        cout << "\nThe map after applying erase() function is : \n";
        cout << "KEY\tELEMENT\n";
        for (auto itr = mp.begin(); itr != mp.end(); ++itr) {

            cout << (*itr).first << '\t' << (*itr).second << '\n';

        }

    }

output

    The map before using erase() is : 
    KEY     ELEMENT
    1       Wade
    2       Lebron
    3       Curry
    4       Jordan
    5       Durant

    The map after applying erase() function is : 
    KEY     ELEMENT
    2       Lebron
    4       Jordan
    5       Durant



Erase Given a position, using a find algorithm

    #include<iostream>
    using std::cout; using std::endl;
    #include <map> 
    using std::map;
    #include<string>
    using std::string;

    int main()
    {
    
        // initialize the Map container
        map<int, string> mp;

        // inserting into the Container using NBA Players
        mp.insert({ 2, "Lebron" });
        mp.insert({ 1, "Wade" });
        mp.insert({ 4, "Jordan" });
        mp.insert({ 5, "Durant" });
        mp.insert({ 3, "Curry" });
    
        // prints the elements
        cout << "The map before using erase() is : \n";
        cout << "KEY\tELEMENT\n";
        for (auto itr = mp.begin(); itr != mp.end(); ++itr) {
            cout << (*itr).first << '\t' << (*itr).second << '\n';
        }
    
        // function to erase given position
        auto it = mp.find(1);
        mp.erase(it);
    
        auto it1 = mp.find(3);
        mp.erase(it1);
    
        // prints the elements
        cout << "\nThe map after applying erase() is : \n";
        cout << "KEY\tELEMENT\n";

        for (auto itr = mp.begin(); itr != mp.end(); ++itr) {
            cout << (*itr).first << '\t' << (*itr).second << '\n';
        }
        return 0;
    }


Output

    The map before using erase() is : 
    KEY     ELEMENT
    1       Wade
    2       Lebron
    3       Curry
    4       Jordan
    5       Durant

    The map after applying erase() is : 
    KEY     ELEMENT
    2       Lebron
    4       Jordan
    5       Durant

