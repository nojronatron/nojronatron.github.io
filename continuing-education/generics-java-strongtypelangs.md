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

Non-generic Classes support generic Methods.

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

*Note*: Integer and Double are subtypes of Number, but when used with Generics, the generic class T, whether Integer or Double, are not. Think of it this way: What is the common parent of the Genericized Type? If there is no common parent, than the Types will not be compatible with the Bounded Types list. Oracle Docs say to look at 'Wildcards and Subtyping' for details about this behavior and how to work with it.

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

### Java Type Inference

The Java Compiler uses a Type Inference Algorithm that:

- Figures out the type argument(s) necessary for a declaration.
- Selects *the most specific* type argument that works for all arguments.
- Uses invokation arguments, target types, and obvious expected return types of a Member to determine inferred Type.
- Does NOT consider returns or outputs later in the code to determine inferred Type.

Use the diamond `<>` symbol when instantiating a new generic class to avoid incidentally referencing the Raw Type.

Constructors can use Generics as well, and Type Inference can figure out the Type the same as described above.

### Type Witness Notation

When declaring a new Generic instance, the common syntax is:

```java
// taken directly from Oracle's Java docs on generic type inference
static <T> List<T> emptyList();
List<String> myList = Collections.emptyList();
```

Type Witnesses are placed in front of the instance declaration for readability:

```java
static<T> List<T> emptyList();
List<String> myList = Collections.<String>emptyList(); // <--
```

When Type Witnesses are not used, the compiler relies on Type Inference algorithm to figure it out.

Another example where Type Inference will chose 'Object' incorrectly unless a Type Witness is included:

```java
// starter method code
static <T> List<T> emptyList();

// will not compile in JSE 8 and earlier because the Type cannot be inferred in the invocation or return
processStringList(Collections.emptyList());

// will compile because the Witness Notation was included
processStringList(Collections.<String>emptyList());
```

### Wildcards in Java Generics

Wildcard Syntax: `?`

Wildcard is a placeholder for an 'unknown type'.

Can be used as a Type in a parameter, field, or local variable.

Avoid using wildcards:

- In a return type. It is possible but the most specific Type should be declared for a return Type.

#### Upper Bounded Wildcards

- Relax restrictions on a variable.
- Usage: `List<? extends String>`
- Meaning: 'Wildcard Extends UpperBoundType'
- Keyword 'extends' applies to both extending a Class and 'implements' an Interface.

```Java
// bounded to List<String>
public static void process(List<Number> list) {
  ...
}
// less restrictive, allowing subtypes including Integer
public static void process(List<? extends Number> list) {
  // this can accept a list of any sub-class of Number
}
```

#### Unbounded Wildcards

- AKA 'Unknown Type'
- Usage: `List<?>`
- Meaning: Method will use functionality provided by Object class.

Example of a Class that does NOT require type T:

```java
public static void printList(List<?> list) {
  // list.size() interrogates a List property size (length) 
  // Types stored within the Collection are ignored
  System.out.println("list size is %s%n", list.size());
  // also note that any Type that has a toString method can be accessed
  for (Object item: list) {
    System.out.println("%s ", item);
  }
  System.out.println();
}
```

If `Object` were used instead of `?` the iterator would provide Object instances instead of returing the String representation of the Type actually stored at each element.

There are [Guidelines](https://docs.oracle.com/javase/tutorial/java/generics/wildcardGuidelines.html) and if/when Wildcard should be used.

#### Lower Bounded Wildcards

- Restricts the unknown Type to be a specific 'Super Type' of that Type.
- Usage: `List<? super String>`
- Meaning: 'Wildcard IS A Super Type of LowerBoundType'
- Keyword 'super' ensures the Lower Bound Type is the most derived, and any parent Classes to the Lower Bound Type are acceptable.

```java
public void printList(List<Integer> items) {
  //  limited to an Integer Type
}

public void printList(List<? super Integer>) {
  //  supports Integer, Number, and Object,
  //  anything that holds Integer values
}
```

#### Wildcards and Subtyping

When one Class A 'IS A' Class B (such as through the 'extends' keyword), the extended Class is the super, and the extending Class is the inheritor.

The documentation example states:

```java
class A {}
class B extends A {}
B b = new B();
A a = b; // possible because B extends A
```

BUT when used as a Type Parameter:

```java
List<B> lb = new ArrayList<>();
List<A> la = lb; // compile-time error
```

The problem is `List<?>` is the common parent, not `A`.

Therefore, use an upper-bounded wildcard:

```java
List<? extends Integer> intList = new ArrayList<>();
List<? extends Number> numList = intList(); // OK
```

This is because `List<? extends Integer>` is a subtype of `List<? extends Number>`.

#### Wildcard Capture and Helper Methods

The compiler infers a particular type from the code when using Wildcards.

It is probably a good idea to assume the Compiler will guess the type is 'Object' if it isn't made apparent.

A private helper method should be implemented so Type inferrence will work properly (from the Oracle Docs):

```java
public class WildcardFixed {
  void foo(List<?> i) {
    fooHelper(i);
  }

  // by convention name Helper Methods after the member they are for
  private <T> void wildcardFixedHelper(List<T> list) {
    list.set(0, list.get(0));
  }
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
