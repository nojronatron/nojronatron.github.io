# DotNET CSharp Stuff

Notes on various topics while developing software with, or learning more about, C# and .NET.

## Table of Contents

- [Extensions](#extensions)
- [Aggregation and Composition](#aggregation-and-composition)
- [Null Safety in CSharp](#null-safety-in-csharp)
- [Footer](#footer)

## Extensions

Custom extension methods can be created for any class.

- Introduced in 2009.
- Tend to break rules of encapsulation.
- A primary tool of functional programming.
- Take input, calculate and return output, all without modifying objects received from the outside.
- Live in their own class (ideally).
- Generic enough to be applicable to many Types (ideally), not just one.

Using extension methods via:

- Metaprogramming: Require specific classes and their properties for inputs and processing.
- Functional: Usually requires defensive-coding techniques to avoid nullable or non-guaranteed-returned object instantiations.
- Bridging OOP and procedural techniques: Create generic functions that can be applied to many Types that do not modify input objects, but guarantee a usable return i.e. not null.

## Aggregation and Composition

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

## Null Safety in CSharp

Null detection and handling changes in C# 2.0 and greater provide a means to better avoid null reference exceptions in an app.

### Overview

C# 2.0 introduced `Nullable<T>` where a generic reference type could be initialized as null. Use `T?` to implicitly or explicitly set a null:

- `int? first;` (implicit)
- `int? first = null;` (explicit)

C# 8.0 allows setting intent as in the reference type _might_ be null or _is always_ non-null (default value). The compiler tries to enforce this setting.

When a null is 'dereferenced', it means the variable is evaluated at runtime but refers to an initially null value.

Null safety reduces the possibility of `NullReferenceException` occurences, so the compiler provides warnings when possibly derefencing null.

Basically, that last point is the goal: Help to avoid throwing `NullReferenceException` whenever possible.

### Setting Nullability In Your Code

To infer intent of code and enforce desired behavior, set "Nullable Context", using these contexts:

-	disable: C# 7.3 behavior is followed
-	enable: all null reference analysis and language features enabled
-	warnings: all null analysis is performed and warnings emitted  when code dereferences a possible null
-	annotations: NO null analysis is done, no warnings emitted where code might dereferences null, but annotations are allowed

Settings are available:

- CSPROJ file: `<Nullable>` element. Scopes to entire project.
- .CS file: '#nullable enable'. Scopes to just that .cs file.

### Null Operators

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

### Best Practices Handling Nullability

- Assign an initial value to initialized objects and structs whenever possible.
- Avoid relying on the Null Forgiving Operator and instead perform logic statements that ensure nullable references are handled properly.

## Footer

Return to [ContEd Index](conted-index.html)

Return to [Root README](../README.html)
