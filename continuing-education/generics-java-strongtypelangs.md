# Generics

Generics are used in Java, C#, and other strongly typed programming languages. Following are some notes and lessons learned about them.

## Java Tutorials Notes

Baeldung states that Generics were added to Java in JDK 5.0. This explains why I wasn't already aware of them from college where I was introduced to Java at v.1.5, but the curriculum wasn't updated yet.

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

Raw Types: No type arguments are included with the instantiation of the Generic Type.

> The catch is Un/Boxing penalties apply, and unsafe code can execute at run time. Code is unsafe because Type Safety cannot be validated. Older APIs (Java 7 and earlier) will require use of Raw Types for backward compatibility reasons. Use `@SuppressWarnings` syntax for ignore Raw Types warning messages.

Methods use Type Inference to process generic parameters.

Non-generic Classes support generic Methods.

Due to Type Erasure, generics incur no runtime overhead, ensure type safety, and ensure only ordinary classes, interfaces, and methods will be produced in bytecode.

### Java Primitives

Primitives allocate less memory than Types.

Primitives cannot be used as a Type Parameter in the generic declaration at this time.

Primitives can utilize comparison operators like `<` `>` `!=` etc.

List of Java SE 8 Primitives:

- short
- int
- double
- long
- float
- byte
- char

Types can compare for value or equality by:

- Implementing the `compareTo()` method of `Comparable<T>`.
- Overriding `Object.equals()` method with a custom implementation.

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

*Note*: Primitives can then be used as the Type within the Generic Class, Interface, or Method.

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

A method signature of a Generic Method must include a generic type `<T>`:

```java
public class Processor {
  // static method is prefixed with a generic template <T>
  public static <T> void exchangeElements(T[] list, int left, int right) {
      T firstItem = list[left];
      list[left] = list[right];
      list[right] = firstItem;
  }
}
```

When a generic method will use multiple types, they can be listed in the method signature *[Baeldung.com/java-generics]*:

```java
public static <T, G> List<G> fromArrayToList(T[] arr, Function<T, G> mapperFunc) {
  return Arrays.stream(arr)
    .map(mapperFunc)
    .collect(Collectors.toList());
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

Leveraging abstract classes and methods allows definition of Bounded Wildcards in generics. Reminder of Inheritance:

```java
abstract class Animal {
  abstract void talk();
}
class Dog extends Animal {
  void talk() {
    System.out.println("Bark!");
  }
}
class Cat extends Animal {
  void talk() {
    System.out.println("Meow!");
  }
}
```

Here, Dog IS-A Animal, and Cat IS-A Animal too, so filtering a type by tye super class Animal, allows including Dog and Cat types.

Using Interfaces, a Type can be made to fit requirement by implementing expected members.

```java
interface Language {
  void speak();
}
class Terrier extends Animal implements Language {
  // dogs bark
  public talk() {
    System.out.println("Bark!");
  }
  // breeds bark in a dialect
  public speak() {
    System.out.println("Bow-wow!");
  }
}
class GermanShepherdDog extends Animal implements Language {
  void talk() {
    System.out.println("Bark!");
  }
  // GSDs have a deeper dialect
  public speak() {
    System.out.println("Woof!");
  }
}
```

More about this later.

### Java Type Inference

The Java Compiler uses a Type Inference Algorithm that:

- Figures out the type argument(s) necessary for a declaration.
- Selects *the most specific* type argument that works for all arguments.
- Uses invokation arguments, target types, and obvious expected return types of a Member to determine inferred Type.
- Does NOT consider returns or outputs later in the code to determine inferred Type.

Use the diamond `<>` symbol when instantiating a new generic class to avoid incidentally referencing the Raw Type.

Constructors can use Generics as well, and Type Inference can figure out the Type the same as described above.

During compilation the 'T' is replaced with 'Object' during Type Erasure (below).

### Type Witness Notation

When declaring a new Generic instance, the common syntax is:

```java
// taken directly from Oracle's Java docs on generic type inference
static <T> List<T> emptyList();
List<String> myList = Collections.emptyList();
```

Type Witnesses are placed in front of the instance declaration for readability:

```java
static <T> List<T> emptyList();
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

- In a return type. It is possible but the most specific Type should be declared for readability sake.

Bounded Wildcards are compiled-down to the bounded Type Parameter during Type Erasure (below).

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

