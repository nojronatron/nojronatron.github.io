# Class Notes Week 2

23-May through 27-May 2022

## Monday Discussion

Inheritance: Super and Extends => Create sub-classes.  
Abstraction: Abstract Classes => Stepping "out one layer" from doing the actual thing.  
DRY: Code modularization => Don't Repeat Yourself. Why keep writing the same code over and over?  
Object hierarchy: Built-in methods get inherited down the tree.  
Everything is Java is either a Class aka Object aka REF type, or a Primative.  
Type casting: Upcasting (free in Java) and Downcasting (manual)  
Instance of: IS-A => Is this Type type an instance of AnotherType.  
Arguments: Have actual value and are set when a method is called.  
Parameters: Are placeholders for Arguments that are expected as method inputs.  
Primatives: Long, Double, Short, Char, Integer, Decimal, Float, Byte, Boolean.  
Keyword 'this': Use to limit the scope, i.e. within a Constructor or inside a spefific Class and not it's base or Parent Class. Objects do NOT have a 'this' keyword, but CLASSES need this.  
Dot Notation is equivalent to Class Notation => ClassName.memberName  
Encapsulation: Data Hiding => Do not show Properties to other Classes.  
Getters & Setters => Methods that enable reading from, and writing to, Properties.  
Use *methods* (getters and setters) to retrieve and update Properties.  
Not a primative? Then it is a Reference Type.  
Keyword 'new' => Results in creating a new Object (instance).  
70/30 Time Split: Devs spent more time planning their project (70%) over writing it (30%).  
Passing by Value vs Passing by Reference => High level, parameter values are copied or a reference to the memory location is copied.  
Sub Class == Child Class == Inheriting Class.  

### Monday Domain Modeling and Inheritance

List out all of the things and their properties into boxes.  
Look for overlaps between the items and push any common members 'up the hierarchy'.  
Identify member types including Primatives or Classes (Built-in or Custom).  
Once the Member details and Hierarchical arrangement are drawn out, THEN open your IDE and start coding the Classes and inheritance.  
Use inheritance in Class definitions while coding, e.g.:  

```java
public class Artist {
  protected String name;
  String genre;
  public void writeMusic() {
    System.out.println("boopy-dooby");
  }
}
public class Musician extends Artist {
  ...
}
public class Composer extends Artist {
  ...
}
```

Write Tests! Use the IntelliJ generator to help you write test methods.  

Constructors of child classes must be created too!  
We can create Constructors that are rooted in the Class's Parent Class.  

```java
public class Musician extends Artist {
  public int totalSongs;
  public Musician(String name, String genre, int totalSongs) {
    super(name, genre); // this is calling the parent constructor grabbing its properties
    this.totalSongs = totalSongs;
  }
}
// private fields in the parent will NOT show via the super() constructor call
```

Packages vs Sub Classes: A sub class might be imported via another Package, so Access Modifiers are important to understand.  
While domain modeling, ask yourself: Which Class should be responsible?  

- Acquiring data  
- Processing data  

### Abstract Classes

You cannot instantiate an Abstract Class => NO NEW KEYWORD!  
Abstract Classes: Write your "big logic" code here so all inheriting classes implement it without rewriting the same code.  
Keyword 'abstract', e.g.:  

```java
public abstract class Artist {
  protected String name;
  String genre;
}
```

Abstraction: Hide complexities of an implementation. Only expose an API that includes implementations that *you want inheritors to use*.  

Abstract Members: Use the 'abstract' keyword to define methods that *tells inheritors they must implement it*.  

### Override vs Overload

Override: Used to implement abstract methods.  
Overload: Create multiple methods using the same name but changing the number or input parameters and possibly the return type.  


## Wednesday Discussion

MVP: Pare this down more than you want to for your final! Avoids.  
Passing by value: This is the *default* operation in Java, primatives and classes.  
Java passes REFERENCES by value by default.  
Passing by reference: MUST BE SPECIFIED with a keyword.  
Call Stack: Where temporary memory gets stored and methods are stored during execution.  
Heap: Longer-term memory storage of object instances and their data.  
Reference Addresses: Stored in the Stack, point to memory locations in the Heap e.g. to an Object.  
GSon: Stringifying objects.  
JSON: Similar to javascript objects (braces surrounding KVPs), using string-based keys.  
Java cannot natively read JSON:

- You need to define object(s) that are in the JSON before Java can use it.  
- Also need to use a Package Library to read-in and write-out JSON.  

### Weds Callenge Review

KEY CODE TO REMEMBER FOR LINKED LISTS: `while(current != null) {...}`  
Keywords:

- break: Break OUT of the parent loop/iterating structure.  
- continue: Stop the current iteration and start the NEXT iteration.  

### Weds Lab Review

Push as many members UP the hierarchy to a parent class as possible to simplify domain model design.  
Use GETTERS so that other Objects have access to information in parent, sibling, and other Objects.  
super. vs super():

- `super.`: References the parent class using object (dot) notation.  
- `super()`: invokes the parent Constructor, based on parameter list matching.  

Implicit Upcasting: A shortcut, affirms that a type IS-A, which is similar to how Generics are implemented.  

### Good Developer Concepts

DRY: Don't repeat yourself.  
YAGNI: Don't implement what is not needed right now. Future-Proofing can end up violating this rule.  
RuleOf3: If you're writing the same code for the 3rd+ time, consider modularizing it into a common or helper function.  
MVP: Minimum Viable Product => An experiment that early, visionaries get to use and provide feedback of an App while it is a mimumally usable (but functional) state.  
KISS: Keep is simple. Don't over-complicate the code, just solve the problem at hand, as directly as possible.  
SOLID: A set of principles.

