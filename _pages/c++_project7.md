---
layout: archive
permalink: /C++/c++_project7
title: "Project 7 in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---


## Code so Far


        #include<iostream>
        using std::cout; using std::endl; using std::boolalpha;
        #include<string>
        using std::string;
        #include<sstream>
        using std::ostringstream;
        #include<utility>
        using std::pair; using std::make_pair;
        #include<map>
        using std::map;
        #include<set>
        using std::set;

        using ServerData = map<string, set<string>>;  // ServerData is a "Type"

        ServerData server; // heres our "actual server that we will work with"



        void print_server ( ServerData &server_passed){
            //print server

            for(auto const& pair : server_passed) {

                cout << pair.first << " : ";
                for(auto const& elem : pair.second) {
                    cout << elem << ", ";
                }
                cout << "\n";
        }
        

        }


        bool AddConnection(ServerData &sd, string sn, string un)
        {

            //Check if ther server_name sn is already in, if so
            // add user to server
            //otherwise we create a new set and add it to the map

            ServerData:: iterator found = sd.find(sn);
            if (found != sd.end() )
            {
                // then we have to insert
                found -> second.insert(un);
                return true;
            }

            else 
            {
                // the server name exist so we need to add the user
                set<string> temp; // temp storing
                temp.insert(un);
                sd.insert(make_pair(sn, temp));
                return true;
            }

            
        }

        int main()
        {   
            // send user_name  and server to  addconections

            // add conections 
            AddConnection (server, "Server1", "Devin");
            AddConnection (server, "Server3", "Paul");
            AddConnection (server, "Server3", "Chris");
            AddConnection (server, "Server2", "Ben");
            AddConnection (server, "Server1", "Austin");
            AddConnection (server, "Server1", "Tony");
            AddConnection (server, "Server1", "Arod");
            AddConnection (server, "Server1", "bob");
            AddConnection (server, "Server1", "Carrie");

            // Call to print server

            cout << "Servers and users:" << endl;
            print_server(server);

        }