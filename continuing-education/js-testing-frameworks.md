# Exploration of JavaScript Testing Frameworks

I've used Jest, and run into Mocha and Chai many times in the last year or so. This is a quick exploration of the differences between the three.

## Jest

This will be filled in at a later time.

## Mocha

### Mocha Basics

Runs on:

- Node.js v14.x and higher.
- Browser (see compatibility list).

[In the browser](https://mochajs.org/#running-mocha-in-the-browser).

Note: When run in the browser, an HTML report is produced.

Can be used to test synchronous and asynchronous code.

Can be run [in a command line](https://mochajs.org/#command-line-usage).

Install: `npm install --save-dev mocha`

### Mocha Configuration

JS, YAML, JSON, or in package.json.

Config file can be specified using `--config <path>` option. Assumes JSON unless extension is specified.

Package.json can be specified using `--package <path>` option.

### Mocha Errors

A Code and Message are provided for Mocha-specific errors. Use the _code_ not the message to determine the cause.

### Mocha Plugins

There are plugins for editors like IntelliJ.

### Mocha Sync and Async

Asynchronous code:

- The callback `done()` within an `it()` block tells Mocha to wait for the function to be called to complete this test.
- Callback `done(err)` accepts an error argument for handling.
- Instead of `done()` return a Promise (usually provided by the API under test).
- Calling `done()` _and_ returning a Promise will result in an exception.
- Alternatively, use [async-await](https://mochajs.org/#using-async-await) (wrapped Promises) in the tests.

Synchronous code:

- Omit the callback and Mocha will just move to the next test.
- Remember to include `.should.be` or `.should.equal` in the test (chaining).

_Avoid_ using arrow functions (lambdas). This is due to the fact that `this` context is changed and does not include the Mocha context.

### Mocha Test Setup and Teardown

AKA "Hooks".

`before()`, `after()`, `beforeEach()`, `afterEach()`

From the website:

```javascript
describe('hooks', function () {
  before(function () {
    // runs once before the first test in this block
  });

  after(function () {
    // runs once after the last test in this block
  });

  beforeEach(function () {
    // runs before each test in this block
  });

  afterEach(function () {
    // runs after each test in this block
  });

  // test cases
});
```

## Chai

This will be filled in at a later time.

## References

[MochaJS](https://mochajs.org/)

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root README](../README.html)
