# Generics

Generics are used in Java, C#, and other strongly typed programming languages. Following are some notes and lessons learned about them.

## Java Tutorials Notes

### Basics

'Generics add stability to your code by making more of your bugs detectable at compile time.' *[The Java Tutorials]*

- Compile-time errors are easy to detect. Between the IDE and the compiler, you'll get a notice.
- Run-time errors are more difficult to detect or anticipate. Generics help in this regard.
- Type Safety: Issues with type safety are caught at compile-time.
- Casting Risks: Un/Boxing operations can be expensive.
- Enhance Algorithm capabilities: By using Generics, an Algorithm can work on collections of different objects, easily, and in a more readable way.

Generics enable Types to be Parameters.

Apply Generics to Classes, Interfaces, and Methods.

Formal Parameters: Strongly-typed parameter that is a *value* i.e. `Integer weight`.

Type Parameters: Generic parameters are parameters that are *types* i.e. `T object`.

Keyword 'T': Used as a placeholder for the Type that will be used in the Generic Class, Interface, or Function.

Raw Types: No type arguments are included with the instantiation of the Generic Type. The catch is Un/Boxing penalties apply, and unsafe code can execute at run time. Code is unsafe because Type Safety cannot be validated. Older APIs (Java 7 and earlier) will require use of Raw Types for backward compatibility reasons. Use `@SuppressWarnings` syntax for ignore Raw Types warning messages.

Methods use Type Inference to process generic parameters.

### Java Primitives

Primitives allocate less memory than Types.

Primitives cannot be used as a Type Parameter in the generic declaration.

Primitives can utilize comparison operators like '< > !=' etc, Types cannot.

List of Java SE 8 Primitives:

- short
- int
- double
- long
- float
- byte
- char

### Java Generic Type Invocation

Replace 'T' with a concrete non-Primitive or Reference Type Class.

```java
public class DSNode<T> {
  private T data;
  public DSNode(T payload) {
    this.data = payload;
  }
}
```

*Note*: Primitives can then be used as the Type in the Generic Class, Interface, or Method.

```java
int myValue = 11;
DSNode<Integer> myNode = new DSNode<>(myValue); // <-- DSNode will store an Integer, and a primitive int value is added
```

Create multiple versions of DSNode with different values:

```java
string myData = "This is a message.";
DSNode<String> messageNode = new DSNode<>(myData);

MyCustomType payload = new MyCustomType();
DSNode<MyCustomType> anotherMessageNode = new DSNode<>(payload);
```

Define static and non-static method's generic parameters using similar syntax:

```java
public class DSNode<T> {
  private T data;
  public DSNode(T payload) {
    this.data = payload;
  }
  public void setData(T newData) {
    this.data = newData; // <--
  }
}
```

### Bounded Types in Java

Allows restricting types that can be used in a parameterized type.

Sending a parameterized type of String when only a Number-type is expected will no longer work.

Example of a Bounded-type Parameter usage in a method:

```java
public <U extends Number> void process(U u) {
  ...
}
```

This enables compile-time warnings and errors when types are passed-in to the method that don't meet the bounded type declaration in the parameters list.

Multiple Bounded Types can be included in the same parameter:

```java
public <U extends Number & X1 & X2> void process(U u) {
  ...
}
```

Multiple Bounded Types in the Type Parameter list are sensitive to the inheritance chain. A Bounded Type following an Ampersand must be more-specific than the one preceeding it.

Use the OOP rule 'IS A' to determine if a primitive or Type will be allowed in a Bounded Types listing, and what order it should be within the Bounded TYpes listing.

*Note*: Integer and Double are NOT subtypes of Number, it is actually *the other way around*. Think of it this way: What is the common parent of the Types? If there is no common parent, than the Types will not be compatible with the Bounded Types list. Oracle Docs say to look at 'Wildcards and Subtyping' for details about this behavior and how to work with it.

### Primitive Operators in Java

Certain Operators *only work on primitive types* and therefore cannot be used to compare custom Types or Generic arguments that don't have their own Operator definitions or overrides.

Implement an interface i.e. `Comparable<T>` so `e.compareTo(elem) > 0` can be utilized.

### Subtyping in Java

Extend or implement a generic class or interface to *subtype* it.

Determination of a subtype are made within 'extends' and 'implements' clauses.

Extending a class to make it a 'subclass':

```java
public class Juice extends Liquid {
  ...
}
```

```java
public class Juice implements Pourable {
  // extend Interface Pourable here
  ...
}
```

### Common Naming Conventions (Java SE 8+)

Directly from *[Oracle JavaSE Tutorial: Java Generics]*

Use single, upper-case letters:

- E: Element
- K: Key
- N: Number
- T: Type
- V: Value

Multiple type placeholders? Use 'S', 'U', 'V', ...etc in the template diamond.

## References

[The Java Tutorials](https://docs.oracle.com/javase/tutorial/java/generics/index.html)

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
