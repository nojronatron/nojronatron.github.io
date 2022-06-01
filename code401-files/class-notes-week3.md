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

- Project Type: Gradle (over Maven)
- Language: Java (rather than Kotlin or Groovy)
- Spring Boot type (2.7.0, non-snapshot recommended)
- Metadata: Fill-in with the actual project info.  
- Packaging: JAR (rather than WAR)
- Java version: Your version (today is v17)

Metadata:

- Group: Must be *unique*. 'com.example' works on localhost. Will *not* work on Heroku.  
- Artifact: Internal Project Name  
- Name: Your custom project name.
- Description: Your custom description for your project.  
- Package Name: Derived from inputs above.

DO: Click Generate => Zip is downloaded to your localhost.
THEN: Unzip to your project location and then open your IDE to the root of the project.
ALSO: Verify '.gitignore' has the correct additions to avoid sharing built code and other Project details related to your IDE settings.  

#### Folder Hierarchy Review

application.properties: Synonymous with '.env' file.  
main resources static: CSS, Images, and non-dynamic HTML files like 'index.html'.  
Create new Folders and Files to store CSS etc e.g. 'resources/static.css/style.css'.  
src main java com.ProjectName.Name => Add a '$name$Controller' file.  

##### CSS

Yes BOOTSTRAP CAN BE USED!!
Import Bootstrap to Spring MVC: TBD

