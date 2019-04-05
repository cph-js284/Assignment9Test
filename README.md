# Assignment9Test
This is the 9th. assignment for PBA Test soft2019spring

# What it is
This is a project that contains stresstests for a server. The Server is a simple server able to send and receive Json along with outputting dynamic html based on the URL.<br>
The server is run on a droplet on Digital Ocean and is configured as NignX sitting as a reverse proxy infront of Kestrel that is running the dotnet-core app.<br>
<br>
<b>NB: the droplet will be destroyed after the review periode</b></br>
<br>
This project also contains a *\*.jmx* file that has all the Jmeter tests.<br>
The folder *mvnjmeter* contains a java maven project that executes the jmeter tests (besides these tests the project is an empty template)

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


![dynamic1](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/DynamicHtml.png)<br>
*Showing the request contained in the URL*<br>
<br>
![da1](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/DynamicHtml_assert1.png)<br>
*Assert made on the response data*<br>
<br>
![da2](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/DynamicHtml_assert2.png)<br>
*Assert made on response code*<br>
<br>
![da3](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/DynamicHtml_assert3.png)<br>
*Assert made on response header*<br>
<br>
![pj](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/PostJson.png)<br>
*Posting Json data*<br>
<br>
![pja1](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/PostJson_assert1.png)<br>
*Assert made on the post json data response (the server mirrors the posted json object back as reponse)*<br>
<br>
![rj](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/ReceiveJson.png)<br>
*Requesting Json data*<br>
<br>
![rja1](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/ReceiveJson_assert1.png)<br>
*Assert made on the response-array (the double '.' is a deep-dive inside the response array)*<br>
<br>
![rja2](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/ReceiveJson_assert2.png)<br>
*Assert the id values from response array are integers between 1 and 5*<br>
<br>
![rja3](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/ReceiveJson_assert3.png)<br>
*Assert the name value is text*<br>
<br>
![rja4](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/ReceiveJson_assert4.png)<br>
*Assert the age value is int between 0-99*<br>
<br>
![csv1](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/CSVdata.png)<br>
*Extracting data from CSV file - special note here is the 'variable names' field*<br>
<br>
![csv2](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/CSVdata_dynamicHtml.png)<br>
*Constructing the URL using data from CSV file (contense of file above)*<br>
<br>
![csv3](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/CSVdata_dynamicHtml_assert1.png)<br>
*Assert the response data using data from CSV file (contense of file above)*<br>
<br>
![s1](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/report10.png)<br>
*Summary report - 10 users*<br>
<br>
![s1](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/report100.png)<br>
*Summary report - 100 users*<br>
<br>
![s1](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/report250.png)<br>
*Summary report - 250 users*<br>
<br>
*Notice the avg. response time goes down for the 100 and 250 users - likely due to response being cached on server*

# Maven project using jmeter
*A lot of files downloaded for this one*<br>

the POM.xml file from the project:
```
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>js284</groupId>
  <artifactId>mvnjmeter</artifactId>
  <packaging>jar</packaging>
  <version>1</version>
  <name>mvnjmeter</name>
  <url>http://maven.apache.org</url>
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>


  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
  <build>
     <plugins>
        <plugin>
            <groupId>com.lazerycode.jmeter</groupId>
            <artifactId>jmeter-maven-plugin</artifactId>
            <version>2.9.0</version>
            <executions>
                <execution>
                    <id>jmeter-tests</id>
                    <goals>
                        <goal>jmeter</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
</project>
```
Besides the POM-file a folder called 'jmeter' was created in src/test/ this folder is scanned for *\*.jmx* files durring mvn verify
To execute the jmeter tests:<br>
*Beaware this will take more than 30 secs. due to the jmeter tests alone taking 30 secs.*
```
mvn clean verify
```
I did a 
```
mvn clean verify >> verifylog.txt
```
Resulting in the [verifylog.txt](https://github.com/cph-js284/Assignment9Test/blob/master/mvnjmeter/verifylog.txt) (inside the mvnjmeter folder) file contained in this repo - this log documents the successful verification and testing of the maven project executing the jmeter tests

# Blazemeter
I was not sure how exactly to document the Blazemeter test/executing, so I just added some more screenshots; showing 50 users, running for 20 mins. from location: Japan.<br>
![bla1](https://github.com/cph-js284/Assignment9Test/blob/master/Screenshots/blazemeter1.png)<br>
