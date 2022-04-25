# Memory Usage Notes and References

## Understanding the JS Call Stack

- The Call Stack is for function invokation.  
- There is only one Call Stack.  
- Functions are executed one at a time and removed once completed successfully.  
- The Call Stack is a LIFO (Last In First Out) data structure.  

## JS Q and A

What is a ‘call’?

> An invokation of a function.  

How many ‘calls’ can happen at once?

> One.  

What does LIFO mean?

> It is a stack (or array) where the last item in is always the first item out.  

Draw an example of a call stack and the functions that would need to be invoked to generate that call stack.

```text
[A| | | | ]
 ^
 PUSH fx(a)
```

```text
[A|B| | | ]
   ^
   PUSH fx(b)
```

```text
[A|B|C| | ]
     ^
     PUSH fx(c)
```

```text
     POP => function(c)
     v
[A|B| | | ]
```

```text
[A|B|D| | ]
     ^
     PUSH fx(d)
```

```text
     POP => function(d)
     v
[A|B| | | ]
```

```text
   POP => function(b)
   v
[A|B| | | ]
```

Etcetera.

What causes a Stack Overflow?

> Googling the answers to tough coding questions.  
> A recursive function that calls itself without an exit condition.  
> More functions are placed on the stack than there is memory allocated to store them.  

## JS Error Messages and Debugging

### Tools

- The `debugger;` statement: Stops RunTime execution of the code at that code line.  
- The `console.trace();` statement: Outputs the stack trace (labels) to the Console.  
- Insert a 'try-catch' block into areas of code that might fail, overflow, or where error flow control is needed.  
- RunTime Errors (which is all of them in javascript) are only detectable at RunTime.  
- Quokka and ESLint: Evaluate code as you type; Display warnings and error messages about code style and syntax during developing time.  

### Error Messages and Debugging Q and A

What is a ‘reference error’?

> Attempting to use an uninitialized variable.  

What is a ‘syntax error’?

> Incorrect syntax was used when defining an expression.  

What is a ‘range error’?

> When indexing into an iterable, selecting an index ID that is not included in the iterable.  

What is a ‘tyep error’?

> Not sure about "tyep error" but a Type Error happens when tyring to use incompatible types together, such as an Array and a Number.  

What is a breakpoint?

> A developer-assigned location in the code where the RunTime will halt when reached so that value and reference types can be examined.  

What does the word ‘debugger’ do in your code?

> It stops code execution at the line where the keyword is.  

## Resources

Understanding the JS Call Stack on [Free Code Camp.org](https://www.freecodecamp.org/news/understanding-the-javascript-call-stack-861e41ae61d4)  
JS Error Messages and Debugging [codeburst.io](https://codeburst.io/javascript-error-messages-debugging-d23f84f0ae7c)  
MDN on javascript [Errors](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors)  
List of Udemy courses for full-stack developers at [CodeBurst.io](https://codeburst.io/best-udemy-courses-for-learning-full-stack-web-development-45e2bd3ec28b)  
Brandon Morelli on [Medium.com](https://medium.com/@bmorelli25)  

## Footer

Back to [readme.md](../README.html)  
