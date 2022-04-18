# Read06 Node and Pair Programming

## Index

[Node JS Q and A](#node-js-q-and-a)  
[Pair-Programming Q and A](#pp-q-and-a)  

## Node JS

Article by James Hibbard of [sitepoint.com](https://www.sitepoint.com/an-introduction-to-node-js/)

### What is Node

A runtime environment that supports javascript.  
NPM is Node Package Manager, which handles registration, updates, and dependencies in node packages.  
NVM is Node Version Manager, which allows changing versions of Node easily.  
Node is *single-threaded*.  
When Node encounters a blocking call, it "registers a call-back" and moves forward in execution until the callback is "called" by the other entity that Node *could have been waiting for* but didn't.  

### Server-side Node

Node allows execution of javascript, server-side.  
Use a cloning strategy with node to handle large volumes of requests and calls.  
Node uses an "event loop" to manage thread pooling and effecient utilization.  
CPU-intensive operations should be sent to a "worker thread" so it does not block other operations.  

*Note*: Newer features "Promises" and "async-await" of javascript make working with asynchronous code a little easier.  

### What Node Is Good At

- Real time interaction.  
- Streaming data.  
- Building APIs.  
- Native ability to read, process, and output JSON.  

### About Packages

They can be installed globally with the '-g' switch.  
To save a package as a project dependancy add the '--save' switch.  
lodash: Install to make working with JS objects and arrays easier, see [the docs](https://lodash.com/docs)  
package.json: npm stores node modules in this file, as a lookup or directory of installed or dependent packages.  
Node is the modern way to easily build and use javascript applications.  
Express is a package that helps structure and build applicatiosn with Node. [ExpressJS](http://expressjs.com/)  

### Node JS Q and A

What is node.js?

> A javascript runtime.  
> V8 is an opensource JS runtime that runs in Chromium-based browsers.  

In your own words, what is Chrome’s V8 JavaScript Engine?

> It compiles javascript to a language computers can execute.  

What does it mean that node is a JavaScript runtime?

> It interprets javascript and executes JS functions in a particular order in order to do work.

What is npm?

> *N*ode *P*ackage *M*anager.
> NPM is used to install, upgrade, and maintain node and packages for execution in Node.  

What version of node are you running on your machine?

> v14.19.1

What version of npm are you running on your machine?

> 6.14.16

What command would you type to install a library/package called ‘jshint’?

> npm install jshint

What is node used for?

> Node is based on the V8 javascript runtime engine so it will execute javascript.  
> Client-side and server-side applications, especially Apps that required real-time interaction, streaming, or have APIs.  

## Six Reasons to Pair Program

### Improve Code Quality

Use a linter.  
Code review.  
*Pair Programming*.

### PP Q and A

What are the 6 reasons for pair programming?

1. Greater efficiency. Improve code quality, reducing coding mistakes (two heads are better than one).  
2. Promotes a collaborative environment. Pair programmers are more likely to focus on the job at hand, for the benefit of each other.  
3. Supports learning. Exposes pair programmers to new or unique approaches and solutions to coding problems.  
4. Improve social skills. Communication is key to effective pair programing, and so is learning how to work well with others. Finding the right words to use is necessary. Employers look for employees that can work well with others, and pair programming helps build that soft skill.  
5. Prepares for job interviews. Often times a candidate will be asked to pair program with an employee to evaluate the candidates collaboration style, and ability to get along with the existing team.  
6. Having pair programming skills at the onset of employement will help new hires to rapidly become more productive.  

In your experience, which of these reasons have you found most beneficial?

> Promotes learning. I have seen this technique help fellow students learn javascript and gain a better understanding of a block of code while writing it.  

How does pair programming work?

> Bothe developers sit at the same workstation working on the same app, feature, and/or code block or for a specific coding purpose. One developer is the *navigator* - responsible to researching the code, and determining what code needs to be written to the code page. The other developer is the *driver* - the only person allowed to touch the keyboard, and follows the instructions of the Navigator, asking questions when necessary, but otherwise concentrating on writing the code as described by the Navigator.  

## Resources

Build a NodeJS [MVC App](https://www.sitepoint.com/node-js-mvc-application/)  
Create a javascript project [scaffolding tool](https://www.sitepoint.com/scaffolding-tool-caporal-js/)  
Nodejs [Best Practices](https://www.sitepoint.com/node-js-best-practices-from-the-node-gurus/)  
Six Reasons to [Pair Program](https://www.codefellows.org/blog/6-reasons-for-pair-programming/)  

## Footer

Back to [readme.md](../README.html)  
