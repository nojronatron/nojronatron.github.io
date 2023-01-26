# Typescript Basics

Microsoft Reactor held a presentation series about Typescript. The language has been gaining steam and I am growing increasingly curious. These notes will be mostly ad-hoc to start.

## Microsft Reactor Typescript For Beginners

### Overview

A base experience in javascript will help get going with Typescript.

Javascript was created in 1995 by Brendan Ike in about 10 days. Javascript today is much more robust than it was in 1995. Core parts of Javascript are still in-tact.

Javascript has costs:

- Type errors.
- Mixed-type evaluations e.g. `console.log(2 + '2')` returns `22`.

TypeScript in 2010's was heavily developed at Microsoft, prior to be released to "the Consortium".

TypeScript provides everything in Javascript and more.

### Type System

Static Typing

Available "Everyday" Types:

- String
- Number
- Boolean
- Array
- Functions
- Objects

Additional Types:

- Union
- Type Aliases: Create your own types!
- Interfaces
- Tuples
- Enums

### Why Typescript

- Control code changes.
- Fewer errors during compilation.
- Efficiency.
- Better experience.

### Recommendations

Use GitHub CoPilot! This will help by making suggestions while coding TypeScript.

Get used to learning what the error messages *mean*.

### Benefits

- Compiler.
- Type Checker verifies the actual Type is the expected Type.
- Auto-suggestions (the first example was the 'red squiggly line').
- Types in Tooling extends module-based types into your code, supporting Type Checking at compilation time.
- Type Inference: Instead of having to declare variables with their Type, TSC can figure it out. e.g. Assume a String when quotations are used.

### Learning Curve

Takes some time to learn/get used to.

Confusing error messages: Learning what they mean can slow progress.

Configuration options: (was not explained during the presentation).

### Set Up TS Environment

1. Install locally `npm install -g typescript` (use -g for globally per NPM).
1. Confirm installation using `tsc -version` e.g. 'Version 4.9.4'.
1. Create config file: `tsc -init`.
1. Start developing in TypeScript!

### Declare Variables

Assign a value to a name and include a Type: `let name:type = value`

### Declare an Array

`const myArray: string[] = ['alpha', 'bravo', 'charlie'];`

When declaring the Array as a Type, all the values within the Array *must be the declared Type*.

Pushed Types *must also* be of the declared Type.

### Tuples

Not built-in to JavaScript.

`let myTuple: [string, number, boolean];`

This declares an object with specified Types in the specified order.

Attempting to add a Number type as the 1st value in the Tuple will throw an error (at compile time?).

Editorial: It feels like a TS Tuple boils-down to an Object with fields in JavaScript.

### Objects

`object: { name: type; name: type };`

```typescript
function foo(fooInfo: {
  fooName: string;
  fooEmail: string;
  fooTime: boolean;
}) {
  console.log('fooInfo:', fooInfo);
}

foo('bar', 'baz', true);
```

### Compiling

Outputs JS file(s).

TSC is the TS Compiler executable:

- TSC filename: Compiles only when executed in the Terminal.
- Watcher Mode `tsc -w`: Compiles during code writing (similar to 'nodemon').

### TSConfig

JSON file with lots of comments describing what the configuration item does.

Strict: Boolean switches type-checking level.

Target: Sets the JavaScript version target e.g. ES6

OutFile and OutDir: Uncomment for dev to control where source will be output (default: './'; option: './src').

## References

MSFT Learning [TypeScript Getting Started pt.1](https://aka.ms/GettingStartedWithTypescript1)

MSFT Learning [TypeScript Getting Started pt.2](https://aka.ms/GettingStartedWithTypescript2)

Get used to TS online with [TypeScriptLang](https://www.typescriptlang.org/play)

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
