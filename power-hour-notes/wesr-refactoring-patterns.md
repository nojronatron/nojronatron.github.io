# Wes Discusses Refactoring Patterns

How to refactor code, and how it will help you going forward.

## About Wes

Software developer and educator.

## Key Takeaways

Refactor Code to:

- Reorganize, rename, and rewrite code.
- Improve effeciency, readability, and reusability of the code.
- Avoid 'magic numbers': Values in code that have no obvious purpose. Use a CONST instead!
- Break out difficult to understand code into separate functions (modularize).
- Rename boolean variables so they say what they represent e.g. 'isSubscriber'.
- Avoid calling methods inside template literals.
- Variables are very cheap, use them!
- Refactor in concert with unit testing to ensure results meet requirements.
- Identify 2-3 small steps to improve code readability and reusability.
- Can help to reduce technical debt.

## Why and When to Refactor?

Code smells!

- Large function!
- Unreadable code in function.
- Code used more than 3 times, multiple files.
- Too many comments to 'explain the code'.
- Constantly using code that is difficult to understand.

Often times, code is 1st written as "just get it to work". As possible, take time to refactor that code so it is closer to meeting best code style practices.

## Footer

Back to [pph index](./pph-index.html)
