# Promises

Many languages utilize Promises to manage asynchronous operations.

Review the purpose, use, and gotchas of Promises.

Develop a list of key takeaways that the future me can review.

## Overview

A Promise is:

- A proxy for a value that might not yet be known (because the asynchronous function might not have completed yet).
- Useful for associating handlers with an eventual success value or failure reason coming from an asynchronous method.
- Guaranteed to be asynchronous.

A Promise has one of 3 states:

- pending: Initial state that is neither fulfilled nor rejected.
- fulfilled: Operation was completed successfully. Returns with a value.
- rejected: Operation failed. Returns with an error.

Note: There is a 'settled' state which is short-hand for fulfilled or rejected, and not pending.

### Asynchronous Operations and The JS Event Loop

Event Loop is an execution stack that manages functions, popping them off after execution.

The Event Loop has a Message Queue that pushes functions onto the stack when it is empty.

Callbacks (callback functions) are used as asynchronous technique:

- They _are not asynchronous_ themselves.
- Pass a function by reference :arrow-left: Thisis a callback function.
- When the host function executes, it will eventually execute the callback function passed-in as a parameter.
- Whatever the callback function does will then execute to completion (synchronously) before being popped off the stack.

Callbacks can be used to encourage a set of functions that includes an asynchronous function (like calling a web API) to execute in-order.

Promises are inserted into the Microtask (Job) Queue in the JS Event Loop:

- Handles promise functions at a higher priority than other functions like `.timeout()`
- When the stack is empty the Job Queue inserts functions onto the Stack, and are then executed.
- Callback functions (if included) are then executed (created on the Stack, popped-off when completed).

## Construction

```javascript
// initialize a promise
const promise = new Promise((resolve, reject) => {});

// init with a resolve and reject function
const betterPromise = new Promise((resolve, reject) => {
  resolve('good value');
  reject('an error occurred');
});
```

Only construct a new Promise instance to wrap functions that do not already support promises.

Generally speaking, consuming promises will be more common than creating them.

## Consuming Promises

From the previous example, the 'betterPromise' object has functions that execute depending on the result.

Handle the promise using the following design:

```javascript
// the PromiseValue when resolved will be 'good value'
// and because the resolve method is synchronous it
// will immediately be resolved to variable 'response'
betterPromise.then((response) => {
  console.log(response);
});
```

When calling an API that will take take to return, use a function that will return a promise.

Handling the result is fairly simple:

```javascript
addWordsToDB(listOfWords)
  .then((results) => console.log('added list of words result:', results))
  .catch((err) => console.log('an error occurred:', err.message));
```

Use `.then()` to pass-in the resolved function of the promise (fulfilled) :arrow_right: Resolve handler.

Use `.catch()` to handle an error condition in the reject function of the promise :arrow_right: Reject handler.

## Lazy-evaluation vs Promises

In JavaScript, lazy methods are different than Promises.

In other languages, lazy methods might be referred to as Promises, and might behave differently than JS Promise will.

```javascript
// a lazy method is an arrow function
const lazy = () => expression;

// call the lazy method when ready
lazy();

// js hoisting plays a part
```

## Promise Instance Methods

Promise methods associate further action taken when a Promise is settled, and can be chained.

```javascript
addWordsToDB(listOfWords)
  .then((addResult) => processResult(addResult))) // a simplified callback
  .then((processedResult) => console.log('added and processed list of words result:', processedResult))
  .catch((err) => console.log('an error occurred:', err.message))
```

> Look mo, no pyramids!

Input arguments are callbacks, which can be written as arrow functions `(value)=>{return}`.

Each handler takes one execution tick, so limiting handlers will speed up Promise method execution.

Promise methods are executed in FIFO order but encapsulated such that the result of the first method is passed to the next method.

In the case of a thrown error, the error reason is the result that is passed to the next method.

`Promise.prototype.then()`

- Takes up to 2 arguments.
- First arg: Callback for 'fulfilled' case.
- Second arg: Callback for 'rejected' case.
- Returns a _new Promise object_
- Appends fulfillment and rejection handlers to the promise, returning a new promise resolving to the value of the called handler or its original settled value if the promise was not handled (e.g. `onFulfilled()` or `onRejected()` were not functions).

`Promise.prototype.catch()`

- Same as `then()` but does NOT contain an argument for a 'fulfilled' case callback.
- Place this at the end of the chained functions to catch any thrown error within the chain.
- Appends a rejection handler callback to the promise and returns a new promise resolving to the value of the callback if called, or the original fulfillment value if promise is fulfilled instead.

`Promise.prototype.finally()`

- Appends a handler to the promise and returns a new promise that is resolved when the original promise is resolved.
- The appended handler is called when the promise is fulfilled in either resolved or rejected cases.
- The appended handler is run _asynchronously_.

## Settled Promise Behavior

An action can be assigned to a settled promise. That action would be executed at the next asynchronous cycle (tick).

JS Promises were built to be compatible with previous Promise-like libraries.

Using `Promise.resolve(thenable)` is actually using a 'thenable' in place of a promise.

`Promise.reject('reason')` creates a new Promise object that is rejected with the given reason.

## Concurrent Promise Methods

Use these methods to handle various concurrent Promise fulfill/reject behavior from an iterable of promises (or thenables):

- `Promise.all()`: Fullfills when _all_ promises fulfill, or rejects when _any_ promise rejects.
- `Promise.allSettled()`: Fullfills when _all_ promises settle.
- `Promise.any()`: Fulfills when any promise fulfills, rejects when _all_ promises reject.
- `Promise.race()`: Settles when any promises settles with either Fulfill or Reject.

## Promises vs Async Await

The Syntactic Sugar of `async` and `await` make working with promises even easier.

Instead of using `then()` and `catch()` use the Try-Catch code pattern, executing 'fulfilled' code in the Try and handling 'rejected' in the catch block.

_Note_: There is a new 'top-level await' that can be used at the top of a module, eliminating the need for a module function to be labeled with 'await'. This is new enough that not all browsers currently support it, but this should make async-await code patterns a bit simpler. [MDN Await Operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await)

## Takeaways

Functions that will return a Promise should either be awaited or handled by chaining Resolve and Catch.

Functions are the basis upon which all JavaScript execution is directed.

Need to know how to use a promise example in another context :arrow_right: Use a callback i.e. call a function to do it for you.

Think of Promises as a way to leverage the asynchronous handling pipeline of the JavaScript Message Queue in the Event Loop.

Refresh your understanding the [JS Event Loop et al](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)

## MDNs Basic Example

```javascript
const myFirstPromise = new Promise((resolve, reject) => {
  // We call resolve(...) when what we were doing asynchronously was successful, and reject(...) when it failed.
  // In this example, we use setTimeout(...) to simulate async code.
  // In reality, you will probably be using something like XHR or an HTML API.
  setTimeout(() => {
    resolve('Success!'); // Yay! Everything went well!
  }, 250);
});

myFirstPromise.then((successMessage) => {
  // successMessage is whatever we passed in the resolve(...) function above.
  // It doesn't have to be a string, but if it is only a succeed message, it probably will be.
  console.log(`Yay! ${successMessage}`);
});
```

## References

- Understanding JS Event Loop and Promises by [Digital Ocean](https://www.digitalocean.com/community/tutorials/understanding-the-event-loop-callbacks-promises-and-async-await-in-javascript).
- MDN [JavaScript reference Global Objects Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- MDN [GitHub example of promise used to fetch an image](https://github.com/mdn/js-examples/blob/main/promises-test/index.html)

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
