# ES6 Arrow Functions

ECMAScript 2015 aka ES6 Arrow Functions notes taken while reading MDN and caniuse.com  

## MDN Docs on Arrow Functions

MDN Docs: [Arrow Function Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)  

### Function Expression

Recall that the function keyword defines a Function Expression.  
The syntax is: `function [name]([param1[,paramN]]) { statements; };`  *[Mozilla Developer Network Documentation]*  

Name is the plain-english (or complicated gibberish) word by which the function can be referenced.  
Parameters represent arguments to be passed *in* to the function.  
There can be zero or one or many parameters.  
A Code Block of statement is executed when the function is 'called'.  
Functions always return something:  

- undefined: AKA a void return type.  
- type: Some type, custom or built-in, returned to the 'caller'.  

### Arrow Functions

A compact alternative to function expressions.  

Not-so-good Aspects:  

- Cannot be used as Constructors.  
- Cannot have line breaks in the definition.  
- Cannot use 'this'. Assume 'this' in an arrow function means 'Window'.  
- Should NOT be used as prototype or other methods; They do not *have* a prototype property.  
- Not able to use Yield return type within its body; *however* child-functions within the codeblock *can* use Yield. Arrow Functions cannot be used as 'Generators' because of this Yield statement limitation.  
- Not suitable for 'call', 'apply', and 'bind' methods. These 'add.' methods change the scope of a method call using 'obj' as the first or only parameter in their params list.
- Arrow Functions might alter order-of-operations, so *be aware* when using these together.  

### How To Construct Arrow Functions

`param => expression`

Note the following:  

- Return is implied.
- Parameters are declared to the left of the arrow.  
- Parentheses are necessary when *zero* or *more than one* param are needed.  
- Braces are required when 'statement' needs to be a 'code block' i.e. More than one code statement is necessary.  
- Results of an arrow function can be assigned directly to a variable (example follows).  

```javascript
let myWord = 'bar';

function foo(word){
  return `FOO ${word}.`;
}

let bar = word => `FOO-FOO ${word}.`;

bar (myWord);
'FOO-FOO bar.'
```

### Transform a JS Function to an Arrow Function

ES 6.0 defines a function as a variable that uses the keyword 'function', followed by parentheses for a parameters list, followed by a code block.

Arrow Functions:

- Do NOT use the keyword 'function'.
- Parenthesis are necessary but could be empty, or have 1 or more params.
- An expression without braces and without a 'return' keyword, but automatically returns the result of the expression.
- Code Block contains executable code within braces, ending with the 'return' keyword.

Example:

```javascript
function randomNumber() {
  return Math.random;
}
```

...can be rewritten as an arrow function:

```javascript
randomNum = () => Math.random;
```

#### Parens and Parameters

Parenthesis are required to contain the input parameters, or no parameters at all.

```javascript
(parm1, parm2) => expression
```

```javascript
() => expression
```

#### Braces and Code Blocks

Braces are *not* required for single statement expressions that do not overflow to the next line.

- The return is *implied*.

Multi-line statements *require*:

- Body braces *and*  
- Return keyword.  

```javascript
() => {
  let expression1 = expression;
  return expression1;
}
```

```javascript
param => {
  let result = expression + param;
  return result;
}
```

#### Return an Object Literal

Straight from *[MDN, 'Arrow_functions']*:  

```javascript
params => ({foo: "a"}) // returns object {foo: 'a'}
```

Object Literals have many uses, including:

- Rest Parameters. There might be many of them.  
- Default Parameters. Some inputs should default if not assigned.  
- Destructuring within params.  

#### Advanced Uses

Arrow Functions are useful for many purposes including:

- Simplified single-line functions.
- Event hanlders.
- Callbacks.

#### Summarized Configurations

Arrow Functions can be written in several different ways, with options on when to use parenthesis and braces.

Parentheses:

- Use when *zero* or *more than 1* parameters are necessary.  
- Do *not* use for *single parameter* arrow functions.  
- Use in the *code block* when braces are needed to identify *an object definition*.  

```javascript
/* zero parameters requires parens */
const alpha = () => `Hello World!`;

/* multiple params requires parens */
const bravo = (name, age) => `${name} is ${age} years old.`;

/* single param does not require parens */
const charlie = name => `Her name is ${name}.`;

/* surround object literal with parens */
const delta = (name, age) => ({
  name: name,
  age: age,
});
```

Braces:  

- Do *not* use when following the arrow with a single code statement.  
- Use when *multiple* statements are needed in the code block and *include* the *return statement*.  

```javascript
/* single code statement does not require braces */
let echo = () => `Hello Hello World World!`;

/* multi-line code block requires braces */
let foxtrot = (length, width) => {
  let ttlLen = length * 2;
  let ttlWid = width * 2;
  let perimeter = ttlLen + ttlWid;
  return `Perimeter: ${perimeter}`;
}
```

## Caniuse.com Summary Notes

Support for ES6 Arrow Functions is pretty vast, even on mobile and specialty platforms.  

*Note*: IE (of course) and Opera Mini are two outliers as they do not support arrow functions.

## References

[caniuse.com](https://www.caniuse.com)

[MDN Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

WebDevSimplified [ES6 Arrow Functions Tutorial on Youtube](https://www.youtube.com/watch?v=h33Srr5J9nY)

## Footer

Back to [readme.md](../README.html)  
