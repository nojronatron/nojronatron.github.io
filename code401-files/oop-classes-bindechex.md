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

## About getClass() and .class

The getClass method: `objectInstance.getClass()`  
Using any direct instance of `objectInstance`, '.getClass()' returns the Class from which the instance was instantiated.  
Per Oracle's documentation: "Returns the runtime class of this Object."

The .class property: `ObjectType.class`  
Returns an Object that *represents* the ObjectType class.  

There is interesting conversation about these members in [this StackOverflow discussion](https://stackoverflow.com/questions/15078935/what-does-class-mean-in-java)  

Both members are defined within API java.lang.Object, the top Class in the Java hierarchy.  

See Oracle's documentation on [Java Classes](https://docs.oracle.com/javase/7/docs/api/java/lang/Class.html) for more details.  

Documentation of Spring and a few HTTP-oriented libraries we've looked at recently.  

## Reference: Classes Discussion

[Classes discussion by Oracle](https://docs.oracle.com/javase/tutorial/java/javaOO/classes.html)  

## Binary Decimal and Hexadecimal

Binary, Decimal, and Hexidecimal reading by [MathIsFun](https://www.mathsisfun.com/binary-decimal-hexadecimal.html)  

Decimals are 10-base numbers.  
Digits have positions, arranged around a decimal point.  
Every position is 10x bigger to the left, or 1/10th the value to the right of the decimal.  

### Different Number Systems

Other number systems count using a base other than 10.  
Hexadecimal numbers are base-16.  
Binary numbers are base-2.  
Regardless of the numbering system, once you know the base, you know when to "carry a one" by this algorithm:

```pseudo
while: number % base_system != 0 {
  increment: +1
}
shift: stack a 1 in the 2nd digit position and reset the 2nd digit position to 0
```

### Hexadecimal

A base-16 system.  
Numbers are 0-9 with A-F for the 11th through 16th values.  

```text
0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F
```

#### Convert Hexadecimal to Decimal Algorithm

Source [Permandi.com FP HTML Tips](https://www.permadi.com/tutorial/numHexToDec/index.html)  

1. Get the *last digit* of the hexideciaml number and call this digit the *current digit*.  
2. Make a variable called *power* and set it to 0.  
3. Multiply the *current digit* with `16^power` and store the result.  
4. Increment *power* by 1.  
5. Set the *current digit* to the previous digit of the hexadecimal number.  
6. Repeat steps 3 through 5 until all digits have been multiplied.  
7. Sum all of the result of step 4 to get the answer.  

#### Convert Decimal to Hexadecimal Algorithm

Source [Permandi.com FP HTML Tips](https://www.permadi.com/tutorial/numDecToHex/)  

1. Divide decimal number by 16. Tret the division as an integer division.  
2. Store the remainder as a Hexadecimal number.  
3. Divide the result again by 16. Treat the division as an integer division.  
4. Repeat steps 2 and 3 above until result is 0.  
5. The hex value is teh digit sequence of the *remainders* from *last to first*.  

## Footer

Return to [Parent Readme.md](../README.html)  