Resource: [Bootstrap CSS in Spring MVC on StackOverflow](https://stackoverflow.com/questions/22693452/bootstrap-with-spring-mvc)  

#### Project Execution

Tomcat gets launched for you using a default port 8080.  
*Note*: Use 'kill pid' to get rid of a lingering Tomcat instance.  

#### Building a Controller

This enables *dynamic web pages*.  
Define the controller with '@Controller' to *describe the Class*.
Set the Map using '@RequestMapping(String)` to *describe the Class*.
For now: Make all Controllers using public access modifiers.  
Process:

1. Set the request method
2. Set either a Response Body or use A Model:

    - '@ResponseBody'  
    - 'return "tempateName";'  

3. Set up a View for the results to be sent to (else WhiteLabel Error)

    - Get Mapping '@GetMapping("/routeToGet")`
    - Use ResponseBody '@ResponseBody`
    - Implement the controller method(){} to define what to return.

Use RESTful commands for these Controllers: GET, POST, PUT, and DELETE
Think of Controllers as *the logic for your resource*.  
Domain Model your Controllers to define:

- Routes
- Resources
- Add/Remove/Update operations

#### Path Variables

Use '@PathVariable' keyword with the method definition like `public String doThing(@PathVariable String paramName){}`  
Use '@RequestParam';' keyword to extract query parameters, form parameters, or files from the web Request.  

#### Live Reload

Manual reload is just the Reload button in the IDE.  
TBD  

#### URL Parameters vs POST Call

URL Parameters can be captured by Controllers.  
POST Calls will include data (TBD).  

#### Using Models

Do NOT use '@ResponseBody' because a Model will do this for us.  
Return type is still String.  
Return statement will include "model" i.e. `return "model"` so that the model itself is returns (this is a Spring MVC implementation detail).  
Thymeleaf looks at directory 'templates' when `return "model"` is used e.g. 'model.html'.  
Thymeleaf will allow you to point to a template page within a folder using `return "parentfolder/mymodel` will point to '.../templates/parentfolder/mymodel.html'.  
Thymeleaf looks to the 'templates' folder to find the return type.  
Thymeleaf attributes are `th:name` which can be used within HTML elements.  
Thymeleaf 'th' attributes use a template literal style notation: `${model.name}`  

```html
<span th:text="${model.name}"></span>
```

In Spring, the actual Model is what is passed-in as params to a Controller (route).  
Think of these Models as a data Schema.  
MVC Model `.addAttribute()` method accepts an Object Instance and is used as the Controller return type.  

#### FAT vs skinny Controllers

Fat Controller: Defines ALL or MOST processing and functionality within it.  
Skinny Controller: Relies on other Modules, Packages, and internal Code to do the work, and the Controller's only purpose is to manage the path, parameters, and returning the correct View template.  

### IoC and Dependency Injection

NPM uses DI in terms of creating a dependency list and so on.  
DI is more than what NPM does => Essentially it creates a dependency-filled object out-of-the-gate so that the object instance is ready for you when you need it within the App.  

Common Dependencies We Will Use in Class:

- Thymeleaf: HTML is displayed in common web browsers as static prototypes.
- Spring Boot DevTools: Live Reload and configs for dev.
- Spring Web: RESTful WebApps with Apache Tomcat.

### Tuesday Lab and Code Challenge

#### Lab

1. Use Spring Initializr, create a new App with artifact "songr" using Web and Thymeleaf. If "songr" is missing, the Lab is *not done right*.  
1. Optionally use DevTools (live Reload and other goodies).  
1. Use 'git init' to create new repo, add '.gitignore' etc.  
1. Create a controller to create a hello route.  
1. Create a route to turn words into UPPERCASE.
1. Create and stylize a root 'spash' page, keep it basic.  
1. Create an 'Album' class to act as a Model. It will have several properties including an imgurl.  
1. Create a '/album' route that displays 3 hard-coded Albums.  
1. Build tests for the Album class: Constructor, getters, setters.  
1. Stretch goals. Review the assignment for details. Check out "query parameters" which use '?' indicator, which URL Params are just the *path* itself.  
1. Follow the Grading Rubric that specifies what *needs* to be accomplished!  

*Note*: Images go into the resources folder in the project hierarchy.  

#### Code Challenge 11

Create a pseudo Queue that implements a standard Stack interface.  
Create a pseudo Stack that implements a standard Queue interface.  

Challenges include limited functionality use.  

Hint: Use TWO Stack instances.  

*Note*: Tests are required in this Code Challenge.  

## Wednesday Morning Discussion

RESTful Routing with Spring MVC.  
PostgreSQL as a relational DB.  
JPA - Persistence API? Persist data into the DB.  
JDBC - Connects to Postgres local or remote.  
DB Connection String required (like everywhere else).  

Midterm Prep starts on Monday 1-Jun-22.

### PostgreSQL

Linux info follows:

- Once installed, launch PSQL using this line in SH/ZSH: `sudo -u postgres psql`  

### Weds SongR Code Reviews

`@RequestMapping("/path")` is OPTIONAL and should only be used if all other functionality in the Controller should be *behind* this mapping path decorator.  
Schema and Class are similar, however they are syntactically different:  

- Schema: Context is related to database use.
- Class: Object-oriented programming related.
- Entity: Describes a Table in a Relational DB (SQL). Usually a decorated Class.  

### Salmon Cookies Demo

Rest architecture allows interacting with other REST APIs.  
Architectural *constraints* are put in place.  
Client Server architecture => made RESTful via HTTP.  
Stateless: No data is stored between Req-Res.  

No `@RequestMapping("/...")` path in his SalmonCookiesStoresController.  
`th:each` enables iterating through an array of Attributes passed-in by the Controller.  

Persisting Data: PJA  
RESTful methods: Get, Post, Put, Delete  

- Read One => ID needed
- Update One => ID needed
- Delete One => ID needed

To implement CRUD operations we will need to:

- Update the Model (delivery method for data between Controller and View)
- Update the Album Class (to represent the data in the DB)
- Implement the DB Tables and transport (via JSON)

JPA: Java Persistence API, retains/persists data.  
JPA belongs on our Spring MVC Controller(s).  
Other persistence APIs persist data between refresh, app close, caching data across sessions, cookies, and many more.  
ORM: Object Relational Mapping => Describes relationships within a DB.  
ORM Hibernate: ORM Framework for use with Java, Sring.  

*Recall*: Frameworks have *constraints*, unless Libraries that do not.  

ORM Hibernate enables similar functionality to Mongoose:

- findByOne
- findByAll
- save
- etc

JDBC: Java Database Controller => Makes it easy to implement repositories for our DB.  
JDBC belongs between JPA/Controller and the Database.  
JDBC provides CRUD Services (to abstract-away the Database Interfacee?).  

Services:

- Repository (JDBC) as a service.
- AutoWire: Dependency Injection package. Use `@Autowired`  

Dependency Injection:

- Create a Singleton instance of a service (the repo) to only require as needed
- Ensures that only one instance exists and only as needed

Create a Repository:

1. Add new Package witin your java com.name.project
1. Create a new Interface that extends JpaRepository
1. Import your Entity into this repository Package

Beans: Injected service representations withh nccionality e.g. repo methods and access.  
Autowired: Part of DI system in Spring

### PostGres

PGAdmin => GUI Administrative tool for PostGres SQL  
PosteGresQL => PSQL is like PGAdmin  
ORD: Object Relational Database => Extends SQL (the language)  
JPA will be used to handle all the SQL Language details!  
JDBC connects JPA to PostGres.  
Once installed, set up a new SuperUser with your known password so you have access.  

### Steps to Update Project to Use DB

1. Update the model: Setup Entity with JPA, and ID (generated value), and add a default CTOR
1. Create a Repo with custom CRUD queries
1. Update Controller to use the JPA Repo and set up CRUD methods
1. Update Application.Properties with:

- JPA: Provides implementation of CRUD functionality  
- JDBC: Wrapper around JPA with connectionstring configuration  
- PostGres:  

### Add Dependencies

*Do*: Use SpringInitializr to simplify this process.  

Build.Gradle:

- PostGres as a runtimeOnly

application.properties:

- spring.datasource.url
- spring.datasource.username
- spring.datasource.password
- spring.jpa.hibernate.dll-auto=update
- spring.jpa.generate-dll=true
- #heroku: jdbc:postgresql://heroku//5678
- #also a jpa dependency

After udpating Build.Gradle run `./gradlew build` to bring in the changes.  

### Redirect View

Define a Controller method with a return type of RedirectView.  
And then the return statement: `return new RedirectView("/");`  

### Wednesday Work ToDo

Code Challenge 12: stack-queue-animal-shelter.  
Manage Dequeue and Re-Enqueue animals.  
Whiteboard this prior to doing ANY CODE.  

### Wednesday Lab RESTful Routing

File application.properties should NOT be pushed to GitHub.  
Variable management will be necessary.  
For now just gitignore it and shared GH pullers need to have their own application.properties.  
Update Album so it can be stored in a database.  
`<form action="/" method="post">...` tells the Submit event where to send the data.  
*Call for TA help* and get through this so that this *does not become a blocking lab*!  

## Footer

Return to [Parent Readme.md](../README.html)  