### SOLID Principles

Single Responsibility:  
Open-Closed:  
Liskov Substitution:  
Interface Segregation:  
Dependency Inversion:  

### Team Concepts

PM: Product or Project Manager  
TL: Team Lead  
Senior Dev: Assists with managing the developer processes and workload.  

Clients/customers: Will have a set of requirements, wants/needs that need to get turned into User Stories.  
Take customer/client requirements and develop user stories.  

The Dev (You): Implement these User Stories in code.  

### Code Styling

How do you name your variables and members? Snake_Case? Skewer-Case?  
How do you write tests?  
Where do you throw exceptions?  
How do you name your Classes, Interfaces, etc.  
Single-line or multi-line conditionals?  
How many tab spaces are standard? 2? 4? Some other number?  
How is the directory architecture set up in your project(s)?  

My team / employer might have a code style guide and *you will need to follow it*.  

If a guide doesn't exist MAKE ONE! It will help others create consistent code.  

Code Linters: The Linter enforces (or warns) about code style violations.  

### Wednesday Relational DB Overview

IDs and UUIDs: One is for SQL, the other is for you (the software or API).  
Data that we are storing within classes today, will actually be stored in SQL, in real life.  
Relational checking a-la: 'Where foreignKey = itemId'  

### Wednesday GSON and JSON

GSON is an external package.  
Google Script Object Notation.  
JUnitJupiter is an external package.  
The gradle config has a dependency codeblock that defines the required packages for build (and test).  
JSON is consumed via several ways: Files, Internet, Resources (e.g. libraries, DBs, etc).  
JSON is fast and thin compared to other data types.  
Serialization: Translate INTO JSON format. Makes it easier to XMIT data via the web/network.  
Deserialization: Extract the data from JSON format into an Object or Collection of Objects.  
JSON is plaintext, therefore a String, and WYSIWYG.  

Lab Goal today: Read-in a JSON file.  

Do this using GSON.  
When reading-in JSON, you will need to have a Class instance to push the imported data into (members etc).  

Design:  
App imports Files: `implementation 'com.google.code.gson:n.n.n'` => add this (and more) to build.gradle  
import GSON: `import com.google.gson.Gson;`  
Rebuild: Reset Gradle (use a build command) to ensure build.gradle changes are picked up.  
test => resources directory: Allows Tests easy access to the files during test writing and execution.  
Read-in a file:  

1. Define a Try-Catch to wrap-around the following (or use 'throws IOException' at method definition).  
2. Find filepath: `File myFile = new File("./app/src/test/resources/JSON.json");`  
3. Use try-with-resources to utilize FileReader.
4. Use fileReader: `FileReader fileReader = new FileReader(myFile);`  
5. Create a new Object instance: `MyClass myClass = new FileReader(fileReader, Class.class);`  

Write-out a file:  

1. Find filepath: `File zorkFile2 = new File(path_to_file_output_file.json);`  
2. Use try-with-resources: `try(FileWriter zorkFileWriter = new FileWriter(zorkFile2)) {...}`  
3. The try-with-resources codeblock contains the rest of the code.  
4. Implement the resource and Exceptions will be caught: `gson.toJson(newZork, zorkFileWriter);`  

### Wednesday Code Challenge

Zip-up 2 linked lists!  
Manage your pointers and references.  
Use a TEMP variable!  
MAINTAIN refs to the nodes with access to the rest of your Linked Lists.  

## Thursday 26-May Discussion Topics

The only time you need to use the TypeToken type, is when getting a collection of JSON objects using the Gson package.  
Whenever you make an API call that returns a JSON Array, it will be enclosed in `[ ]` and the TypeToken code will be *required*.  
With GSON, using a Class to schema the data, a constructor is *not required*.  

### HTTP Interaction

Create fun and interactive websites, not single-page static sites.  
UI vs UX: User Interface is one thing, User *Experience* design interactive, intuitive user interfaces, especially websites.  
UX Designers study user psychology and design patterns for useability and interactiveness.  
HttpUrlConnection: Class we will use, based on advice from Baeldug.com, but we'll include Try-With-Resources.  

#### Goals for Today

1. Pick an API - We will use PokeAPI here
2. Get a URL - Check the documentation to find out the URL(s) then set it in code: Java has a type "URL" e.g. `URL pokeURL = new URL(stringURL);`
3. Connect to a URL - Typecast to HttpURLConnection type: `HttpURLConnection myConnection = (HttpURLConnection) myURL.openConnection();`
4. Read contents at the URL (dont forget to manage/handle HTTP Response Codes)
5. Convert/Instantiate objects based on response - We will use "wrapper classes"

Wrapper Classes:

- Follow the naming convention "Wrapper" + jsonObjectName
- Define the WrapperObj properties and other Wrapper Objects within it

Two primery methods of getting data from APIs:

1. REST Method: Get everything from the API  
2. GraphQL Method: Only get the data you specifically want from the API  

#### RESTful Commands

GET: Query, no payload (data) is sent to the API but response is required.  
PUT, PATCH, and DELTE: Action methods that require data to be sent TO the API.  

### Advice Going Forward

Use '_inputName' to name your method input parameters.  
Use '_recursiveFunc' to name your recursive functions.  
Utilize HTTP Status Codes in your REST calls so they are more easily testable.  

## Footer

Return to [Parent Readme.md](../README.html)  
