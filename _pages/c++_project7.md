---
layout: archive
permalink: /C++/c++_project7
title: "Project 7 in C++ "
author_profile: true

header:
  image: "/images/tower3.jpeg"
  
---


## Code so Far


```cpp
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
// I should make sure the trailing comma is removed!

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

bool DeleteConnection (ServerData &sd, string sn, string un){

    bool result;

    ServerData:: iterator found = sd.find(sn);

    if (found != sd.end() )
    {
        //cout << un << " is Leaving : " << sn << endl;
        //found the sever, lets remove the user
        found -> second.erase(un);
        result = true;
    }
    else
    {
        result = false;
    }
    
    
    return result;

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

                //cout << "Error while trying to add " << username << endl;

                //throw domain_error(" Command wasn't Join or Leaving!! ");
                //cout << "ERRORRRRR!!!" << endl;
            }

            if ( command == "join")
            {
                // connect to server

                result = AddConnection(sd, server_name, username );
                //cout << "Connected " << username << " to server named: " << server_name << endl;
            }

            else if (command == "leaving"){

                //out << "Disconnected " << username << " from server named: " << server_name << endl;
                result = DeleteConnection (sd, server_name, username );
            }
        
        
        }
    }

    inFile.close();  //close the file

// print_server(sd);

    return sd; //return our server


}

// This function prints sets!!
void print_set ( set<string> set_passed)
{
    for (auto itr = set_passed.begin(); itr != set_passed.end(); itr++ )
    {
        cout << *itr << "\n";
    }
}


set <string> AllServers (const ServerData &sd)
{
    set<string> Server;
    // loop through our map and return just the keys
    for (auto itr = sd.begin(); itr != sd.end(); itr++ )
    {
        Server.insert(itr -> first);
    }

    return Server;
}

set <string> AllUsers (const ServerData &sd)
{
    set<string> all_users;

    for (auto itr = sd.begin(); itr != sd.end(); itr++ )
    {
        // loop thru the values which is a set
        for (auto itr2 = itr->second.begin(); itr2 != itr->second.end(); itr2++)
        {
            // add names to all_users set!
            all_users.insert(*itr2);
        }
    }

    return all_users;


}

set <string> HasConnections (const ServerData &sd, UserName un)
{
    set<string> connection_set;

    for (auto itr = sd.begin(); itr != sd.end(); itr++ )
    {
        // loop through the  
        for (auto itr2 = itr->second.begin(); itr2 != itr->second.end(); itr2++)
        {
            if (*itr2 == un) // if UserName exist in the set of Usernames
            {
                //cout << "found: our User" << un << endl;
                // need to add the server that oour username is connected too, to our connection_set
                connection_set.insert(itr->first);
    
                
            }
        }
    }

    return connection_set;

}

set <string> HasUsers( const ServerData &sd, ServerName sn)
{
    set<string> has_users;

    for (auto itr = sd.begin(); itr != sd.end(); itr++)
    {
        // loop thru our Servername until we find the Correct one were looking for
        if (itr->first == sn)
        {
            //loop through the users in this server and add them to our has_users set
            for(auto itr2= itr->second.begin(); itr2 != itr->second.end(); itr2++)
            {  
                //insert users to out has_user set

                has_users.insert(*itr2);

            }


        }
    }


    return has_users;

}




int main(){

    // open file and send 

    auto server_data = ParseServerData("prac.txt");

    //out << "Server Data: " << endl;
    //print_server (server_data);

    // lets test the set

// set<string> practice_set;

    //auto practice_set = AllServers(server_data);

    // lets print all servers this set
    //cout << "Printing Set: " << endl;
    //print_set (practice_set);

    //auto practice_set = AllUsers(server_data);

    // lets print all users in the set!
    //cout << "Printing all Users in the set: " << endl;

    // finding all servers that our User is Connected too!
    UserName user = "Nene";
    //auto practice_set = HasConnections(server_data, user);

    //cout << "Our User: " << user << " is connected to the following servers: " << endl;
    ServerName server_ =  "server10";

    auto practice_set = HasUsers(server_data, server_);

    cout << "The People Connected to " << server_ << " are: " << endl;
    print_set(practice_set);



}

# txt file were working with


devin join server1
kobe join server2
lebron join server1
kobe join server2
Nene join server5
paul leaving server3
ryan leaving server3
tommas join server1
Nene join server7
Nene join server9
Carrie join server1
Bill join server2
Ben join server2
Luke join server2
Nene join server2
Tim join server3
Nick join server1
Louis join server2
chris join server1
Nene join server1
Evie join server4
devin leaving server1
Tony join server1
Louis leaving server2
Carl join server2
Nene join server1
chrisopher join server1
Leon join server2
Bill leaving server2
Ethan join server1
Luke leaving server2
Will join server1
Austin join server2
Nene join server3
Vince join server1
Abe join server1
Jimmy join server3
James join server2
Harry join server3
Dex join server2
Wilson join server4
Charlie join server1
Nick join server4
Nick join server3
Nene join server7

```


