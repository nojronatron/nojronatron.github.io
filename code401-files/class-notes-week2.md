# Class Notes Week 2

23-May through 27-May 2022

## Monday Discussion

Inheritance: Super and Extends => Create sub-classes.

Abstraction: Abstract Classes => Stepping "out one layer" from doing the actual thing.

DRY: Code modularization => Don't Repeat Yourself => Why keep writing the same code over and over?

Object hierarchy: Built-in methods get inherited down the tree.

Everything is Java is either a Class aka Object aka REF type, or a Primative.

Type casting: Upcasting (free in Java) and Downcasting (manual)  
Instance of: IS-A => Is this Type type an instance of AnotherType.

Arguments: Have actual value and are set when a method is called.

Parameters: Are placeholders for Arguments that are expected as method inputs.

Primatives: Long, Double, Short, Char, Integer, Decimal, Float, Byte, Boolean.

Keyword 'this': Use to limit the scope, i.e. within a Constructor or inside a specific Class and not it's base or Parent Class.

Objects do NOT have a 'this' keyword, but CLASSES need this.

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

Inheritance introduces the 'instanceOf()' method. It is used to determine inherited hierarchy of your current (or custom) class at runtime.

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

## Tuesday Code Review

You will need to spend ~70% of your time whiteboarding a problem and only ~30% coding the solution!

The order in which you reassign REFs to Nodes is *critical*.

Always reassign the Head pointer LAST.

## Typecasting

Recall primitives  and references are core aspects of Java's Type system.

Two types:

1. Widening Casting aka Upcasting. This is automatic. Converts *smaller* type to a larger type.
2. Narrowing Casting aka Downcasting. Must be implemented by developer. Convert larger type to smaller size type.

For example, an int fits inside a double (lossless conversion) but a double does not fit inside an integer (lossy conversion, requires implementing a conversion process).

Casting sub-class to super-class => UPCASTING.

- Performed implicitly by the compiler.
- Related to inheritance.
- Reference variables are commonly used to refer to a more specific type.

Notes about Upcasting:

- REF variables can refer to an object if obj is of same type as var.
- REF variables can refer to an object if obj is a *subtype*.
- Java objects are polymorphic by default.

Downcasting is the process of casting "from a superclass to a subclass".

- Use lots of extra parentheses to perform the downcast operation.
- Leverage `instanceOf(subclass)` in an IF statement before downcasting!
- Compiler *will not always catch downcast exceptions*, but the runtime will (ClassCastException).

Supplemental comments were added from these resources:

