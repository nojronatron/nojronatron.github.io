# Notes from Duckett HTML and JS Books

## HTML Book Chapter 2: Text

Focus of this chapter are structural markup and semantic markup.  

### Structural Markup

Headings:  

- `<h1>` through `<h6>`  
- Require ending tags too  
- Exact size of headings will vary from browser to browser  

Paragraphs:  

- `<p></p>`  
- Browsers render each paragraph as a new line  

Bold and Italic:  

- `<b></b>`  
- Bold is good for use of *keywords*  
- `<i></i>`  
- Italics indicate the word(s) are said in a different way e.g. technical terms, names of ships, foreign words *[Ducket, pg.45]*  

Superscript and Subscript:  

- `<sup></sup>`
- Superscript applies to e.g. `9th` or in math when denoting 'to the power of'  
- `<sub></sub>`
- Subscript applies to characters often used in chemical notation like 'CO2'  

White Space:  

- Largely ignored beyond the first whitespace character  
- 'White space collapsing' causes multiple space characters to be compressed down to one in html text  

Line Breaks and Horizontal Rule:

These are 'empty elements' and require the closing tag character `/` within these single-tag elements.

- `<br />`
- Forces a line break  
- Content following this will be on a new line, similar to the paragraph tag but can be used within it  
- `<hr />`
- Causes a horizontal line to be drawn at the location the element is placed  

### Semantic Markup

These add information to a web page, and are used by screen readers and other assistive tools.

Strong and Emphasis:

- `<strong></strong>`  
- Indicates important content  
- `<em></em>`  
- Subtle change in meaning to the sentence  
- Text will appear italicized in the browser  

Quotations:

- `<blockquote></blockquote>`  
- Use these when quoting a large amount of information, like an entire paragraph or page of content  
- Render indented compared to a paragraph element  
- `<q></q>`  
- Use for shorter quotes like single or small number of words or amount of content  
- Meant to add quote marks `"` by browsers but IE does not  

Both blockquote and q include an optional `cite` attribute that should be configured with the URL of the source of the quotation

Abbreviations and Acronyms:

- `<abbr></abbr>`  
- attribute 'title' is used to add the fully unrolled term  
- html4 used an acronym element but html5 does not

Citrations and Definitions:

- `<cite></cite>`  
- Reference a piece of work when used for research, a book, etc  
- The enclosed content will be rendered as italicized  
- `<dfn></dfn>`  
- Used when explaining terminology  
- "Indicates the defining instance of a new term" *[Duckett, pg.54]*  
- Browsers could render as italicized content, but is not guaranteed  

Author Details  

- `<address></address>`  
- Use for contact details  
- Browsers render as italics  

Changes to Content

- `<ins></ins>`  
- shows content that has been inserted and is rendered with an underline  
- `<del></del>`  
- adds a 'strikethrough' to the content between the tags  
- `<s>`  
- indicates an inaccurate or deprecated content  

## HTML Book Chapter 10: Introducing CSS

CSS is like a set of rules the browser follows to layout, colors, size and shape of the content.  
CSS terminology:

- selector: an element, class, or id that the CSS declaration will apply to  
- declaration: the CSS code that will apply to the selector. Could be referred to as a 'css rule'  
- property: the CSS attribute that is getting configured  
- value: the value the CSS attribute will take on

### External CSS  

- href: set the path to the external css file  
- type: defines the document type, for example `text/css`  
- rel: short for relationship, mates the HTML page with a linked resource  

Web sites can reference multiple external stylesheets.  
Pages can share the same style sheet.  
Single place to edit style information for the entire site.  
Inline CSS rules can be eliminated (or minimized) thus cleaning-up the code.  
Is a best practice.  

### Internal CSS

Set CSS style rules for the current page.  
Usually stored in the `<head>` element, and/or in-line with html elements.  
Single-page websites might use internal css to keep everything together.  
Apply a few rules to a page with an external CSS ref, for specific situations (not a best practice).  
For code examples in a learning textbook like Duckett's HTML and CSS boook.  

### Selectors

Several portions of this were lifted from *[Duckett, pg.238]*  

- Universal: all document elements in the current page  
- Type: matches element names like `<h1>` etc  
- Class: matches class atribute of one or more elements, starts with a period like `.elClass`  
- ID: matches id attribute of an element, prefixed with the hash symbol like `#elId`  
- Child: matches direct child attributes. Selector usage: `li>a {}`  
- Descendant: matches element that is descendant of primary element. Selector usage: `p a {}`  
- Adjacent Sibling: matches element that is next sibling of another. Selector usage: `h1+p {}`  
- General Sibling: matches elemnt that is sibling of another. Does not have to be the direclty preceding element. Selector usage: `h1~p {}`  

