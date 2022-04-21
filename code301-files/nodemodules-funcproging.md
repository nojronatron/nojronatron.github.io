# Node Modules and Functional Programming

These need to be transferred to nojronatron.github.io and submitted in Read09 assignment on Canvas.  

## Functional Programming Concepts

Article by TK on [Medium.com](https://medium.com/the-renaissance-developer/concepts-of-functional-programming-in-javascript-6bc84220d2aa)  

### Functional Programming Q and A

> Programs developed using collections of functions to do work rather than lists of statements (like in a script).  

What is a pure function and how do we know if something is a pure function?  

> Is deterministic: The function will return the same result given the same input, and does not cause any observable side effects.  
> It does not rely on global objects (variables, files, etc) that are not passed-in explicitly as parameters.  
> Does not utilize an internal random generator.  
> Will not modify any global object or parameter passed by reference.  

What are the benefits of a pure function?  

> All inputs are known and the output is predictable.  
> As stated in the article: "Given param A => expect the function to return value B"  

What is immutability?  

> Changing the value stored in memory mutates the memory (variable). Immutability is a property of dissallowing change in that memory location.
> Strings are immutable, so every time they have a value reassigned, they are actually changing the memory state.

What is Referential transparency?  

> Given the same inputs, functions that are referentially transparent always return the same result.
> As the author put it: "pure functions + immutable data = referential transparency" *[TK on Medium.com, accessed 21-Apr-22]*  

## Node Modules Q and A

[The Net Ninja](https://www.youtube.com/watch?v=xHLd36QoS4k&ab_channel=TheNetNinja)  

What is a module?

> A small piece of executable code that is easy to maintain, and has a specific purpose.  

What does the word 'require' do?

> When we want to use a module in node.js.

How do we bring another module into the file that we are working in?

> Use `require(./path-to-file);`

What do we have to do to make a module available?  

> Use `module.exports = what-functions-to-be-made-available`  
> At that point, use a require statement in the calling module and assign the require output to a local variable.

## Footer

Go back to [Readme.md](../README.html)  
