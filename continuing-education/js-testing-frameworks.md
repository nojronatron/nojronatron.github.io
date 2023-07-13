# Exploration of JavaScript Testing Frameworks

I've used Jest, and run into Mocha and Chai many times in the last year or so. This is a quick exploration of the differences between the three.

## Table of Contents

- [Jest](#jest)
- [Mocha](#mocha)
- [Chai](#chai)
- [References](#references)
- [Footer](#footer)

## Jest

I already have a fair amount of experience with Jest, but I expect to learn a few more things here.

[Jest API](https://jestjs.io/docs/api)

### Jest Basics

1. `npm install --save-dev jest`
1. Identify the file to test e.g. `myModule.js`
1. Create a test file e.g. `myModule.test.js`
1. Import the file to test to the test file e.g. `const myModule = require('./myModule');`
1. Update `package.json` to include a test script e.g. `"test": "jest"`
1. Run the test script e.g. `npm test`

### Jest Command Line

1. Install Jest globally to call it from the command line: `npm install -g jest`.
1. Run Jest and get native OS output: `jest myModule --notify --config=config.json`.

Jest [CLI Options](https://jestjs.io/docs/cli)

### Jest Configuration

`jest --init` creates a baseline configuration file.

### Jest With Babel

1. `npm install --save-dev babel-jest @babel/core @babel/preset-env`.
1. Create a babel config file (see example below from _[JestJS.io]_).

```javascript
module.exports = {
  presents: [
    [
      '@babel/preset-env',
      {
        targets: {
          node: 'current',
        },
      },
    ],
  ],
};
```

See [Babel Docs](https://babeljs.io/docs/en/) for Babel configuration details.

_Note_: `babel-jest` is installed automatically with Jest and will automatically transform files for you. This behavior can be disabled by setting configuration option `transform: {}`.

### Jest Interop With Other Libraries and Frameworks

- Webpack: Jest can be used, but can be challenging. See Webpack docs for details.
- Vite (+ Native ESM): Jest is not fully supported due to the Vite Plugin System. There is a `vite-jest` module, with other limitations. See the vite guide for details.
- Parcel bundler: Zero-configuration, works well with Jest. See Parcell official docs for info.
- TypeScript: Supported, via Babel. See instructions below.

#### Jest and TypeScript

1. `npm install --save-dev @babel/preset-typescript`.
1. Create a babel config file `babel.config.js`.
1. Add `@babel/preset-typescript` to list of presets.

Example babel.config.js from _[JestJS.io]_:

```javascript
module.exports = {
  presets: [
    ['@babel/preset-env', { targets: { node: 'current' } }],
    '@babel/preset-typescript',
  ],
};
```

_Important_: TypeScript is not directly supported by Jest, and Babel transpiles TS to JS prior to Jest executing tests. This means type-checking is not done.

Options are to:

- Use `ts-jest` to enable type-checking Jest tests.
- Run `tsc` separately or as part of the build process.

See [JestJS TS Types Testing](https://jestjs.io/docs/getting-started#type-definitions) for more info.

### Jest Matchers

Matchers are used to test values.

Always use the most precise matcher available.

Common Matchers:

- `toBe()`: Strict equality (===).
- `toEqual()`: Deep equality e.g. recursive matching in an array-like object.
- `not`: Inverts the matcher, e.g. `expect(0).not.toBe(1)`.
- `toBeNull()`: Matches only null.
- `toBeUndefined()`: Matches only undefined.
- `toBeDefined()`: Matches anything that is not undefined.
- `toBeTruthy()`: Matches anything that is not falsy.
- `toBeFalsy()`: Matches anything that is falsy.

#### Jest Floating Point Equality

Use `toBeCloseTo` to compare floating point numbers. This avoids match errors due to rounding.

#### Jest String Matching

Use `toMatch()` and `not.toMatch()`.

The function accepts Regular Expressions.

Does _not_ default to doing a full string match, e.g. can find a substring that matches the regex.

#### Jest Matching Arrays And Iterables

Use `to.Contain(string)` for arrays and iterables.

#### Jest Error Matching

Use `.toThrow([error])`.

Error is an optional argument. If provided, the error message must match the string or regex provided.

#### Jest Matcher Reference

[Jest Expect API Documentation](https://jestjs.io/docs/expect).

### Jest Asynchronous Testing

Jest supports testing asynchronous code using these approaches:

- Promises: Add the matcher to the `.then()` block.
- Rejected Promises: Use the `.catch((error) => {...})` code block.
- Async/Await: Within the test definition, put `async` in front of the lambda expression, then use `await` in from of the awaitable function call.
- `.resolves` and `.rejects`: Compatible with Async/Await usage. Simple pre-pend resolves or rejects keywords to the intended matcher, as part of a `return` statement.
- Callbacks: Include `done` as an argument to the test definition. Call `done()` when the test is complete. Place a `done()` in both the success and failure code blocks e.g. `try{}` and `catch(error){...}`.

_Note_: Do _not_ mix Promises and Callbacks else the test is guaranteed to fail.

### Jest Test Setups and Cleanups

Repeat setup and cleanup code using `beforeEach()`, `afterEach()`, `beforeAll()`, and `afterAll()`.

Simply run the code in the setup or cleanup block that should run:

- Before all test: `beforeAll(() => {...})`
- Before each test: `beforeEach(() => {...})`
- After every test: `afterEach(() => {...})`
- After all tests: `afterAll(() => {...})`

#### Scoping Setups and Cleanups

Place the `beforeEach()` etc statement within the `Describe` block for the test of tests the setup/cleanup should apply to.

_Note_: Scoping setups/cleanups like this can cause unexpected order-of-operations. See [JestJS Setup Teardown Order of Operations](https://jestjs.io/docs/setup-teardown#order-of-execution) for more.

#### Jest Single-Test Run

Use `test.only()` to run a single test. This can be helpful to isolate a test run to a specific test for debugging.

### Jest Mocking

Tests links between code "by erasing the actual implementation of a function, capturing calls to the function..., and allowing test-time configuration of return values."

Two ways to mock functions:

1. Create a mock function for use in the test.
1. Write `manual mock` to override a dependency.

#### Jest Mock Function

1. Import the module to test (SUT).
1. Create a function to store in the imported module function's callback.
1. Call the SUT and supply it input arguments including the mockCallback function.

```javascript
// create a mock function
const mockCallback = jest.fn(() => {...});
```

## Mocha

Claim: "Simple and Fun". Fair enough.

### Mocha Basics

Runs on:

- Node.js v14.x and higher.
- Browser (see compatibility list).

[In the browser](https://mochajs.org/#running-mocha-in-the-browser).

Note: When run in the browser, an HTML report is produced.

Can be used to test synchronous and asynchronous code.

Can be run [in a command line](https://mochajs.org/#command-line-usage).

Install: `npm install --save-dev mocha`

```javascript
// basic test code example lifted from https://mochajs.org/#getting-started
var assert = require('assert');
describe('Array', function () {
  describe('#indexOf()', function () {
    it('should return -1 when the value is not present', function () {
      assert.equal([1, 2, 3].indexOf(4), -1);
    });
  });
});
```

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

Hooks can be Sync or Async.

Use Hooks to clear a database and set test data before each test.

Root Hooks: Any Hook set at the top Scope of the test file.

[Root Hook Plugins](https://mochajs.org/#root-hook-plugins): Preferred over Root Hooks.

## Chai

Chai is an assertion library. It can be used with Mocha, or any other JS testing framework.

Note: The [GitHub Repo](https://github.com/chaijs/chai) seems to have very little recent activity. All branches are considered 'stale' and the most recent open PR is dated February 2022. This doesn't mean Chai is not useful, but it does mean that it is not actively being developed and could become obsolete sooner than later.

### Chai Install

Install as a dev dependency using the `*` version tag to ensure it is always the latest.

1. `npm install --save-dev chai`
2. Edit `package.json` and change the version to `*`.

Chai Browser Build can be included in your testing suite as a globally accessible object.

`<script src="chai.js" type="text/javascript"></script>`

Browser support includes:

- IE 9+ (`should` style assertions not supported)
- Chrome 7+
- FireFox 4+
- Safari 5+

### Chai Assertion Styles

Pick _one_ and stick to it!

- Assert: A full assertion API exposed through the `assert` interface. Similar to node.js: `assert.typeOf(foo, 'string');`
- BDD: Behaviour Driven Development. Sub-styles are `expect` and `should`.
- Configuration

#### Chai BDD Expect and Should

Expect and Should:

- Both allow chaining e.g. `expect(foo).to.be.a('string').with.lengthOf(3);`
- Expect allows adding a failure message e.g. `expect(answer, 'topic: meaning of life should be 42').to.equal(42)`
- Should starts chaining differently than Expect e.g. `foo.should.be.a('string).with.lengthOf(3)`

Differences importing Expect vs Should:

- Chai import: `var chai = require('chai');`
- Chai with Expect: `var chai = require('chai'), expect = chai.expect;`
- Chai with Expect and Should: `var chai = require('chai'), expect = chai.expect`, `should = chai.should();`
- Start an Expect chained assertion using the Expect function. Compatible with _all_ browsers and node.
- Should interface extends `Object.prototype` so assertions are available via a single _getter_. Compatible with _modern_ browsers and node.

Should is limited when it comes to checking Object instances:

```javascript
// example provided by Chai documentation
var should = require('chai').should(); // use of var provides access to helpers
db.get(1234, function (err, doc) {
  should.not.exist(err); // this 'throws' because should cannot operate a non-instance
  should.exist(doc); // we get here because doc is an instance
  doc.should.be.an('object'); // safely verify doc is of type 'object'
});
```

Additional Helpers:

- should.exist
- should.not.exist
- should.equal
- should.not.equal
- should.Throw // Pascal case!
- should.not.Throw

#### Chai Should In ES2015

Example:

```javascript
// cannot use a chain to import should
// instead use a 2-liner
import chai from 'chai';
chai.should();

// or use this special syntax
import 'chai/register-should';
```

### Chai Configuration

- config.includeStack = boolean: Configure whether Stack Trace is included in Assertion Error messages. Default: false.
- config.showDiff = boolean: Include `showDiff` flag in thrown Assertion Error messages. Default: false.
- config.truncateThreshold = number: Value truncates error messages for actual and expected Assertion Error messages. Default: 40.

### Chai Plugin API

See the [tutorial](https://www.chaijs.com/guide/plugins/) on this topic.

Summary:

- Write a plugin to validate input data.
- Plugins can assert schema validations.
- Plugins can be used to verify DOM element behavior.
- Compatible with any synchronous task.
- _Must add the api_ that is _not_ included in the import statement: `chai.use(function (chaiExport, utilityMethods) {...});`
- ChaiExport: This is the result of the import/require statement.
- utilityMethods: An object containing the wanted utility methods.
- Utility Methods are available in `./helpers/model`.

Example configuring Chai Plugin API:

```javascript
var chai = require('chai'),
  chaiModel = require('./helpers/model'),
  expect = chai.expect;
chai.use(chaiModel); // similar to how Express.js initializes API Utilities
```

There are _many many_ plugins already available for Chai, check them out [here](https://www.chaijs.com/plugins/).

#### Building a Helper

There is a [helper tutorial](https://www.chaijs.com/guide/helpers/) at the Chaijs.com website.

Remember creating Object Constructors in javascript? Check this out:

```javascript
function Model(type) {
  this._type = type; // set the type based on the initialization argument
  this._attribs = {}; // initialize an empty object for this instance
  Model.prototype.set = function (key, value) {
    this._attribs[key] = value; // a lot like the cache model introduced in Code 301
  };
  Model.prototype.get = function (key) {
    return this._attribs[key]; // return using the property selector
  };
}

var testPerson = new Model('person');
testPerson.set('name', 'John Doe');
testPerson.get('name'); // returns 'John Doe'
```

Helper Model could represent an instance in any ORM, for example.

Once the Model exists, you can:

- `addProperty()`: API is fully documented in the [Chaijs.com documentation](https://www.chaijs.com/api/plugins/#method_addproperty).
- 'addMethod()`: API is fully documented in the [Chaijs.com documentation](https://www.chaijs.com/api/plugins/#method_addmethod).

Chai allows construction of a 'Language Chain' that can target either a method or a property of a Model.

- There are rules about this.
- Try not to use double-negatives.
- Avoid testing if a Model is _not_ something and instead assert that is _is_ something.

There is a bunch more at [Chai Resources](https://www.chaijs.com/guide/resources/).

### Flags

- `utils.flag`.
- Functions as a getter.
- ALSO functions as a setter.
- object flag: `var obj = myAssert._obj;`
- `ssfi`: Start stack function blocks errors displaying callback stacks.
- `message`: Additional error information is included.
- `negate`: Is set when `.not` is in the chain.
- `deep`: Is set when `.deep` is in the chain. See `equal` and `property`.
- `contains`: Set when `include` or `contains` is used. Changes behavior of `keys`.
- `lengthOf`: Set when `length` is used as property. Changes beahvior of `above`, `below`, and `within`.

### Assertions and Error Messages

Asserts accept six arguments:

- boolean result of truth test
- string error message when 1st arg is false
- string error message when first arg is true
- expected value (default: \_obj)
- boolean displayDiff if first arg is false

Compose an error message using template tags:

- Three available: (see below).
- Allows dynamic creation of error messages.
- Templates are replaced with stringified components of the target object.

The Three Template Tags:

- `#{this}`: The \_obj of the assertion.
- `#{exp}`: The expected value (if provided in the assert).
- `#{act}`: The actual value. Defaults to `_obj` but can be overwritten.

## References

[MochaJS](https://mochajs.org/)

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root README](../README.html)