### How CSS Rules Cascade

CSS Rules have an order of precedence:

- Last Rule: the latter of duplicate selectors takes precedence  
- Specificity: the more specific rule takes precedence  
- The `!important` indicates the rule is higher precendence than other rules that apply to the same element  

### Inheritance

Several portions of this were lifted from *[Duckett, pg240]*  

- some properties are inherited by child elements, and therefore the declarations can be simplified  
- some properties are NOT inherited by child elements such as border and background-color  

### Different Versions of CSS and Browser Quirks

CSS Definitions and releases overview:  

- 1996: CSS1.  
- 1998: CSS2.  
- Current, ongoing standard: CSS3.  

Meanwhile, there are many browser makes and models, and releases.

- Not all CSS declarations or properties will function as expected in all browsers  
- Always test every change when working with CSS  
- Use online tools  

Browser Quirks aka CSS bugs: A CSS property that displays in an unexpected way.  

Online CSS Validation Tools Reference *[Duckett, pg.242]*

- [Browser Cam](https://www.browsercam.com)  
- [Browser Lab](https://www.browserlab.adobe.com)  
- [BrowserShots](https://www.browsershots.org)  
- [CrossBrowserTesting](https://www.crossbrowsertesting.com)

CSS Bug Sites Reference *[Duckett, pg.242]*  

- [PositionIsEverything](https://www.positioniseverything.net)  
- [QuirksMode](https://www.quirksmode.org)  

## JS Book Chapter 2: Basic JavaScript Instructions

### Statements

Individual instructions are called Statements.  
A code block is contained between curly braces `{` and `}`  
Code blocks contain one or more Statements.  
Code blocks can contain other code blocks.  
JavaScript is CaSe SeNsItIvE  
Statements are separated by a new line, and should end with a semicolon  

### Comments

There are two types of comments: Multi-line and Single-line.  
Use comments to document the code, or to stop commented code statements from executing for testing.  

### Variables

Variables store data in memory.  
The JavaScript interpreter executes code statements one at a time, in order, and variables allow the interpreter to store values for future code statements to recall the variable to obtain the value.  
Data stored within a variable can be changed.  
There are two steps to storing data in a variable (memory):

1. The var keyword is used to define the variable name.  
2. The variable name is assigned a variable value using an assignment operator.  

Declare the variable: `var age;`  
Assign a value to them: `thingy = 11;`  

*Note*: A variable that is declared but not assigned has a type of 'undefined'.  

### Data Types

Some common data types are:

- Numeric: Integral or decimal number types.  
- String: Data types that contain letters, digits, characters, or all of the above.  
- Boolean: Binary values representing 'true' and 'false'.  

Additional types:

- arrays: Stores a list of multiple variable entries.  
- objects: Complex memory locations, discussed later in the book.  
- undefined: A memory location that has not had a value assigned to it.  
- null: Nothing (not to be confused with numeric 0).  

### Using Variables for Storage

Numeric: Do not use quotations, just a raw integer or decimal number, followed by a semicolon.  
String: Use single quotes `'` or `"` to encapsulate the string data, but do not mix them.

### Strings and Quotes

To include a quote insie of a string, encapsulate the entire string value with the other type of quote mark.
Example using single and double quotes:

```JavaScript
var message = '<p class="intro">Welcome to my website!</p>';
```

Example using the escape character `\`:

```html
<p class="post">My car has a name: \"Scooby\"</p>
```

### Store a Boolean

Assign a variable the keywords 'true' or 'false'.  
Do not use quotation marks for the keywords.  

```JavaScript
var switchIsOn = true;
```

### Creating Variables

Instead of taking two steps to declare a variable and assign it a value, both can be done in a single line:  

`var sales = 150000;`

Multiply your efforts by declaring and assigning multiple variables on each line!  

`var sales = 150000, year = 2022;`

*Note*: Assignment is not required when declaring multiple variables in a single statment.  

### Changing the Value of a Variable

Once a variable has been declared, the 'var' keyword is no longer necessary when assigning to the variable, or returning its stored value.  

```JavaScript
var stimpy = "cat";
stimpy = "cartoon character";
```

### Runes for Naming Variables

Varible names in JavaScript Can:

- begin with a letter, `$` or `_`; NOT a number  
- contain the same characters as the starting characters rule; NOT `-` nor `.`  
- not contain keywords or reserved JavaScript terminology  
- and are case sensitive: person and Person are two distinct variables in JS  
- and should be named after their purpose; of the data that they store  
- be made up of more than one word, so use camelCase styling  

### Arrays

Arrays store lists of variables.
Initialize arrays with the syntax `var myArray = [ ];`  
Initialize and assign values to an array of integrals with `var myArray = [ 1, 2, 3, 4, 5 ];`  
Alternately, use the array literal initialization: `var myArray = new Array( 1, 2, 3, 4, 5);`  
Determine the number of items in an array with `myArray.length;`  
Arrays are zero-based indexed storage types.  

Arrays include an indexer:  

1. Access the 3rd item in the array with the following syntax: `var arrayItem = myArray[2];`  
2. Assign the 3rd item in the array a new value: `myArray[2] = 100;`  

### Expressions and Operators

"An expression evaluated into a single value." *[Duckett, pg.74]*  
There are two types of expressions: Simple assignment; Return a single value from two or more variables.

1. Simple Assignment Expression: `var name = 'Dave';`  
2. Multi-value Single-return Expression: `var sum = 2 * 3;`  

Expressions rely on operators (see next subsection).

### Arithmetic Operators

The following symbols will perform mathematical operations on Number types:

- Addition: `+`  
- Subtraction: `-`  
- Multiplication: `*`  
- Division: `/`  
- Increment: `++`  
- Decrement: `--`  
- Modulus (return remainder): `%`  

The rules you learned about mathematical orders of operation are followed in JavaScript: PEMDAS.  

### String Operators

There is only one, the concatenation operator: `+`  
Use it to 'add' strings together!

```JavaScript
var name = "Tom";
var action = "ran";
var place = "Madrid, Spain";
var sentence = name + " the 3rd grader " + action + " from his home in Paris to " + place + ", overnight!";
console.log(sentence);
```

The concatenation operator will bring together the string values on either side of it, so the previous code block when executed would return the following to the console: "Tom the 3rd grader ran from his home in Paris to Madrid, Spain, overnight!"  

### Additional Operators

Comparison Operators and Logical Operators are covered in Chapter 4.

## JS Book Chapter 4: Decisions and Loops (up to switch statement)

This chapter will cover the topics of *evaluations*, *decisions*, and *loops*.  

### Decision Making

JavaScript can be coded to make decisions based on current variables, user input, etc.  
A flow chart is a great example of a decision tree, which could be used to help programmers write conditional statements.  
In order to make a decision, code statements must:

1. Evaluate an expression, returning a value, like a boolean.  
2. Perform the action(s) in the following code block(s), depending on the result.  

### Comparison Operators

Equal to `==` evaluates equality of *values* on each side of the operator, but not the types.  
Not equal to `!=` evaluates like Equal, but returns the opposite result.  
*Note*: For this class, avoid using 'loosely equals' and 'loosely not equals' because it will evaluate different types as 'loosely equal' and that might not be intended behavior.  
Strict equal to `===` evaluates the *type* *and* the *value* and returns true only if both conditions are true.  
Strict not equal to `!==` evaluates the opposite of Strict Equal To.  
*Note*: Stick with Strict evaluators to check that the type is the same before evaluating if the values are the same.  
Greater than `>` evaluates true if the left-hand value is larger than the right-hand value.  
Greater than or equal to `>=` evaluates the same way `>` and `==` do, and returns true if one or the other is true.  
Less than `<` evaluates true if the left-hand value is smaller than the right-hand value.  
Less than or equal to `<=` evaluates the same way `<` and `==` do, and returns true if one or the other is true.  

Enclosing brackets '(' and ')' are used to create a comparison operating statement.  
Operands sit on either side of the comparison operatork, between the enclosing brackets.  

```JavaScript
(savingsAccount >= withdrawlAmount)
```

Expressions with operands can be used on either or both sides of the comparison operator within enclosing brackets to perform the comparison on the results of the expressions.

```JavaScript
( (10 - 6) < (8 - 2))
```

### Logical Operators

AND: `&&` If both expressions return true then the operator result is true.  
OR: '||' If either expression returns true then the operator result is true.
Not: `!` Inverts a Boolean value. If a conditioni returns 'true', !condition returns 'false'.  

Both AND and OR are short-circuit evaluations: AND returns false as soon as a false if found; OR returns true as soon as a true is found.

### IF and IF-ELSE Statements

The IF statement is used to check a condition and executes the following codeblock only if the condition returns 'true'.  
IF statements can be followed by ELSE statements with another code block that executes when the IF conditioni returns 'false'.
