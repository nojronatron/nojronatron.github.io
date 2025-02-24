# DotNET CSharp Stuff

Notes on C# usage and capabilities, with additional related .NET details.

## Table of Contents

- [Records, Structs, and Classes](#records-structs-and-classes)
- [Custom Extensions aka Extension Methods](#custom-extensions-aka-extension-methods)
- [About Aggregation and Composition](#about-aggregation-and-composition)
- [For ForEach While DoWhile](#for-foreach-while-dowhile)
- [Null Safety in CSharp Overview](#null-safety-in-csharp-overview)
- [Setting Nullability In Your Code](#setting-nullability-in-your-code)
- [Null Operators](#null-operators)
- [Best Practices Handling Nullability](#best-practices-handling-nullability)
- [References](#references)
- [Footer](#footer)

## Records, Structs, and Classes

Reference: [Carl Franklins DotNet Show 13 on GitHub](https://github.com/carlfranklin/dotnetshow-13)

Classes:

- Can have initializers.
- Creates a reference type.
- Created on the Heap. An area of memory belonging to an Application, accessible by all threads, where all Reference Types and all values contained within a Reference Type.
- Use when a reference is needed to a single source of truth.
- Instantiation yields a reference type.
- More commonly used than Structs.
- Hash Codes uniquely ID an object in the Head. `Equals()` uses this fact to compare objects.
- ReferenceQuals leverages the __memory location__ in the heap to identify same-ness.
- `Equals()` can be overridden to determine how an instance is considered equal, using the instance _value types_ after confirming instances are not null. This overrides equality check to look at the values, instead of looking at the referenced memory location.

Structs:

- Creates a value type.
- Created on the Stack (a stack of values and pointers). An execution thread only operates on the "top" item in the stack.
- Common structs: Point, Rectangle, Color. Small-bits of information containing value-types that will make-up a thing.
- Created on the Stack.
- Use to express sets of value types that represent something.
- `Equals()` determines structs are the same if the values are the same.

> When comparing Value Types, it is the _value_ that is being compared.

Records:

- Can be a Class (ref type) or a Struct (value type), in C# 10 and later.
- By default _is a Class_ (prior to and through C# 10).
- Similar to classes, with the benefit of built-in `Equals()` override that checks values instead.
- Positional Syntax is supported.
- Creating and setting values is done similarly to using a Class instance Getters and Setters.
- Are Mutable by default.
- Define as a struct: `public record struct RecordName {}`
- When defined as a struct, is _immutable_.
- Pretty output using built-in formatting that is JSON-like.
- Can inherit from other Records.
- Classes are not inheritable, nor can they inherit from a Record.
- Records can be used in place of a Class.
- Record Structs can be used in place of a Struct.

Constraints:

- No generic constraints that require a Record specifically, so cannot be applied to meet the definition exactly.
- Records statify either the Class or Struct constaint.
- Therefore, you can use a Record in place of a Class, and a Record Struct in place of a Struct.

The `with` expression:

- Operates on Records.
- Creates a new Record using an existing record.
- "Non-destructive mutation"
- Records remain immutable.

A Record Struct is the same as a Struct with the following benefits:

- Can be defined with positional syntax.
- Can use `with` expression for non-destructive copying.
- Much better performance than a Class or a Struct.

Immutability is not always appropriate, but is more and more believed to be a good thing.

- Make a Class immutable by eliminating setters from the Properties.

The Init Keyword is used in place of a setter, and relinquishes the requirement to have a CTOR.

### When to Use Records, Structs, and Classes?

- Need a reference type: Use a Class or Record Class.
- Use a Record to get the Equality feature of a Struct without overriding `Equals()`
- Use a Record to enforce immutability with less code.
- Use a Record Struct to leverage positional syntax or the `with` expression for non-destructive duplication.
- Use a Record Struct if performance is a primary requirement.

## Custom Extensions aka Extension Methods

Custom extension methods can be created for any class.

- Introduced in 2009.
- Tend to break rules of encapsulation.
- A primary tool of functional programming.
- Take input, calculate and return output, all without modifying objects received from the outside.
- Live in their own class (ideally).
- Generic enough to be applicable to many Types (ideally), not just one.
- Available in C# (of course), as well as F# and Visual Basic.

Using extension methods via:

- Metaprogramming: Require specific classes and their properties for inputs and processing.
- Functional: Usually requires defensive-coding techniques to avoid nullable or non-guaranteed-returned object instantiations.
- Bridging OOP and procedural techniques: Create generic functions that can be applied to many Types that do not modify input objects, but guarantee a usable return i.e. not null.

Extension Method Binding:

- Happens at Compile Time.
- Classes and Interfaces can be "extended" with Extension Methods _but not overriden_.
- Name collision will result in the Extension Method never getting called (dead code).
- Extension Methods are always lower-priority than the extended Type's own Instance Methods.

The Compiler Ingestion and Processing Order:

1. Extended Type's method signatures.
2. Extended Interface method abstractions.
3. Extension Method Type method signatures.

Once the Compiler finds a signature match, it stops working its way down this list.

### What Are Extension Methods

Extension Methods Are:

- Static Methods.
- Called as if they were Instance Methods on "the extended type".
- Compiler instructions: The compiler translates Extension Method codeinto appropriate calls that follow encapsulation rules.

Examples of Existing Extension Methods:

- LINQ Standard Query Operators. Extend `System.Collections.IEnumerable` and `System.Collection.Generic.IEnumerable<T>`.

_Note_: Extension Methods _can_ help create cleaner code.

### How To Build An Extension Method

To build an extension method:

- The extended Type is referenced with the `this` keyword.
- `this` must be the first parameter.
- Additional parameters must be the Type that is being extended.
- Additional parameters beyond the first two are allowed.

### How To Use An Extension Method

1. Call the Extension Class into scope with a `using` directive.
2. Call the Extension Method as if it were the target Type's instance method.

### When to Use Extension Methods

- Free up functionality from custom or existing `.NET` and `CLR` objects and make it reusable.
- Extending `Struct` types requires using the `ref` keyword. Structs are Value types, not Reference types so changes made are only made to the _copy of the struct_, and are lost when the Extension Method exits.
- Use Extension methods when private members do _not_ need to be accessed to get the job done.
- The original Class or Object is not under your control. Use Extension Methods to build-out portable functionality.
- When a `derived` object cannot be used. Try Extension Methods instead.
- _Chain_ functions using Extension Method calls. LINQ Standard Query Methods are a good example.

### Risks Using Extension Methods

Code you don't control might change unexpectedly, causing functionality our input/output changes your Extension Method cannot support, or method signatures silently override your Extension Method(s).

### Why To Use Extension methods Or Not

Collection Pattern:

1. Define a Collection Class that implements `IEnumerable<T>`.
2. Build functionality around this custom class like Add, Remove, Find, etc.

Collection Functionality using Extension Methods:

1. Build Extension Methods that have the functionality necessary to operate on `IEnumerable<T>` interfaces.
2. Bring-in the Extension Namespace to use when a type that `IEnumerable<T>` is in scope.

Extension Collections Benefit:

- Any Type that implements `IEnumerable<T>` is accessible to the Extension Method.
- No need to define an entire Collection manually.

Layered Application Design Pattern:

1. Design Data Transfer Objects with little functionality.
2. Implement object translation between application boundaries as needed.

Layered Applications Leveraging Extension Methods:

1. Design Domain Entities (same as above) with little-to-no functionality.
2. Add Extension methods to add the functionality that is specific to each Application Layer.

Layer Application Extension Methods benefits:

- Minimize Domain Entitiy code block size.
- Limit overall capability of each Domain Entity to just what it needs for its parent Application Layer.
- Separates added Domain Entity functionality from the Domain Entity itself.
- Added features in Extension methods do not rev the Domain Entities but still provide functional benefit.

Chain Your Method Calls!

- Extension Methods allow chaining Method calls using dot-notation.
- Clear-up code intentions with more concise naming and parameter usage.
- Reduce number of necessary parameters by calling the source Type/instance and filling-in required defaults (similar to what a Factory Method would do).

Avoid Nested Method Calls!

- Deeply nested calls are difficult to interpret in code.
- Nested method calls are difficult to debug.

Separate Dependencies from Classes that don't need them:

- If a class needs to write to a database, an Extension Method can provide the capability to access the database. The calling method would still need to include the DbConnection String, but the extended Class would _not_.

_Avoid_:

- Building Extension Methods to built-in .NET Library Classes as it will quickly become confusing.
- Deploying _many_ Namespaces to sort the Extension Methods will quickly become difficult to track and especially to debug and test.

_Do_ use Extensions Methods to:

- Add new functionality to your own classes that are already implemented and well tested.
- Minimize adding bugs by adding functionality on top of existing.
- Group your Namespaces. This helps avoid namespace collisions.

## About Aggregation and Composition

Create larger, more complex Types by piecing together existing, smaller and less complex Types.

Both:

- Specify a whole/part relationship.

### Aggregation

- Lifetime of the whole and its parts are not bound together.
- Parts can exist without the whole.

### Composition

Enable a Class to utilize another class

- Lifetime of the whole and its parts are bound together.
- Individual components cannot exist without the whole.
- Establishes a "has a" relationship between classes.

With inheritance, a base class is used to store the state data, simplifying definition and management of inheriting class ojects.

- Use abstract bsae classes to enable inheritors to use and/or override as needed.
- Until a level of complexity grows.
- Code duplication begins to appear with complexity and when the base class is not designed to support complex functionality of inheriting classes.
- Did the base class model the correct behaviors/capabilities?

Use Composition to help overcome issues with inheritance, especially as inheritor complexity requirement rises.

- Define separate classes to define behaviors individually.
- Assign Fields to those classes to define the capability of the Composed class.
- Utilize nullability to allow assigning a possibly not-enabled capability.
- Add factory methods to return new instances based on the Composed-class Properties.

### Favor Composition Over Inheritance

Inheritance is fine, but as complexity increases, inheritance limitations become a barrier to further development.

Composition enables continued added complexity with less repetitive code, guaranteeing valid object generation through factory methods.

## For ForEach While DoWhile

For: Use this to iterate over an indexed collection.

ForEach: Syntactic-sugar for `GetEnumerator` and `Next` calls on an `IEnumerable` collection.

While: Execute code within the attached code block so long as the condition returns true.

Do-While: Execute code within the attached code block _and then check the conditional_, and only execute the codeblock if the condition returns true.

## Null Safety in CSharp Overview

Null detection and handling changes in C# 2.0 and greater provide a means to better avoid null reference exceptions in an app.

C# 2.0 introduced `Nullable<T>` where a generic reference type could be initialized as null. Use `T?` to implicitly or explicitly set a null:

- `int? first;` (implicit)
- `int? first = null;` (explicit)

C# 8.0 allows setting intent as in the reference type _might_ be null or _is always_ non-null (default value). The compiler tries to enforce this setting.

When a null is 'dereferenced', it means the variable is evaluated at runtime but refers to an initially null value.

Null safety reduces the possibility of `NullReferenceException` occurences, so the compiler provides warnings when possibly derefencing null.

Basically, that last point is the goal: Help to avoid throwing `NullReferenceException` whenever possible.

## Setting Nullability In Your Code

To infer intent of code and enforce desired behavior, set "Nullable Context", using these contexts:

- disable: C# 7.3 behavior is followed
- enable: all null reference analysis and language features enabled
- warnings: all null analysis is performed and warnings emitted  when code dereferences a possible null
- annotations: NO null analysis is done, no warnings emitted where code might dereferences null, but annotations are allowed

Settings are available:

- CSPROJ file: `<Nullable>` element. Scopes to entire project.
- .CS file: '#nullable enable'. Scopes to just that .cs file.

## Null Operators

There are several operators dedicated to working with nullable references:

Conditional operator (ternary) `?`:

- Tells the compiler the object is _intended to be nullable_.
- Enables shorter boolean expressions such as `int bar = foo > 20 ? foo : 0`
- Defined as `condition ? consequent : alternative` that _must evaluate to true or false_.

null forgiving operator `!`:

- Tells compiler to not warn about possible null.
- Does not protect code from throwing an exception.

null coalescing operator `??`:

- Check for null and apply the property accordingly.
- `return (foo ?? bar)` returns 'bar' only if 'foo' is null.
- Can also be used with an equality operator `??=` e.g. `(foo ??= new List<int>()).Add(bar);` only initilizes foo with 1 item if foo is null.
- Left-had operand must be a variable, property, or indexer element.
- Both sides of the operand _must be nullable types_.

null conditional operators `.?` and `?[]`:

- Perform an action based on the state of a nullable object.
- Applies member aaccess to its operand only if that operand evalutes to non-null, else returns null.
- Applies element access using `?[]` to its operand (under same condition as previous bullet point).
- Example: `string thingy = foobar?.ToString()`. Equivalent to turnary statement `string thingy = foobar is not null ? foobar.ToString() : default`.
- When evaluation of left-hand operand returns null, the rest of the statement is short-circuited!

## Best Practices Handling Nullability

- Assign an initial value to initialized objects and structs whenever possible.
- Avoid relying on the Null Forgiving Operator and instead perform logic statements that ensure nullable references are handled properly.

## References

- MSLearn docs on [Extension Methods](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/extension-methods).

## Footer

Return to [ContEd Index](conted-index.html)

Return to [Root README](../README.html)
