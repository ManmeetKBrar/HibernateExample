# Simple Hibernate Example

## Dependency and Tool Versions
Whilst is it NOT anbsolutely essential you have/use all of the following versions,
I am listing the versions I am using for reference.

* IntelliJ CE 2018.1
* Java SE 1.8.181
* Maven 3.3.39
* Hibernate 5.3.5.Final
* MySQL 5.6.40
* MySQL Connector 8.0.11

## Maven Project
The basic Maven Project (directory structure) was created using:

`mvn archetype:generate -DgroupId=academy.ausgrads.example -DartifactId=HibernateExample -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

The source files consist of:
```
.
└── java
    └── academy
        └── ausgrads
            └── example
                ├── entity
                │   └── Name.java			- The Java Class we want to save into DB
                └── hibernate
                    ├── HibernateUtil.java		- A Utility Class 
                    ├── SessionSaveExample.java		- Example 1 - "Save"
                    ├── SessionPersistExample.java	- Example 2 - "Persist"
                    └── SessionSaveOrUpdateExample.java - Example 3 - "SaveOrUpdate"
```

## How to use / run these examples

There are 3 files that you can execute:

### Preparation
Before running these you should:

(a) make sure your MySQL database is running, and if necessary change the source code in HibernateUtil.java to reflect the correct URL, PORT, DATABASE NAME, USER and PASSWORD for your database. **Note: normally this kind of configuration would be "externalised", that is, put into a config file which is read by the application. But for this simple example it is included in the Java code.**

(b) open a connection to your database using the same USER that the program will be using, and switch ("use") the same database the program will be using. Initially check to see what tables exist in the database ("show tables;")

(c) build these examples with: mvn package

Then try running each of the examples - reading this instructions to know what to expect

1/ SessionSaveExample - demonstrates using save to store an object into a db - not that if you try running it twice on the second and subsequent successful attempts you will get an exception saying that there is a duplicate ID - this is because you can't have two database records with the same primary key - this is expected behaviour.

`java -cp target/HibernateExample-1.0-SNAPSHOT.jar:target/classes/lib/* academy.ausgrads.example.hibernate.SessionSaveExample`

This program deliberately outputs a lot of information, for diagnostic purposes. It even shows the SQL that is automatically generated by Hibernate for you.

After running it, look in the database again to see that it has created a table called NAME, and that it has one record in it ("select * from NAME;")


2/

This does much the same thing as the last example, except it uses "persist" instead of "save". It can also only be used for storing a record in a database for the first time. Once the primary key exists, it can not be used again.

`java -cp target/HibernateExample-1.0-SNAPSHOT.jar:target/classes/lib/* academy.ausgrads.example.hibernate.SessionPersistExample`

3/

This example uses "SaveOrUpdate" which allow Hibernate to update a record if it exists, or create it if it does not exist. This means it can be run multiple times without exception.

`java -cp target/HibernateExample-1.0-SNAPSHOT.jar:target/classes/lib/* academy.ausgrads.example.hibernate.SessionSaveOrUpdateExample`

Don't forget to check that the data is being stored in the database.

# Challenge
Refer to the Hibernate documentation and various tutorials to try to extend this to read back the data from the database table.

# References

ref: http://hibernate.org/orm/documentation/5.3/
