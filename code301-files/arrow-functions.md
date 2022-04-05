# ES6 Arrow Functions

ECMAScript 2015 aka ES6 Arrow Functions notes taken while reading MDN and caniuse.com  

## MDN Docs on Arrow Functions

MDN Docs: [Arrow Function Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)  

### Function Expression

Recall that the function keyword defines a Function Expression.  
The syntax is: ` function [name]([param1[,paramN]]) { statements; };`  *[Mozilla Developer Network Documentation]*  

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

#### Parens and Parameters

```javascript
(parm1, parm2) => expression
```

```javascript
() => expression
```

#### Braces and Code Blocks

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

Straight from *[MDN]*:  

```javascript
params => ({foo: "a"}) // returns object {foo: 'a'}
```

#### Other Advances Purposes

- Rest Parameters. There might be many of them.  
- Default Parameters. Some inputs should default if not assigned.  
- Destructuring within params. *An advanced topic* to me.  

## Caniuse.com Summary Notes

Support for ES6 Arrow Functions is pretty vast, even on mobile and specialy platforms.  

*Note*: IE (of course) and Opera Mini are two outliers as they do not support it.

Reference: [caniuse.com](https://www.caniuse.com)  

## Footer

Back to [readme.md](../README.html)  
