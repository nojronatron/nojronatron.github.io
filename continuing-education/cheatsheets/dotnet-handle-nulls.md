# DotNET Handle Null Notes

Tidbits on how to handle nullables and null safety, and null-handling code patterns.

## Table of Contents

- [Stream of Consciousness](#stream-of-consciousness)
- [References](#references)

## Stream of Consciousness

Nullable reference type usage is common today. Embrace them.

"DotNET Compiled Code does not indicate existence of Nullable Types." -Zoran Horat

Console.WriteLine() accepts nullable types without complaining. It replaces the null with a newline character sequence.

Prefer using 'is null' and 'is not null' operators over Equality operators `!=`.

Test that an object is referencing a certain type of sub-type:

```c#
void TypeTestAndSet(T t)
{
  T variable = t switch
  {
    Expression1,
    Expression2,
    _ => defaultExpression
  };
}
```

Use `as` instead of the cast expression:

- Cast: `return (Derived)instance;`
- As: `var result = instance as Derived; return result is not null ? result.ToString() : "Conversion failed.";`
- Use a 'null' test to confirm that the `as` conversion succeeded.
- Cast could throw an Exception.
- `as` will assign `null` to the instance if it fails, _instead of throwing an Exception_!

The `is` operator does the following:

1. Checks if the operand is null and only continues if it is not null.
1. Checks the operand for actual type or derived type and returns True if it is either.
1. Returns false in any other case.

Remember: Null objects _do not have Properties_.

Objects do things _for us_:

1. Coders should not have to do all the work of figuring out null types.
1. Coders should not have to do all the work to protect against unsafe nullable Property access.

Null Propagation Operator and Null Coellescing Operator:

- `?.` could return a null string! Aka a Nullable string `string? item`
- `??` will test for null to its left, and if it is null, will execute the expression to its right.
- Using _both_

Optional Objects:

- Install `LangageExt` to get access to these.
- Syntax: `Option<T> ...`
- There is _no null_ there are only objects `None` or `Some`.
- Coders must supply a mapping function to instruct an Optional method what to do when there is something, and where there is nothing.
- Example: `void Optional(Option<T> maybeT) { ... }`
- The implementation is up to the developer, so a Linq Extension Method like `Match(Func<T, TResult>)` where Func could be an anonymous function like a Lambda.

## References

- [MSFT: Type testing operators and cast expressions](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/type-testing-and-cast)
