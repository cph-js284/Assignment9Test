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

# Documentation
Here is a variaty of screenshots I found the most relevant for documenting the setup, further analysis can be made from inside the Jmeter IDE after the included *\*.jmx* file is loaded.


![dynamic1](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/DynamicHtml.png)
*Showing the request contained in the URL*<br>
<br>
![da1](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/DynamicHtml_assert1.png)
*Assert made on the response data*<br>
<br>
![da2](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/DynamicHtml_assert2.png)
*Assert made on response code*

![da3](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/DynamicHtml_assert3.png)
*Assert made on response header*

![pj](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/PostJson.png)
*Posting Json data*

![pja1](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/PostJson_assert1.png)
*Assert made on the post json data response (the server mirrors the posted json object back as reponse)*

![rj](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/ReceiveJson.png)
*Requesting Json data*

![rja1](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/ReceiveJson_assert1.png)
*Assert made on the response-array (the double '.' is a deep-dive inside the response array)*

![rja2](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/ReceiveJson_assert2.png)
*Assert the id values from response array are integers between 1 and 5*

![rja3](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/ReceiveJson_assert3.png)
*Assert the name value is text*

![rja4](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/ReceiveJson_assert4.png)
*Assert the age value is int between 0-99*

![csv1](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/CSVdata.png)
*Extracting data from CSV file - special note here is the 'variable names' field*

![csv2](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/CSVdata_dynamicHtml.png)
*Constructing the URL using data from CSV file (contense of file above)*

![csv3](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/CSVdata_dynamicHtml_assert1.png)
*Assert the response data using data from CSV file (contense of file above)*

![s1](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/report10.png)
*Summary report - 10 users*

![s1](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/report100.png)
*Summary report - 100 users*

![s1](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/report250.png)
*Summary report - 250 users*

*Notice the avg. response time goes down for the 100 and 250 users - likely due to response being cached on server*

