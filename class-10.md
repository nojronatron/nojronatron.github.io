# Notes from Duckett HTML and JS Books

Notes taken from Ducketts JS book:  
Chapter 6: “Error Handling and Debugging” (pp.449-486)  

## Chapter 6 Error Handling and Debugging

### Key Aspects of JS Execution  

- JS interpreter reads one line of code at a time from top-to-bottom.  
- JS execution is stacked during execution, meaning asynchronous operations 'wait' until other processing is completed.
  - An example is when a function is called, execution at the current line halts until the called function returns.  
  - Operations style can be thought of as a LIFO stack.  
- Variables are scoped to the function they are definied within.  
  - Multiple calls to the same function will no automatically re-use the same values in the same variables.  

### Context and Scope

Three execution contexts:

1. Global: Code in the script but not inm a function. Only one of these per code page.
2. Function: Code running inside a function is bound by the function's braces.  
3. Eval Context: An internal function context.

Two variable scopes:

1. Global: Variables declared outside a function can be accessed from anywhere.  
2. Function-level: Variables declared inside a function cannot be access from outsite same function.  

### Execution Context and Hoisting

Two phases of activity when JS enters a new execution context:

1. Prepare: Scope, variables, functions, and args are created.  
2. Execute: Values assigned to variables, functions can be referenced and executed, and statements are executed.  

### More About Scoping

Variables Object is used in the interpreter to store aspects of different execution contexts.  
Each execution context has access to variables object of its parent.  
Create variables as close to where they are needed because the interpreter will 'climb the stack' of contexts to find a more widely scoped variable, which is an expensive operation.  
Each function gets its own execution context to run within.  

### Understanding Errors and Error Objects

The Process:

- Exceptions are thrown by the interpreter when it cannot continue execution.
- Exception Handling Code is necessary to deal with a 'thrown exception'.  
- Execution is halted when an Exception is thrown so the interpreter can find and execute exception-handling code.
- If there is no excepion-handling code all the way up through the global context, the interpreter stops execution entirely and report the exception message(s).  

Error Objects:

- JS creates Error Objects to hold information about Exceptions.  
  - name, message, fileNumber, lineNumber.  
- Browsers have tools to help use these.  

There are 7 types of Error Objects in JS:

1. Error
2. SyntaxError
3. ReferenceError
4. TypeError
5. RangeError
6. URIError
7. EvalError

In summary, either something doesn't exist, was not used correctly, or is outside of a range like number of elements not the correct Type.

### Debugging and Dealing with Errors

- Use Developer Tools in the browser to look for logged error messages or other hints.
- Use Try-Catch-Throw statements to gracefully handle erors.  
- Debug the code to find and eliminate (or work around) the errors.
  - Where is the problem?
  - What *exactly* is the problem?

- Use the console.* methods to output information while the script runs to gain insight as to what might be going wrong prior to the error.  
  - `console.warn()`
  - `console.error()`
  - `console.group()`
    - `console.info()`
    - `console.log()`
  - `console.groupEnd()`

`Console.Table()` can be used to show tabular output of objects and multi-dimensional arrays.  

`console.assert()` displays assertion failed messages to the console.  

### Breakpoints and Stepping Through Code

Breakpoints are spots where code is 'halted' so the state can be inspected.
Chrome and Firefox have built-in breakpoint/debugger tools.  
Once code hits a breakpoint, the engineer can step through the code lines, in and out of function calls, to learn what is happening during code execution.  
Conditional breakpoints can be set so a breakpoint will only be hit under certain conditions.  
Breakpoint from your code with `debugger;` but it requires developer tools are open in the browser.  

### Handling Exceptions

Try block: wrap this around code that you think will (or does) throw an exception.
Catch block: Required? Wrap this around code that will do something (intelligent and helpful) with the application state or handle the situation gracefully and allow code execution to continue.  
Finall block: Optional? Used to 'clean up' after a try block has been entered and exited, regardless of whether or not an Exception was thrown.

### Throwing Errors

Keyword `throw` will raise an Exception along with a String message.  
Usage: `throw new Error('message');`  

### Debugging Tips

Things to try when debugging errors, exceptions, and unexpected results:

- Try a different browser.  
- Log to the console to see what is output and confirm good/bad during execution.  
- Comment out code segments and re-run, observing the behavior.  
- Try reading the code aloud or explaining what it is doing. Talking through it often helps uncover errors.  
- Use the interwebs: Stack Overflow, MDN, W3Scools, etc.  
- There are many online 'code playgrounds' where ideas can be tested out and code segments can be duplicated and executed in isolation.  
- Validation tools to check the syntax.  
- Check case sensitivity.  
- Verify correct variable keyword and scope are used.  
- Confirm spellings using a search & replace utility for handle mis-keyed words and identifiers.  
- Confirm whether an issue is `undefined`, `null`, or `NaN`. These are different types and concepts.  
- Verify the correct TYPE is in use. Take into consideration type coersion, strictly equals, and parse or other evaluating statements.  

### Resources

jQuery debugger (Check the Chrome Store)  
[JSBin.com](https://jsbin.com)  
[JSFiddle.com](https://jsfiddle.com)  
[Dabblet.com](https://dabblet.com)  
[CSSDeck.com](https://CSSDeck.com)  
[CodePen.com](https://codepen.com)  
[JSLint.com](https://www.jslint.com)  
[JSHint.com](https://www.jshint.com)  
[JSONLint.com](https://www.jsonlint.com)  

[Back to index in readme](./README.md)