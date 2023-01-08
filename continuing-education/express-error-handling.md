# Expressjs Error Handling

## Overview

Express can catch and process (handle) errors both synchronously and asynchronously.

A default Error Handler is included by default, based on the Middleware system.

An error thrown within a synchronous route handler or middle will automatically trigger the default Error Handler without any extra coding.

Asynchronous errors can easily be handled by adding a callback containing 'err' and 'data'. In the callback arrow function test for 'err' and send it to next so Express handles it, and if no 'err' then continue processing or just `res.send(data)`.

## Synchronous Automatic Error Handling Example

```javascript
app.get('/throw', (req, res) => {
  throw new Error('An error has occurred!');
});
```

Notes:

- Synchronous operation.
- Throwing within a route handler: Express Error Handler will handle it.
- Express code continues to run without crashing with call stack.

## Asynchronous Error Handling Passed To Express

```javascript
async function anAsyncMiddleware(inputParam, callback) {
  if (!inputParam) {
    callback('missing', 'email.'); // set callback parameters
    return; // exit this function
  } else {
    callback('good data', undefined);
    return; // exit after setting callback datum
  }
};

app.get('/foo', async function (req, res, next) {
  await anAsyncBar(req.query, (err, data) => {
    if (err) {
      res.status(400);
      next(err);
    } else {
      res.status(200);
      res.send(data);
    }
  });
};
```

Notes:

- Asynchronous function calls are made to an awaited Middleware.
- Async function call includes 'next'.
- Middleware takes inputParam and callback as args and somewhere it sets a value to err and/or data when it returns.
- Async function tests for value in 'err' and if so passes it to next() so Express Error Handler handles it.
- Aync function executes 'else' codeblock using returned 'data' and no error is thrown nor needs to be handled.
- Default HTTP Status Code is 500. Simply add res.status(n) where n is the appropriate status code for the situation.
- Middleware will continue collecting 'err' and 'data' values until it gets to the end of the function or a 'return' keyword.

## Random Notes For Later Categorization

To simplify using Promises and catching 'error' within code it is helpful to break-out all functionality into smaller executable functions, so that `then()` statements can be used to continue a Promise-resolve chain through to completion.

Find a reasonable spot to `trim()` String inputs so that they are ready to be handled natively in the Node environment, rather than trying to trim them later.

If your middleware produces more than one possible "good" result that the server path handler should manage, then just rely on a `then()` that handles a Resolve (not a Reject) response, followed by a `catch()`. The Catch should be configured to return a 5xx HTTP Status Code. The Then should be able to discern which HTTP Status Code (4xx or 2xx most likely) the Response should return, along with appropriate data.

If necessary, it is still possible to use `Response.locals` to pass data around within the server context.

## References

[Expressjs Error Handling](https://expressjs.com/en/guide/error-handling.html).

## Footer

Return to [ContEd Index](./conted-index.html).

Return to [Root README](../README.html).
