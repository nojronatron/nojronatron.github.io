# Notes from Duckett HTML and JS Books

HTML Book Chapters 3 and 13  
JS Book Chapters 2 and 4  

## HTML Book Chapter 3 Notes - Lists

Three types of lists are supported in HTML:  

- Ordered `<ol>`  
- Unordered `<ul>`  
- Definition `<dl>`  

Ordered and unordered list items are tagged with `<li>` elements.  
List Item tags can have a 'type' attribute added to change either:  

- Numbering type e.g. 1,2,3 vs a,b,c  
- Bullet style e.g. dots, arrows, etc  

CSS property `list-stype-type` can be used to change the numbering or bullet types.  

Definition Lists contain terms `<dt>` and definitions `<dd>`.  

- dt and dd have a 1+ to 1+ relationship.  
- There is not a one-to-one relationship requirement between dt and dd elements.  
- In effect, one term can have two definitions, or two terms can have the same definitions.  

Nesting Lists

- Create a new list inside of an existing one.  
- Browser will render the nested list indented from its parent.  
- Use CSS or element properties to adjust the icon/indicator for these sub lists.  

## HTML Book Chapter 13 Notes - Boxes

Topics Summary: Dimensions, Borders, Margins, Padding, and Show/Hiding of.  

### Dimensions  

Box Dimensions are:  

- Height  
- Width  

Measurements for sizing:  

- pixels: Absolute control of size.  
- percentages: Relative to browser window, or parent object e.g. another box.  
- 'em's: Bases size against the *font size* used within it.  

For flexibility, percentage and em are used.  

When content should be no smaller-than a certain width or height, use `min-width`.  
Conversely, use `max-width` to ensure the content/element does not get too large for the intended design.  
`min-width` and `max-width` can be used together to constrain content exansion or contraction.  
`min-height` and `max-height` are used similarly to the *-width properties.  

*Note*: If width is specified, padding and margin are also added (see below).

### Overflowing Content

Content can "spill over" from `min-width` and `min-height` settings of boxes.
By default the browser will allow the content to "spill" into other portions of the document or window.  
Properties `hidden` and n`scroll` can be set to tell the browser to handle the overflow more neatly.  

Hidden: Hides all content when an overflow is detected.  
Scroll: Overflow content is moved and a scrollbar is added to allow the user to scroll the content to read/access it.  

Older browsers used to shrink the font size when an overflow situation would otherwise occur. This is a good reason to use hidden or scroll to work around these back-level issues.  

### Border Padding Margin

These properties define the edge, inside edge, and outside edge of all sides of a box.  

- `padding`: Provides releif between the *content* and the *border*.  
- `border`: Every box has a border, and it can have `width: 0px` which makes it not visible, or visible with larger px sizes.  
- `margin`: Provides a gap between the *border* and other *boxes* or *elements* that are around it.  

Whitespace plays an important part is page readability and useability, so use these properties to your advantage.  

There are additional Border property settings:

- `border-width`: thin, medium, thick.  
- `border-style`: solid, dotted, dashed, double, groove, ridge, inset, outset, hidden.  
- `border-color`: colors can be set using rgb(), common color names, and other syntax.  

These and other settings can be 'shorthanded' to put all into a single line of the element properties:

``` html
head {
  border: 4px solid blue;
}
```

Borders actually have four sides, and these can be configured all as one, two at a time, all four simultaneously, or all four individually:  

- `border-width: thin medium;` causes the top and bottom border lines to be 'thin' and the left and right border lines to be 'medium'.  
- `border-style: dashed, solid, groove, ridge;` where these properties are applied in this order: TOP, RIGHT, BOTTOM, LEFT.  
- `border-top-style: ...; border-right-style: ...; border-bottom-style: ...; border-left-style: ...;`  
- `border-color: blue red white green` for colors.  
- `padding-top: 2px; padding-bottom: 4px;` for custom padding of the top and bottom of the box.  
- `margin-left: 40px;` for custom margin on the left side of the content.  

*Note*: Padding and Margin also support shorthand notation of just 2 values where the arguments represent top+bottom, and left+right, respectively.  

### Centering Content

Requirements:

1. Set the width of the box.  
2. Set the left-margin and right-margin to 'auto'.  
3. Older browser set: Add 'text-align' property but remember it is inherited by child objects.  

### Change Inline and Block Properties

The `display` property can be set to change the inline or block properties of elements.  

- `inline`: Causes the element to position itself in-line with the content.  
- `block`: Causes the element to position itself as a separate block between content.  
- `inline-block`: "Causes a block-level element to flow like an inline element while retaining other features of a block-level element." *[Duckett, pg.317]*  
- `none`: Causes element to not render on the document.  

*Note*: There is also a `visibility` property that can be set to 'hidden' or 'visible', rather than using `display: none;`.  

A wonderful example from *[Duckett, pg.317]* causes list item elements to list horizontally (inline) rather than vertically stack (block-level):

```html
<style>
  li {
    display: inline;
    margin-right: 10px;
  }
</style>
```

### Border Images

This property allows customizing a border, so the developer doesn't have to rely on the built-in `border-style` settings:

- An image can be applied to the border.  
- The image is repeated, once for each side (T, R, B, L) and for each corner between the sides.  

Three property settings are required to make this work:

- The URL of the image.  
- Where to 'slice' the image.  
- How to render the edges:
  - `stretch`  
  - `repeat`  
  - `round`  
