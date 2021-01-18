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


Heres some extra code


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
        #include<fstream>
        using std::ifstream;
        using std::invalid_argument;
        using std::domain_error;

        using ServerData = map<string, set<string>>;  // ServerData is a "Type"
        using UserName = const string &;
        using ServerName = const string &;
        //ServerData server; 

        void print_server ( ServerData &server_in ) {
        // using iterators to print

            for(auto it=server_in.begin();it!=server_in.end();++it)  //Loop to iterate over map elements
            {
                cout<<it->first<<": ";    
                for(auto it1= it->second.begin(); it1 != it->second.end(); it1++)
                    cout<<*it1<<", ";
                cout<<"\n";   
            }
        }

        bool AddConnection(ServerData &sd, string sn, string un)
        {

            //Check if ther server_name sn is already in, if so
            // add user to server
            //otherwise we create a new set and add it to the map
            //.find will return the highest index which is index of .end()
            // if it doesnt find our server, that why it will evaluate to !=,
            // because if it's not equal, it means the server doesnt exist
            // if find, actually finds the server, that will evaluate to true
            // which means it exists and the name will be

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



        ServerData ParseServerData (const std::string &fname){



            ServerData sd; // heres are server data structure that we will add to!

            ifstream inFile(fname);


            bool result; // if we were sucessful

            // throw an error if no file is found!!
            if (!inFile){
                throw std::invalid_argument("invalid argument");
            }
            if (inFile.is_open()){

                string username, command, server_name;

                while (inFile >> username >> command >> server_name ){


                    if ( command != "join" && command != "leaving"){
                        cout << "ERRORRRRR!!!" << endl;
                    }

                    if ( command == "join")
                    {
                        // connect to server

                        result = AddConnection(sd, server_name, username );
                        cout << "Connected " << username << " to server named: " << server_name << endl;
                    }

                    else if (command == "leaving"){

                        cout << "Disconnected " << username << " from server named: " << server_name << endl;
                        /// disconnect from the server code 
                    }
                
                
                }
            }

            inFile.close();

            cout << "Server so Far: ";
            print_server(sd);

            return sd; //return our server


        }


        int main(){

            // open file and send 

            auto server_data = ParseServerData("prac.txt");


        }