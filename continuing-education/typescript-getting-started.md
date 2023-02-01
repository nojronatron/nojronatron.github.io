# Typescript Basics

The language has been gaining steam and I am growing increasingly curious. These notes will be mostly ad-hoc to start.

## Microsft Reactor Typescript For Beginners

Microsoft Reactor held a series of presentations series about Typescript.

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

Get used to learning what the error messages _mean_.

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

When declaring the Array as a Type, all the values within the Array _must be the declared Type_.

Pushed Types _must also_ be of the declared Type.

### Tuples

Not built-in to JavaScript.

`let myTuple: [string, number, boolean];`

This declares an object with specified Types in the specified order.

Attempting to add a Number type as the 1st value in the Tuple will throw an error (at compile time?).

Editorial: It feels like a TS Tuple boils-down to an Object with fields in JavaScript.

### Objects

`object: { name: type; name: type };`

```typescript
function foo(fooInfo: { fooName: string; fooEmail: string; fooTime: boolean }) {
  console.log("fooInfo:", fooInfo);
}

foo("bar", "baz", true);
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

## Build a Project in TS

### Setup

Free TraficLab APIs at [https://developer.trafiklab.se/api](https://developer.trafiklab.se/api).

- SL Real-time Informaiton 5 API
- SL Location lookup API
- Get a DevKey: [https://developer.trafiklab.se/projekt](https://developer.trafiklab.se/projekt).

Guest Developer: Lucas Santos :arrow_right: Twitter: @\_staticvoid :arrow_right: GitHub: khaosdoctor

TS was intended to be:

- An easy migration from JS.
- "JavaScript that scales."

### Basics

Interfaces: Define what an object IS and DOES:

- Contract: This object will have these properties and methods implemented.
- Interfaces only define the members but do not implement them.
- Built-in are used to ensure a Type is created properly.
- Create your own to define custom object creation and TS will provide guidance on using them.

Typed Aliases:

- Define your own Types in TS.
- Similar to Interfaces (maybe the same?).
- Cannot add more members "later on".
- Adds restrictions to code e.g. to limit range of options in an object property.

There are also Typed Functions (but they were not defined nor discussed).

Initialize the project: npm init -y
Prep TS environment: npm i -D typescript @types/node @types/express
Create config file for TS "tsconfig.json": npx tsc --init
Find outDir and change it to "./dist".
Find strict and either:

- Change value to 'false' to migrate JS to TS.
- Leave 'true' in a new project to help ensure strict typeing.

DotEnvRC is roughly equivalent to '.env'.

Zod:

- Library (github: colinhacks/zod) that helps enforcing structure and types in TS.
- Error Class is brought in.
- 'z' Class.
- Is a type validator.

_Note_: ThunderClient can generate Typescript Types from a Response using the 'Response > Snippet' drop-down.

### Build

Confusingly, this topic was not discussed.

Givent the code that was shown during the session, I discovered the following:

1. In tsconfig.json: update 'rootDir' to ensure the correct source file root is targeted (might not be 'Project Root').
1. TSC was not finding the tsconfig.json file, so to work around errors indicating Express could not be 'imported' I did: `tsc --esModuleInterop ./src/app.ts` and the build succeeded.

## References

MSFT Learning [TypeScript Getting Started pt.1](https://aka.ms/GettingStartedWithTypescript1)

MSFT Learning [TypeScript Getting Started pt.2](https://aka.ms/GettingStartedWithTypescript2)

Get used to TS online with [TypeScriptLang](https://www.typescriptlang.org/play)

MSFT Reactor [Code and Links shared during TS Code](https://aka.ms/FirstTSProject)

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