- `border-width` greater than zero.  

Earlier browser versions of Chrome, Firefox, and Safari will need the following to render properly:

- `-moz-border-image`  
- `-webkit-border-image`  

### Box Shadows

Drop shadows on a box!
Must use at least horizontal or vertical offset, plus a color.

- horizonal offset: Negative values for left, positive for right-side shading.  
- vertical offset: Negative above, positive below.  
- blur distance: Drop Shadow is more like a border when this property is not set.  
- spread of shadow: Causes shadow to widen with positive values, shrink down with negative.  

*NOTE*: Be sure to accommodate Chrome, Firefox, and Safari with the following properties:

- `-moz-box-shadow`  
- `-webkit-box-shadow`  

### Rounded Corners

This effect can be applied to *any box*. The size of radius is defined in pixels.  

- Also use `-moz-border-radius` and `-webkit-border-radius` properties (not in spec but helps some browsers).

Can apply specific configuration to 1, 2, or 3 corners rather than all four:

```css
border-top-right-radius: npx;
border-botton-right-radius: npx;
border-bottom-left-radius: npx;
border-top-left-radius: npx;
```

*Shorthand* is also supported (TR, BR, BL, TL).  

### Eliptical Shapes

Uses `border-radius` creatively to define more complex curves.  
Configure horizonal and vertical distances with different values.  

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

## JS Book Chapter 4 Notes

Notes starting from Switch Statements in *[Duckett pg.164]* through the rest of Chapter 4.

### Switch Statements

Similar to if...else statement chains.  
My opinion is these are a bit tidier and a little easier to read through.  
Primary components:

- `switch (arg)`: 'arg' is the variable that will be tested against each 'case' value.  
- `case Object:`: Object will be compared to switch(arg) before executing the code block that follows.  
- A code block that includes `break;`  
- `default:` followed by a code block to run if no other cases are matched.  

### Type Coercion and Weak Typing

Data Types are important in JavaScript, even though developers do not need to strictly declare types when initializing variables.
Type coercion: JS statements can be written to 'coerce' a type to be like another type.

From *[Ducket, pg166]*:

```javascript
('1' > 0)
// returns true because the string '1' is convered to a Number type during evaluation
```

Weak Typing: Term used to describe how javascript allows type coersion and simple conversions.
Type Coercion can cause unexpected results so *use it carefully*.  

Various Data Types in JavaScript (Type: Purpose)

- string: Text  
- number: Number  
- Boolean: true or false  
- null: empty value  
- undefined: A declared but unassigned variable  

### Truthy and Falsy

When something is 'truthy', it means that something can be resolved to Boolean 'true'.  
Similarly, when an item is 'falsy' it can be resolved to Boolean 'false'.  

Falsy Values are things like boolean false, 0 (zero), empty strings, using a divisor of type String, NaN (not a number), an unassigned variable.

Truthy Values are things like boolean true, Number with a value != 0, and non-empty Strings (including Strings with values of '0', 'true', or 'false', because the string is non-empty), valid number calculations.

### Checking Equality and Existence

Unary Operator: Returns a result from a single operand.  

Strict Equality operators result is fewer unexpected results. This is due to type coercion.

To ensure something exists, check for the following:

- null?  
- undefined?  
- 0?  
- empty String?  
- NaN?  
- false?  

### Short Circuit Values

Quoted from *[Ducket, pg.169]* (because it is written so succinctly):

"""Logical operators are processed left to right.
They short-circuit (stop) as soon as they have a result - but they return the value that stopped the processing (not necessarily true or false)."""

The OR operator `||` will short-circuit as soon as a truthy value is returned.  
The AND operator `&&` will short-circuit as soon as a falsey value is returned.

### Loops and Loop Counters

Three types of loops using these keywords:

- FOR  
- WHILE  
- DO WHILE  

All three types have keyword followed by the conditional statement or counter, followed by opening and closing braces for code statement(s).  

The Conditional in a 'For' loop contains:

- A variable initialization: `var idx=0;`  
- A condition that will break the loop: `idx > 11;`  
- An update statement or incrementor: `idx++;`  

Additional keywords:

- 'break': causes loop to terminate and drop out of the loop codeblock to the parent level.  
- 'continue': ceases current iteration to re-check the conditional statement without processing any more code statements or blocks.  

*Note*: The browser will wait for javascript loops to complete, halting all other processing, so be certain your loops will exit cleanly and efficiently.  

It is best practice to define variables outside of a loop whenever possible, to avoid having them reset or altered unexpectedly within the loop.

### For Loop

An example For loop:

```javascript
for (let int=0; int < 10; int++) {
  console.log("I'm loopy!");
}
//  I'm loopy! will be logged to console 10 times then the code will exit.
```

### While Loop

An example While loop:

``` javascript
let idx=10;
while (idx > 0) {
  console.log("Counting backwards! " + idx);
  idx--;
}
//  On each iteration, the text and the value of idx will be logged to console, counting backwards until idx == 1.
```

### Do While Loop

An example Do While loop:

```javascript
let idx=1;
let top=26;
do {
  console.log("Counting odd numbers " + idx);
  idx += 2;
} while (idx < top);
//  idx starts at 1 and is logged to the console with the message, as are every 2nd number until the idx is > 25 then the loop will exit.
```
