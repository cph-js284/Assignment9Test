# Assignment9Test
This is the 9th. assignment for PBA Test soft2019spring

# What it is
This is a project that contains stresstests for a server. The Server is a simple server able to send and receive Json along with outputting dynamic html based on the URL.<br>
The server is run on a droplet on Digital Ocean and is configured as NignX sitting as a reverse proxy infront of Kestrel that is running the dotnet-core app.<br>
<br>
<b>NB: the droplet will be destroyed after the review periode</b></br>
<br>
This project also contains a *\*.jmx* file that has all the Jmeter tests.

# Setup
1) clone the repo
2) open the *\*.jmx* inside the Jmeter IDE and run it.

# Report data
The folder <b>report data</b> contains 3 *\*.csv* files. Each of these files are the result of executing the 3 different threadgroups (10/100/250 users)

# Test data
The folder <b>test data</b> contains an *\*.csv* file that is used when pulling values into the assertions in Jmeter.<br>
It has the following format:
````
Id value given:     Expected ID:    Expected Name:      Expected Age:     Expected Err msg (if any)
1,                  1,              Adam,               23,               
2,                  2,              Brian,              31,
3,                  3,              Cecilia,            32,
4,                  4,              Dante,              41,
5,                  5,              Eve,                33,
42,                 ,               ,                   ,                 Invalid input
-42,                ,               ,                   ,                 Invalid input
````
*This is based on the fact the server has a build-in (hardcoded) list of 5 student-objects, any id non-valid id returns 'Invalid input'*

