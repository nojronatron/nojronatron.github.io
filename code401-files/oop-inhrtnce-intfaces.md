# Reading Notes OOP Inheritance and Interfaces

## References

OOP Q&A Source on [Oracle Docs](https://docs.oracle.com/javase/tutorial/java/concepts/QandE/questions.html)  

About Interfaces docuemntation by [Oracle Docs](https://docs.oracle.com/javase/tutorial/java/concepts/interface.html)  

About Inheritance documentation by [Oracle Docs](https://docs.oracle.com/javase/tutorial/java/IandI/subclasses.html)  

## OOP QandA

Real world objects contain ____ and ____ ?

> State (data) and functionality.  

A software object's state is stored in ____ ?

> Properties.  

A software object's behavior is exposed through ___ ?

> Methods.  

Hiding internal data from the outside world, and accessing it only through publicly exposed methods is known as data ____ .

> Encapsulation.  

A blueprint for a software object is called a ____ ?

> Class.  

Common behavior can be defined in a ____ and inherited into a ____ using the ____ keyword.  

> Interface  
> Class  
> Implements

A collection of methods with no implementation is called an ____.  

> Interface.  

A namespace that organizes classes and interfaces by functionality is called a ___.  

> Package.  

The term API stands for ____?  

> Application Programming Interface.  

## Interfaces

Contracts: Spell out how software will interact.  
Utilize interfaces to write code that interacts with other code *without concern for how the details are implemented within the other code package*.  

Interfaces:  

- ARE a REFERENCE TYPE  
- Only contain: Constants; method signatures; default methods; static methods; nested types.  
- Do not contain method bodies except for *default methods* and *static methods*.  
- Cannot be instantiated, only *implemented* by other classes.  
- Can be *extended* by other interfaces.  

Use Interfaces as APIs so that other code/packages can use your code without having to know or understand your implementations.  

### Define a new interface

```java
public interface MyInterface {
  int alpha(Object obj);
  void storeThing(double number);
  // all of the above are method signatures without implementation
}
```

### Implement an Interface

```java
public class MyClass implements MyInterface {
  public int alpha(Object obj) {
    // code to implement MyInterface method 'int alpha'
  }
  // it is REQUIRED to implement other interfaces here
}
```

## Inheritance

Java's Inheritance model starts with the class "Object" at the root of all other objects.  
Inheritance allows other Classes to re-use code from a parent Class.  
Use *extends* keyword to leverage inheritance in your custom Classes.  
Many common *base methods and properties* are made available through this hierarchy starting with 'Object'.  

### Subclassing Enablements

Inherited fields can be used directly, just like the Classes' own fields.  
Declaration of fields in the subclass can use the same name as the superclass (inherited class).  
New fields can be declared that are not already in the Superclass.  
Inherited methods can be used directly by the inheriting Classs.  
New instance methods can be written in the subclass with the *same signatures* as the one in the Superclass (method hiding).  
New methods can be declared in the inheriting class that do not already existin in the Superclass.  
A subclass constructor that invokes the superclass constructor can be written using the keyword *super*.  

#### Limitations and Things to Note

Reusing a Superclass Field name will *hide it* and is *not recommended*.  
Inheriting classes do *not* inherit *private members* of the Superclass.  
A *nested class* has access to private members of its *enclosing class* including private Fields and Methods.  

#### Casting Objects

Subclasses are cast *of the superclass type* (Polymorphism).  
A subclass can be instantiated *of the superclass type* such as `Mountainbike mb = new Bike(...);`  
A *promise* can be made when casting an object of a distant super-class so the compiler doesn't throw, e.g. `Mountainbike mb = (MountainBike)obj;  

## Footer

Return to [Parent Readme.md](../README.html)  
