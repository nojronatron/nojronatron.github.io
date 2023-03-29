# Promises

Many languages utilize Promises to manage asynchronous operations.

Review the purpose, use, and gotchas of Promises.

Develop a list of key takeaways that the future me can review.

## Overview

A Promise is:

- A proxy for a value that might not yet be known.
- Useful for associating handlers with an eventual success value or failure reason coming from an asynchronous method.
- Guaranteed to be asynchronous.

A Promise has one of 3 states:

- pending: Initial state that is neither fulfilled nor rejected.
- fulfilled: Operation was completed successfully. Returns with a value.
- rejected: Operation failed. Returns with an error.

Note: There is a 'settled' state which is short-hand for fulfilled or rejected, and not pending.

## Construction

Only construct a new Promise instance to wrap functions that do not already support promises.

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

- Appends a handler to the promise and returns a new promise tha tis resolved when the original promise is resolved. Handler is called when the promise is fulfilled in either fulfilled or rejected cases.

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

## Takeaways

Functions that will return a Promise should either be awaited or handled by chaining Resolve and Catch.

Think of Promises as a way to leverage the asynchronous handling pipeline of the JavaScript Message Queue in the Event Loop.

- Refresher on the [JS Event Loop et al](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)

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