public static void addToFamily(T<? extends Animal> pet) {
  // accepts dogs or cats based on abstract class defined earlier
}
```

#### Unbounded Wildcards

- AKA 'Unknown Type'
- Usage: `List<?>`
- Meaning: Method will *use functionality provided by Object class*.

Using an unbounded wildcard for an input limits members to that of the base class Object:

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

If `Object` were used instead of `?` the iterator would provide Object instances represented as a String, instead of returing the String representation of the Type actually stored at each element.

There are [Guidelines](https://docs.oracle.com/javase/tutorial/java/generics/wildcardGuidelines.html) and if/when Wildcard should be used.

Avoid using a wildcard on a method output as it will make the return type unknown and difficult to debug and work with.

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

Applying a lower-bounded wildcard to Animal `public void show(T<? super Animal>){...}` would result in only Animal and base class Object as acceptable types. Meaning neither Car nor Dog would be accepted as a wildcard matched type.

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

#### Guidelines for Wildcard use (Java)

Variables provide one of 2 functions:

- `In`: Serves data to the code. An IN parameter.
- `Out`: Holds data to be used elsewhere. An OUT parameter.

The In-or-Out-Principle:

- IN variable is defined with an *upper bounded wildcard* using 'extends' keyword.
- OUT variable is defined with a *lower bounded wildcard* using 'super' keyword.
- Use UNBOUNDED when: IN can be accessed using defined methods in Object class.
- Do NOT USE A WILDCARD in cases where code needs to access *both IN and OUT* variables.

Additionally:

- AVOID using wildcard in a Method Return Type (complicates code).

### Type Erasure in Java

See the docs for details, here are the highlights:

- Type Erasure removes all type parameters and replaces them.
- Type parameters are replaced by thier bounds.
- Unbounded type parameters are replaced with Object.
- Proper casting is applied (by the Compiler) to avoid casting mistakes.
- Primitives *do not extend Object* and so do not apply to Generics!

```java
// type parameters are replaced by their bounds
public <T extends Animal> void foo(T animal) {...};
// becomes...
public void foo(Animal animal) {...};
```

The following are just a few things to watch out for:

- The Compiler *might* create a synthetic method (aka Bridge Method), which could throw a ClassCastException. Avoid using Raw Types to avoid this situation.
- When Bridge Methods are created, Method Signatures could no longer match, which could throw a ClassCastException.
- Reifiable Types: Type information is fully available at Runtime (primitives, raw types, unbound wildcard invokations).
- Non-reifiable Types: Type information missing due to Type Erasure.

Non-reifiable Types example:

```java
public void addList(List<String> list) {...}
public void addList(List<Integer> list) {...}
// JVM cannot tell difference because these are Non-reifiable Types
```

Avoid using non-reifiable Types:

- In `instanceof` statements.
- As an element in an array.

Heap Pollution:

- A variable of a parameterized type refers to an object that is *not of that parameterized type*.
- An *unchecked warning* situation.
- Code contains mixed raw types and parameterized types.
- Code performs unchecked casts.

Possibly good advice: If you find yourself using `___` consider rewriting your code to avoid non-reifiable Types or incorrectly handling casts:

- `@SafeVarargs`: An annotation asserts the implementation will not improperly handle varargs formal parameter.
- `@SuppressWarnings({"unchecked", "varargs"})`: Suppresses unchecked and varargs warnings. Not advisable.

### Java Generics Restrictions

Things you *cannot do* with Java Generics:

- Instantiate using primitive types. *Instead* of `char` use `Character`, etc.
- Create instances of Type parameters. The *Type Parameter is a hint* for the compiler, not a concrete Type.
- Declare static fields using Type parameters. Static fields are *class-level variables*.
- Use casts or `instanceof` with parameter types. Type Erasure makes this impossible execution at runtime.
- Create Arrays of parmeterized types. A list of a list cannot be an Array of Objects containling List of type T.
- Create, Catch, or Throw Objects of Parameterized types. Generic *Classes* cannot extend `Throwable` Class directly or indirectly.
- Overload a method where the formal parameter types of each overload get 'erased' to the same raw type.

*Note*: A method *can* throw a placeholder type e.g. `public void parse(File file) throws T {...}`.

*Note*: Method overriding *must* use type parameters that won't cause the methods to have the same signature after Type Erasure.

```java
// before type erasure
public void print(Set<String> set) {...}
public void print(Set<Integer> set) {...}
```

```java
// after type erasure
public void print(Set set) {...}
public void print(Set set) {...}
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

Oracle's [Java Tutorials](https://docs.oracle.com/javase/tutorial/java/generics/index.html)

Baeldung: [Java Generics](https://www.baeldung.com/java-generics)

Baeldung: [Comparing Objects in Java](https://www.baeldung.com/java-comparing-objects)

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
