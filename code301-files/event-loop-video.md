# Video Notes: Event Loops

Notes taken while watching Philip Roberts' discussion on the Event Loop.  

YouTube video [What the heck is the event loop anyway?](https://www.youtube.com/watch?v=8aGhZQkoFbQ&ab_channel=JSConf)  

## Who Is Philip Roberts

Philip is a software developer who works for '&yet', a "dev-shop / product company" that specializes in real time help.

## JS Runtime and Blocking

V8, single-threaded, callbacks, etc.  
JS uses a synchronous language, but it has some asynchronous-esque capabilities.  
v8 has a call stack and a heap, among other things.  

## The Browser As A Runtime

V8 runs inside Chrome, that is the runtime for JS.  

- Heap: Where JS stores its methods while they are executing.  
- Call Stack: Stack Frames live here.  

The browser provides some bigger picture items for the JS Runtime & V8:

- Web APIs: DOM Document, ajax (XMLHttpRequest), and something called setTimeout.  
- Callback Queue: Stores methods that are instantiated within a callback.  
- Event Loop: Regularly checks for items in the Callback Queue and in the JS Stack  

## The Event Loop

On a regular basis the Event Loop does the following:  

1. Checks to see if anything is in the JS Stack.  
2. If JS Stack is empty, it checks the Callback Queue.  
3. If an item exists in teh Callback Queue it takes the FIFO item and places it *on the JS Stack*.  

### The Call Stack

JS is single-threaded, therefore a single Call Stack.  
Keeps the actively-executing function in memory while it executes.  
'Main()' is a function in itself, indicating a JS file is being executed.  
Every function-call within Main is then 'added to the stack'.  
After each function "returns", it is removed from the Stack and the previous function entry continues excution.  

### Blocking

When things are 'slow', it blocks execution of other methods, they have to 'wait'.  
This is due to the synchronous behavior of the JS Runtime.  
Single-threaded applications will suffer from this.  
Browsers make this problem very apparent when blocking happens because the UI will not appear to respond, even to UI clicks or other events.

*The browser has to wait until the call stack is cleared before waiting functions and requests can be executed.*

## Concurrency and the Event Loop

JS - the Runtime - cannot make additional requests while it is working on something else.  
The Browser has other APIs, that are basically threads that will do their own work.  
The WebAPI cannot just push completed work onto the JS Stack so instead it puts the completed work item into the Task Queue.  
Whenever the JS/V8 Stack is clear, the Event Loop takes the first-in work item from the Task Queue and passes it to the JS Stack to be executed.  

*Note*: Node is like the DOM except instead of web APIs it is made of C++ APIs and hides all the concurrency and threading issues from the developer.  

What about setting a function timeout timer to zero (set time zero) when we call a Web API? *This forces the completed task to move directly to the Task Queue so it is 1st in line once the JS Stack is clear*.



## Blocking Effects on the Event Loop

## Footer

[Back to Readme.md](../README.md)  