- [w3schools](https://www.w3schools.com/java/java_type_casting.asp)
- [article at Baeldung.com on java type casting](https://www.baeldung.com/java-type-casting)

### The Cast Method

Use MyClass.class.cast(superClassRef) and MyClass.class.isInstance(superClassRef).

- Use `cast()` and `isInstance()` methods together.
- Useful when dealing with generics.

Supplemental comments were added from an [article at Baeldung.com on java type casting](https://www.baeldung.com/java-type-casting)

## Generics

What are Generics?

- Basic idea is a non-specificy type can be placeheld for what could be used at Runtime.  
- The requirement to define the exact Type is not required during design time.  

```java
public class Node<T> {
  public T value; // value of node
  public Node<T> next; // generic Node with type T
  public Node(T value) {
    this.value = value; // works within constructors and methods
  }
}
public class LinkedList<T> {
  public Node<T> head = null;
  public Node<T> tail;
  public void insert(T val) {
    Node<T> newNode = new Node(val);
    if (head != null) {
      newNode.next = head;
    }
    if (head == null) {
      tail = newNode;
    }
    head = newNode;
  }
  ...
}
```

### Generic Extensions

Class Number is the parent to int, long, float, double, etc.

Restricts the Types to certain super and child types, rather than the entire Java Libraries types.

Similar to C# "Constraints".

`public class Node<T extends MyClass> {...}`

### About Generics And Casting

Check out [this article at Baeldung.com on java type casting](https://www.baeldung.com/java-type-casting) for information about casting within generic methods to safely handle generic types.

At the bottom of the article is a demonstration unit test that verifies only the correct type is handled in the generic method under test.

### User Input and Data Flow

How do we know how the user is going to interact with our App/Packages? The WRRC and API modeling can help answer these questions.

We will also need to consider validating input, etc.

All of this will get revisited in a future class.

For now just keep in mind user-input and output are impotant aspects with code design.

### Code Design and Data Relationships

One to One: 1:1 =>  Each pair of items are directly related to each other and only each other.

One to Many: 1:Infinite => The single has many, many links to other items but each item has only one link to the one.

Many to Many: Infinite:Infinite => Many Items have many links to many other items.

What does good coding practices say about a class that is used A LOT? Modularize it!

Consider whether releated objects have a relationship that indicates whether inheritance with sub-classing or abstract classes etc are necessary.

### Interfaces

Why are these necessary? An *interface* is like a contract, that guarantees a class or Type will have certain members.

Interfaces are NOT Classes but they are instantiated similarly: `public interface iMyInterface {...}`

Only implement logic and methods *as required*.

To attach an interface to a Class, use the keyword "implements": `public class myClass implements iMyInterface {...}`

Notes:

- Define members *without implementation* in your Interface definition.
- Classes that "implements" that interface *need to implement those member(s)* in order to compile.
- Interfaces enable reusability and are well suited in many-to-one scenarios.
- It is possilbe (and legal) to define a Class *within an interface*.
- Classes that *implement* an interface *must* define the implementations within the Class to meet the interface requirements.
- Classes can implement *multiple interfaces*.

#### Loggers

Create a Logger interface that all of your classes implement to ensure logging in your App!  

#### Implementing Multiple Interfaces

```java
public class Zork extends Doggo implements Feeding, logger {
  // now implement the members required by Feeding and logger interfaces
}
```

## Tuesday Lab

- Create a Domain Model first
- Try to use interfaces => ID where they will come in handy e.g. many-to-one relationships  
- Step 1 Shouldn't take more than 30 minutes
- Step 2 Consider using an abstract class or other modularization means to achieve goals  
- Step 3 Movie Class creation is not required so do a String name if not Classing it  
- Utilize Java built-in Packages as possible e.g. ArrayList.add() remove() etc  
- Remember that specific Reviews could be for *many things* and ensure the "user" is able to enter the correct type of Review  
- DO NOT write complex tests - 1 for each method is enough for Labs  

## Tuesday Code Challenge

More linked lists!

## Questions and Things to Think About

- [ ] Project Idea: Try to develop a Linked List using javascript

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

Robert C. Martin and Michael Feathers are credited with building these principles while developing software design patterns.

Single Responsibility: A class should have one job. There should only be one reason to change.

- Reduces test cases.
- Lowers dependencies and "coupling".
- Smaller, more simply organized classes result.

Open-Closed: Open for extension, Closed for modification.

- Stop modification of existing code, which could introduce new bugs.
- Only modify existing code *to fix bugs*.
- Extend classes to build-out functionality/features.

Liskov Substitution: Related to polymorphism.

- "If class A is a subtype of class B, then class B can be replaced by class A without disrupting program behavior."
- Rework models into interfaces that will handle differences in types, so they are polymorphically adaptable.

Interface Segregation: Larger interfaces should be split into smaller ones.

- Implementing classes only need to be concerned with methods that are of interest to them directly.
- Developing smaller, more specific interfaces allows defining smarter contracts that are more easily maintained and better describe required functionality.

Dependency Inversion: Decouple software modules, and depend on abstractions.

- When defining specific Types for a Class Field, instead use an interface to support changing requirements but still meet the internal requirements of the Class holding the Field.
- Decouple Classes by using abstraction to allow using any test framework.

This section was completed by taking notes from [Baeldung.com article on solid principles](https://www.baeldung.com/solid-principles)

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

GSON is an external package: Google Script Object Notation.

- The gradle config has a dependency codeblock that defines the required packages for build (and test).
- JSON is consumed via several ways: Files, Internet, Resources (e.g. libraries, DBs, etc).
- JSON is fast and thin compared to other data types.
- Serialization: Translate INTO JSON format. Makes it easier to XMIT data via the web/network.
- Deserialization: Extract the data from JSON format into an Object or Collection of Objects.
- JSON is plaintext, therefore a String, and WYSIWYG.

Lab Goal today: Read-in a JSON file using GSON.

When reading-in JSON, you will need to have a Class instance to push the imported data into (members etc).  

Design:

- App imports Files: `implementation 'com.google.code.gson:n.n.n'` => add this (and more) to build.gradle.
- Import GSON: `import com.google.gson.Gson;`
- Rebuild: Reset Gradle (use a build command) to ensure build.gradle changes are picked up.
- Test => resources directory: Allows Tests easy access to the files during test writing and execution.
- Read-in a file: 

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

- Use '_inputName' to name your method input parameters.
- Use '_recursiveFunc' to name your recursive functions.
- Utilize HTTP Status Codes in your REST calls so they are more easily testable.
- Use Baeldung's examples to put together REST operations in Java.
- Always put Stream Reader types inside of a Try-with-resources e.g. `try (BufferedReader responseReader = new BufferedReader(args)) {...}`: This auto-closes (garbage-collects) the enclosed resources automatically.
- Define Methods to return things like StringBuffer so the caller gets the data wholesale.
- Try to return HttpConnection types in your methods so the caller can utilize the response codes, etc.
- Case Sensitivity between JSON object parameters and Class properties MUST MATCH.
- Describe the Schema of what you are expecting to get back from the REST Call.
- If the JSON data contains collections, your Schema will need to include `ArrayList<T>` and nested Classes that define T in order to fully model the JSON data.

Heads: Linked Lists.  
Tops: Stacks have these.  
Front: Queues have these.  

### Recursion

There are two methods of traversal:

1. Iteration: Loops, While, ...
2. Recursion: Function calls itself Directly or Indirectly  

A function that calls itself is a Recursive Function.  
Direct Recursion: Method calls itself.  
*Remember*: The Call Stack is a LIFO system and recursive functions take advantage of that.  
Indirect recursion: A helper function is called by the 1st function that recurse-calls from there.  
*Note*: At every single iteration the base-case MUST BE TESTED.  
Base Case: Tells recursion when to stop.  
Recursion does *not* allow 'break' and 'return' statements.  

## JB Tellez Stacks and Queues

Execution or Call Stack: First In Last Out frames. It's a stack!  
Getting back to something is pretty easy in a stack, compared to a willy-nilly random pile. 
When the Call Stack is empty, the program is over / closed.  
Queues are First In First Out: Formally ordered front to back.  
With queues you put things in the front, and take things out of back/end?  

### Terminology

Stack

- Consisted of Nodes, similar to (or the same) as LinkedList Nodes.
- PUSH: Only puts things on TOP of the stack. Handles VALUES *only*!
- POP: Remove the last-in item from the "top" of the stack. *Could* throw an exception if stack is empty/null, but depends on the implementation.
- IsEmpty: Check the Stack if it is empty *before* trying to Pop it. Can use Try-Catch and handle any exception would be an implementation.
- Top: The top of the stack.  
- Peek: What's there at the top of the stack, without Popping it.

FILO

- First In Last Out
- Same a LIFO just flipped around
- The Top's Next is the Node that USED TO BE THE TOP

Pseudo Code for Push and Pop: See the DS&A Class-10 => resources => stacks_and_queues.md

*Important*: Be sure to update the this.top property with PUSH and POP operations:

- Top: private property that tracks the last-in Node reference, or null if there are no nodes
- Initial state of Stack: Empty list.head needs to be set to null
- Implement an isEmpty method to test the state of this.top and return true if null, false if has Node
- Push: Newly created node.next points to head, and then head is pointed to newly created Node
- Pop: head Node value is stored, then head pointer is moved to head.next, then value is returned to the user
- Implement a peek method to return the value of top only if isEmpty is false

Queue

- Queues have *two ends*: Front and Rear
- FIFO: First In First Out
- Enqueue: Nodes are items that are added to the *rear* of the queue
- Dequeue: Remove the FRONT Node from the QUEUE
- Front: Same as Rear when there is only one Node. Always the "next" node ready to be DEQUEUEd
- Rear: The last Node that was ENQUEUEd into the Queue
- Peek: Preview the value of the FRONT Node
- IsEmpty: Return True if QUEUE size is 0, False if > 0

The Next property of each Node points *toward the Rear* and *toward the Enqueue side* of the Queue.  
Rear.next will always equal NULL.  

### Calendar Planning

Due Today:

1. Prep work: Career Coaching Personal Pitch and Stage Fright assignments  
2. Code Challenge: Partner interviews  
3. Lab: Partners to call an API (Quote APIs). Refactor any code from previous lab to prepare for this lab  
4. 9am Friday Zoom: Dr. Robin; 1215 Power-Hour Session; 2pm Zoom: Stacks and Queues with JB Tellez; Feedback assignment(s) too
5. Monday: NO CLASS
6. Networking appointments are coming due: 1:1 in-person or remote, outside of this class. Targeted company interview counts!  

## Footer

Return to [Parent Readme.md](../README.html)  
