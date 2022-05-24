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

Inheritance introduces the instanceOf method.  
'instanceOf()' is used to determine inherited hierarchy of your current or custom classes at runtime.  

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

## Feedback Review

You *will* feel lost at times.  
Give yourself breaks from a project by timeboxing and then walking away for a while.  
Code Fellows is going to rapidly run through concepts that college-level classes take weeks and months to get through.  
What if you're behind? Finish the current days work before working on catchup labs/challenges/etc.  
Pair Programming!!  
Try code warmups to get going in the morning.  

## Tuesday Code Review

You will need to spend ~70% of your time whiteboarding a problem and only ~30% coding the solution!  
The order in which you reassign REFs to Nodes is *critical*.  
Always reassign the Head pointer LAST.  

## Typecasting

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
Similar to C# "Constraints"  

`public class Node<T extends MyClass> {...}`

### User Input and Data Flow

How do we know how the user is going to interact with our App/Packages?  
The WRRC and API modeling can help answer these questions.  
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

Why are these necessary?  
Interfaces are NOT Classes but they are instantiated similarly: 

`public interface iMyInterface {...}`  

Only implement logic and methods *as required*.  
To attach an interface to a Class, use the keyword "implements": 

`public class myClass implements iMyInterface {...}`  

Define members *without implementation* in your Interface definition.  
Classes that "implements" that interface *need to implement those member(s)* in order to compile.  
Interfaces enable reusability and are well suited in many-to-one scenarios.  
It is possilbe (and legal) to define a Class *within an interface*.  
Classes that *implement* an interface *must* define the implementations within the Class to meet the interface requirements.  
Classes can implement *multiple interfaces*.  

#### Loggers

Create a Logger interface that all of your classes implement to ensure logging in your App!  

#### Implementing Multiple Interfaces

```java
public class Zork extends Doggo implements Feeding, logger {
  // now implement the members required by Feeding and logger interfaces
}
```

## Tuesday Lab

[ ] Create a Domain Model first  
[ ] Try to use interfaces => ID where they will come in handy e.g. many-to-one relationships  
[ ] Step 1 Shouldn't take more than 30 minutes
[ ] Step 2 Consider using an abstract class or other modularization means to achieve goals  
[ ] Step 3 Movie Class creation is not required so do a String name if not Classing it  
[ ] Utilize Java built-in Packages as possible e.g. ArrayList.add() remove() etc  
[ ] Remember that specific Reviews could be for *many things* and ensure the "user" is able to enter the correct type of Review  
[ ] DO NOT write complex tests - 1 for each method is enough for Labs  

## Tuesday Code Challenge

More linked lists!  

## Schedule Through Memorial Day

Friday: Alex is out, so JB (or another) and Dr.Robin  
Monday: NO CLASS  
Homework will get shifted back by 1 day  
Fridays WILL NOT CHANGE  
There will be updates to cover for the missed day on Monday  

## Questions and Things to Think About

[ ] Project Idea: Try to develop a Linked List using javascript

## Footer

Return to [Parent Readme.md](../README.html)  
