# Readings for 15Apr2022

[Thinking in react](https://reactjs.org/docs/thinking-in-react.html)

## Start With A Mock

Mock-up of what a site page looks like.
An example of JSON data that the page will consume, i.e. from an API.

## Break Up The UI

Think of the UI as a Component hierarchy.  

1. The entire mocked-up page.  
2. Header or top-of-page component(s).  
3. An output area or main body of the page, which could be thought of as a table.  
4. Row headings.  
5. Possibly iterable row content.  

## Build a Static React Site

Start with the main page that handles the UI layout but has no interactivity.  
Add Components that reuse other components and pass props but *do not use state* in this version.  
Start building top-down or bottom-up, whatever your preference.  

You should end up with a number of components that are used to render the data in the main page.  

### ID the Minimal Representation of UI State

Enable triggering changes to underlying data using state.  
Determine the absolute minimum representation of state that will enable all necessary computations, on-demand.  

To help decide what items should be held in state, ask three questions:  

1. Is it passed-in from parent via props? Not state.  
2. Does it remain static over time? Not state.  
3. Can value be computed based on other state or props? Not state.  

Which of the following items should be held in state?  

- List of products: Not state if passed-in as props.  
- Search text user has entered: Change over time and cannot be computed so *probably state*.  
- Value of a checkbox: Change over time and (generally speaking) cannot be computed so *probably state*.  
- Filtered list of products: Computed from user input so is not state.  

### ID Where State Should Be

A component that *owns* a state will be allowed to *mutate it*.  
Mutation means to change the value of a variable or property.  
It can be difficult to figure out which component should actually own what state.  

Direct from the article:

For each piece of state in your application:

- Identify every component that renders something based on that state.
- Find a *common owner* component (a single component above all the components that need the state in the hierarchy).
- Either the common owner or *another component higher up* in the hierarchy should own the state.
- If you can’t find a component where it makes sense to own the state, *create a new component solely for holding the state* and add it somewhere in the hierarchy above the common owner component.

### Add Inverse Data Flow

Child and grand-child components that need to update state higher up the hierarchy need to be handed *callbacks* to functions within the Component that holds the state, allowing the state change to occur.  

### Interesting Notes

Building the static portion of the website will require lots of typing but not much thinking.
Building the interactivity of the website will require lots of thinking and not much typing.  

## Thinking In React Q and A

What is the single responsibility principle and how does it apply to components?

> A component should (ideally) do only one thing (and do it well).

What does it mean to build a ‘static’ version of your application?

> Build a rendering website that shows the components but has no interactivity and no data (state) changes.  

Once you have a static application, what do you need to add?

> Determine the absolute minimum representation of state that will enable all necessary computations, on-demand.

What are the three questions you can ask to determine if something is state?

> Is it passed-in from parent via props? Not state.  
> Does it remain static over time? Not state.  
> Can value be computed based on other state or props? Not state.  

How can you identify where state needs to live?

> Find the most common component that renders something based on that state.  
> If difficult to find a single owner, then use a parent component to hold the state.  

## Higher Order Functions

[Higher Order Functions](https://eloquentjavascript.net/05_higher_order.html#h_xxCc98lOBK)  

What is a “higher-order function”?

> Functions that operate on other functions by taking the function as an argument or returning a function.  

Explore the greaterThan function as defined in the reading. In your own words, what is line 2 of this function doing?

> The line `greaterThan10(11)` calls the stored function `greaterThan(10)` and also supplies a parameter of `11`.  
> When `greaterThan(10)` executes it evaluates `m > n` which returns a boolean.  
> In this case, effectively `let m = 11` and `let n=10`.  

Explain how either map or reduce operates, with regards to higher-order functions.

> Map uses what boils down to a for-loop 'under the hood', but instead of having a completed execution block, the execution block 'calls' the function that the developer passes in.
> For example: `myArr.map(x => x + 2)` passes-in the function expression `x => x + 2` to the for-loop body (see below).  

```javascript
const newArr = myArr.map(x => x + 2);
// the expression is called something like the following
for (let i=0; i<myArr.length; i++) {
  let currentItem = myArr[i];
  newArr.push(userExpression(return currentItem));
}
// Note: this is pseudocode that looks a whole lot like javascript
```

## Footer

Go back to [Readme.md](../README.html)  
