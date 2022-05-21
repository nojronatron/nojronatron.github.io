# OOP Classes Binary Decimal Hexidecimal

## Reading Materials

### OOP Principles - Oracle Docs

[Object Oriented Programming Principles by Oracle](https://docs.oracle.com/javase/tutorial/java/concepts/)  

#### What Is An Object?  

Characteristics of objects: State and behavior.

State: What an object *is*, or the data it stores, e.g. React State.  
Behavior: What an object can *do*, or the capabilities is has, e.g. React Render or Callback Functions.  

"""
Bundling code into individual software objects provides...benefits:

1. Modularity: Write and maintain code independently of other objects or code pages.  
2. Information Hiding: Details of internal implementation are hidden from outside world.  
3. Re-use: Use existing objects in your program.  
4. Pluggability and debugging ease: If a particular object turns out to be problematic...remove it from your app and plug in a different object as its replacement.  
"""

All above skimmed from *[Oracle Docs (see link above)]*

#### What Is A Class?

Objects are built using a Class to create individual *instances*.  
Define a Class from which many Object Instances can be created without writing much code.  

#### What Is Inheritance?

Common details between objects can be identified between them.  
There is no need to re-write the same properties or methods for classes that share those same members.  
Instead inheritance allows creating Classes *which reusing existing "parent class" members*.  
Inheritance enables creating a single "parent" or "root" class, then creating "child" classes that automatically get access to Members from their parent class.  
Reduces code writing.  
Enables rapid object instantiation.  
Keyword: EXTENDS.  

```java
class ParentClass {
  ...
}
class ChildClass extends ParentClass {
  ...
}
```

#### What Is An Interface?

An interface describes required Methods that a Class guarantees will be implemented.  
I have heard in the past that Interfaces can be considered "contracts" so the code knows what capabilities a Class will have.  
Keyword: IMPLEMENTS.  

```java
interface Parent {
  // the following methods are not implemented
  // the members must still define a return type and any strongly types parameters
  void methodOne();
  void methodTwo(int number);
  String methodThree();
  Boolean isMethodFour(Double bigNum);
}
class MyParent implements Parent {
  public void methodOne() {...};
  public void methodTwo(int number){...};
  public String methodThree(){ return "Returning a String"; };
  public Boolean isMethodFour(Double bigNum) { return bigNum > 0;};
}
```

#### What Is A Package?

"""
...is a namespace that organizes a set of related classes and interfaces.
"""

The above is skimmed from *[Oracle Docs (see link at head of this section)]*  

Libraries are called "Application Programming Interfaces" or APIs.  
Many files and entire directory hierarchies can be stored in packages to define a set of state and functionality that other Applications can make use of.  

Note: There is an entire Oracle website dedicated to the [Java SE 8 API Specification](https://docs.oracle.com/javase/8/docs/api/index.html)  

## Classes Discussion

[Classes discussion by Oracle](https://docs.oracle.com/javase/tutorial/java/javaOO/classes.html)  

## Binary Decimal and Hexidecimal

Binary, Decimal, and Hexidecimal reading by [MathIsFun](https://www.mathsisfun.com/binary-decimal-hexadecimal.html)  

TBD...

## Footer

Return to [Parent Readme.md](../README.html)  
