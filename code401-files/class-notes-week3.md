# Class Notes Week 3

31-May through 3-June 2022

## Tuesday Discussion

For the next 2 weeks: Working on building servers in Java.  
Lots of assignments / calendar will be shifted around a bit due to Memorial Day.  
Using URL Params to make sites reactive.  
Personal Pitches:

- Okay to rework it as needed!
- Bullet points is a good way to go
- Might be *less than 15 seconds* to make a good impression on somebody

## Code Reviews

Whenever doing data structures *make them generic* it just makes sense.  
When using a built-in Class or 3rd Party Package you should at least review its description, usage, etc. This could be good if asked about it while reviewing code.  
When opening HttpUrlConnection in Java, remember to call '.close()' method *or use Try with resources* so that when done, memory resources are freed.  

## Tuesday Schedule

Career Coaching Friday! Get your plan in *now*.  
Midterm Project: Does *not* have to be a website! Could be a cool tool.  
This week:

- Spring: MVC, Boot, and Initializr => Hello Internet!
- Thymeleaf templates, styling.
- Deploying to Heroku.

### Spring MVC Discussion

Difference between a Framework and a Library:

- Frameworks have RULES and constraints: Rules of Framework utilize markers like '@' to identify the rule that is being utilized.  
- Library is a resource with no rules (or very few): Just import it and leverage the Library functionality.  

Spring MVC is a Framework.  
MVC is a design pattern.  
Spring has pretty thorough documentation so *use it*!  
Spring enables creating Java Servers.  
Model: A description of the data that will be read, written, and transformed (or transported between functions and components).  
View: A template that defines a graphical interface (UI).  
Controller: Handles logic of a resources.  
In Spring MVC only *one Model* can be injected into each *View* so it is critical to create Models that properly model the expected data returned from the DB.  
Controllers are defined following Separation of Responsibility coding practices.  

### SQL vs Non-SQL DBs

Mongo is a non-relational database, so scalability can be a limitation.  
SQL is a relational database and is very scalable.  
SQL implements it's own ID field in data.  
UUID is a user-defined ID that might be a good idea to implement depending on app and dev requirements.  
Fields must be defined specifically e.g. String Name, and FK Colors.ID.  

#### Designing Relationships

1:1 => The data just goes into the record directly.  
1:Many => Use an FK (Foreign Key) to point to the table and ID where the data resides.  
*Note*: Domain Model these relationships *every time* before implementing a SQL DB.  

### Spring Initializr

Spring [Initializr website](https://start.spring.io)  
We will be using this going forward with Spring-based development.  
Enables setting:

- Project Type
- Language
- Spring Boot type (2.7.0, non-snapshot recommended)
- Metadata: Fill-in with the actual project info.  

Metadata:

- Group: Must be *unique*. 'com.example' works on localhost. Will *not* work on Heroku.  
- Artifact: Internal Project Name  
- Name: 
- 

## Footer

Return to [Parent Readme.md](../README.html)  
