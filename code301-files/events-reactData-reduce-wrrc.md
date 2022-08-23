# In Class Notes

## Warm Up

C#: Determine output of the function

Creates a new array.  
Compares parameter position to the length of myArray (length: 5).  
If position value is greater than myArray length then return string "not valid index".  
If postion value is lower than myArray length then continue.  
Enter a loop that iterates from 0 to one-less-than array length.  
Inside the loop the for-loop index is compared to position  and if the same then adds value's value to myArray.  
After the loop ends it returns a string to the caller with the message, indicating the value was accepted.  

### Outputs

Value("sample string", 5); => "Not a valid index"  
Value("another string", 2); => "Your value of 2 was accepted"  

## Code Review

I put mine up for review.
Within a Form.Select, onChange event is called whenever any option element is selected, because the Form.Select is the *parent* to the option elements, so it catches the event.  
An explicit default value *can* be set by adding attribute to an option element, otherwise the first-child option element will be the implicit default.  
OnSubmit events: Consider using event.preventDefault.  
Non-onSubmit events: Don't need to add event.preventDefault.  
Filter *original* data then re-assign the output value to the state.
When data has already been filtered, and it gets filtered again, it *could* filter *everything out*.
Consider using `let result = parseInt(event.target.value);` to pull Numbers directly into a variable.  

### Jons Bug

Description: Clicking beast hearts adds a count. However, the index is not associated with the beast, rather the *position in the filtered array*.  
Solution: Use the object._id (if it has one) to track the beasts, strictly.  

## General React Comments

Where did the data come from?

- Import: Component got data from another file.  
- Props: Component got data from its parent component.  
- State: Component *owns* the data and is only one allowed to edit it.  
- this.someVar: A property on the current component, and could be any value (or object).  

Who can change the data?  

- Import: Data cannot be changed by the component.  
- Props: Data cannot be changed by the component.  
- State: Data *can* be changed by the component.  

## Code Challenge - Reduce
  
Check out [MDN on reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)  

### Facts About Reduce

Takes two arguments: Callback Function and optional Initial Value.  
Is a *recursive* function.  
Calls the Callback Function on each element in the array *after the first element*.  
Setting an initial value "starts" the operation at that value.  
Does *not* change the value of the input array.  
Returns a *new array* with the results of execution.  
Return is *not* implicit, a return statement *must be added*.  
*Recommended*: Add the return statement on a separate line from the operation.  
Similar to `Array.prototype.map()` but more can be done with `Array.prototype.reduce()` like returning objects etc, whereas map can only return an array.  

### Simple Example

```javascript
let numbers = [2, 7, 5, 8, 4];
let total = numbers.reduce((runningTotal, currentNumber) => {
  // first iteration loads runningTotal with currentNumber (basically)
  return runningTotal + currentNumber;
})
console.log(`total: ${total}`);
```

Parameters:

- 1st: Callback Function.  
- 2nd: Initial value.  

### Initial Value

```javascript
let numbers = [2, 7, 5, 8, 4];
let initialVal = 29;
let total = numbers.reduce((runningTotal, currentNumber) => {
  // first iteration loads runningTotal with currentNumber (basically)
  return runningTotal + currentNumber;
}, initialVal);
console.log(`total: ${total}`);
```

Initial value can be a String or Number!  
Initial Value can be an empty array!  
Initial Value can be an empty object!  

Use "bracket-notation" to get the property from the current iteration in the loop:

> `{[film.title]: film.episode}`

### Cautions

DO NOT:

- Define a callback function that adds to the input array. Reduce will *not* operate on them.  
- Define a callback function that mutates the input array. Unless you are sure you want reduce to operator on values that *might not be operated on yet* or *might have already been operated on* by reduce.  
- Reduce will not iterate over indexes where the value has been deleted.  

## Lab 05 Assignment

### Goals

Work with someone else's code.  
Have fun while doing this!  
Use Trello board to manage tasks.  

### To Do

Create the React app locally, set up a GH Repo for it, then push it to origin.  
Take what you already know, go in, and figure out what you can of what is there.  
Use the [Trello](https://www.trello.com) board to manage tasks within this assignment, there are a bunch of tasks already created for you to do. Make the Trello Board *public*.  
Deploy the GH Repo to Netlify?  

### Find and Change Code

In the industry, rarely will you create a project from scratch.  
Often times operating on other people's code.  
The 301 Final Exam is an assessment of your ability to figure out someone else's code and expand on it.  

### Advice

Prioritize your efforts to get things done effectively.  
Timebox your efforts to call and end to a task and *move on*.  
Don't worry about the React v.18 error when rendering the site.  
SASS (SCSS) is CSS plus *variables*.  

### Intro the Web Request-Response Cycle

The Client: Your computer, and for these classes mostly means 'web client'.  
API: Client sends requests to an API and receives responses *from* the API.  
Front-end and Back-end: Line is drawn between personal computer and (servers and APIs).  
React runs *entirely* on the back-end.  

#### WRRC

Web Request-Response Cycle.  
Headers: Meta data and Access Tokens.  
Body: Data of some kind e.g. something to add to a database.  
Cache: Repetitive requests get quicker responses and the network traffic will be reduced on the back end.  
