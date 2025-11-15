# Collection of Notes Related to Functional Programming Concepts and Practices

## Learning Functional Programming Through Construction

Presenter: cameron presley, SmallBatchSolutions.io, Microsoft MVP

### Stream of Thought Notes

- Design code in such a way that code won't compile when a bug is written.
  - Not always feasable, but can reduce bug injection.
  - Makes it harder to do the _wrong_ thing(s).
  - Simplifies testing!
- Understand project requirements.
- Think about the _nouns_ that are specific to the project requirements.
- Model the nouns:
  - Strings are not always a great choice.
  - If multiple possible states or 'things', consider an enum or Collection of some type.
- Records
  - Does comparison by _value_ instead of _reference_ (this is helpful).
  - Use 'init' modifiers to record properties to keep it _immutable_.
- Invent conventions that make errors stand out:
  - At design time.
  - At build time.
  - Well before deploy time!
- Using immutable types simplifies code:
  - Disallows unexpected state changes.
  - No longer requires "state tracking".
- Use mappings:
  - Accept one immutable object.
  - Then create a new immutable object with new state based on the input object.
- Input x :arrow_right: function f :arrow_right: output y
  - Map between two sets such that every element in first maps to single element in second.
  - Unmapped or unexpected values cannot be processed, causing inconsistent behavior.
- It is difficult to:
  - Know how to use the type system if the types are lying.
  - Debug inconsistent behavior.
- Use pipelines to glue functions together:
  - Map input to commands (UI level).
  - Map commands to actions.
  - Invoke the action to the object.
  - Replace old object with action applied to new object.
- Do not trust user input. Instead:
  - Not all strings are valid input, so conversion and coertion are usually required.
  - Restricting input values _or_ expand the possible outputs.
- Unknown input?
  - If there are only 4 known commands, but millions of possible inputs, map other inputs to the "Unknown" property (a command in the example).
  - Map unkonwn input(s) via a select statement 'default' codeblock.
- The 'DoNothing()' function:
  - Just returns, matching other known function signatures.
  - The "Identity Function".
  - Allows mapping unknown inputs to a valid function!
- Compose:
  - Can be written as an extension method.
  - Input two functions where A -> B, and B -> C, return will be A -> C
  - Creates a "Pipeline" that is relatively easy to test:
    - If there is something wrong with the mappings, the pipeline will break.

> If you say your code is going to do something, it needs to do that one thing, exactly, everytime.
> If you cannot restrict the input, you will need to expand the output.

_Note_: 'Type Unions' are coming to C# (see GitHub).

_Note_: C# Aggregate maps to Reduce() in JS (and other languages).

## References

- Hosted by the Pittsburgh .NET User Group [PGHDOTNET](https://linkedin.com/in/pghdotnet)
- The Software Mentor Presentation[Learning Functional Programming Through Construction First Principles](https://blog.thesoftwarementor.com/presentations/#learning-functional-programming-through-construction-first-principles)
- Jeff Atwood of [Coding Horror.com](codinghorror.com) re-quote: "Falling into the pit of success".
- [C# has a thing called 'smart pointers'](...)

## Footer

Return to [ContEd Index](./conted-index.md)

Return to [Root README](../README.md)
