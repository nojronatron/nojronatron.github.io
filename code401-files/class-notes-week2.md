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

## Code Review?


## Footer

Return to [Parent Readme.md](../README.html)  
