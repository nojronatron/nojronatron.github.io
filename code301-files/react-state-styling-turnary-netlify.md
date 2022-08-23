# Class Notes

## Morning Code Challenge

Question had to do with using CSS float.  
Resolution was to work around the float setting because float *take containers out of their normal flow*.  

## Code Challenge Review

Challenge #4 was reviewed. Key takeaways:  

- The parameter name 'callback' is arbitrary.  
- Parameter 'callback' is really a method that the method will call.  
- Calling a method like `methodName()` causes the method to execute.  
- Assigning a method to a variable or parameter like `someMethod(someOtherMethod)` actually stores the method as a variable instance within the scope of the calling method.  

## Code Review Lab01

To be able to finish the stretch goal, use Array.map().  
*Recommend*: Make diagrams for yourself as you start-in on projects to visualize the components and the data flow.  
Always use braces to surround variable representations e.g. props.  
When passing something that needs to be interpreted dynamically, surround the item with braces.  

```javascript
//  code snippet
render() {
  return (
    <>
      <Header title={234} />
    </>
  )
}
```

Functions can only return a single item.  
To return multiple items use `<div>` or better yet 'frags' `<>{...}</>` to encapsulate the return into a 'single item'.  
When using CSS with React, define `className=""` instead of `id=""` and `class=""`.  
*Props*: Data that got passed down from one component to another.  

## Review Maybe

Three *required*  codelines for a React component:  

1. `import React from 'react';`  
2. `class ComponentName extends React.Componet {}`  
3. `export default ComponentName;`  

Additional code is required, within the Component definition itself:  

- A `render()` method that will `return()` a single thing.  

## Lab02 Preview

### Goals

- Render unique horned beasts.
- Allow users to vote for their favorite horned beast.  
- Make website visually appealing using Bootstrap.  
- Stretch: Add interaction e.g. change style upon click.  
- *No Buttons Allowed*  

#### Render Unique Horned Beasts

Use `src={this.props.imgURL}` within the `<img>` tag.  
Do this for the alt (property) too.
Import the data from data.json: `import data from './data.json';`  
Create a temporary array to push results to.  
Set up an `Array.forEach()` and use an arrow function to act upon each item in the array.  
Inside the `push()` method add the call to the Component, setting the props.  

##### Unique Key Prop Warning

This is because you need to pass a key to each individual component you create from a collection.

```javascript
let tempArr =[];
myArray.forEach((arrItem, key) => {
  tempArr.push(
    <MyComponent
      myAttribute={arrItem.title}
      IdxAttribute={arrItem.key} />  //  this is suspect
  );
})
key={idx};  // also suspect
```

### State and Changing Data

State: Represents data that can change.  
State can be held in variables, via Forms, eventHandlers, etc.  
If data can change, Event Handlers are necessary.  
Props: Components cannot change data from props; this data comes from the parent Component.  
State: Components *can* change data from state, and data is stored *in* the component.  
Capture and use State by defining a Constructor.  

#### Constructors

Within the component definition, add `constructor(props) { super(props) }`  
*Quote*: "send in props, declare the super, then assign the value to state."  

#### Event Handling

This is the HTML in-line style i.e. `<div onClick={this.eventHandlerMethod}>Click me</p>`  
An event handler method should be created after the constructor statement and property statement(s), and should use an arrow function:  

```javascript
handleEvent = () => (
  this.isEventRaised = true;
)
```

#### Set State

In order to create a new state, use `this.setState()` inside an event handler.  
*Note*: Using the shorthand incrementor '++' will not work, instead use `varItem = varItem + {incrementValue}`  
For this assignment, state will store the number of times an item has been clicked.  

#### Separation of Concerns

JS, CSS, and HTML are constrained to their specific capabilities.  
React Components cross-over these areas, allowing application of CSS (for example) to each component instance on render.  
To edit rendering of many components, apply CSS to the parent.  
Remember to create *separate css files for each component* rather than try to apply css from one file to everything.  

### React Bootstrap

[React-bootstrap](react-bootstrap.github.io)  
Installation command e.g. for React-Bootstrap v.5.1: `npm install react-bootstrap bootstrap@5.1.3`  
*Note*: Be *very careful* about which version you are using due to history of instroduction of breaking changes.  

#### Stylesheets

Import the min.css file to whichever file makes sense. Sheyna suggested 'index.js'. This enables using Bootstrap in "most places".  

#### Importing Components

Example: `import Button from 'react-bootstrap/Button'`  

#### Applying Bootstrap Style

React components, because they are meant for reuse, applying ID's is a bad idea.  
Apply attribute assignment using 'className=""' to be sure styles will apply.  
`<Button className="article-button">Button</Button>`  
Using 'variant': `<Button className='article-button' variant="success">Button</Button>` applies the React-Bootstrap class 'variant' with the preconfigured setting selector 'success'.  
When someone clicks, add an onEvent type and an event handler:  

```javascript
handleEvent = () => {
  this.setState({
    propertyName: newValue;
  })
}
return (
<button onClick={this.handleEvent}>Button</button>
)
```

#### Turnary Operator

Design:  

1. Statement that evaluates to true or false.  
2. A question mark.  
3. Code statement that will be run when evaluation returns true.  
4. A colon.  
5. Code statement that will be run when evaluation returns false.  

Shorthand: "W:T:F"  

Add any javascript statement within a React return() body by enclosing it within braces.  

```javascript
// middle of return block here
/>
<div>{this.state.needsHelp ? 'I need help' : ''}</div>
<Button
```

## Site Deployment

Netlify will break your site if you try to Merge to Main prior to the tests completing.  
When tests fail, CHECK THE LOGS, and locate the error, and follow the advice in the logs to fix the problem(s), one by one, top to bottom.  
Of course, ACP after each fix-and-save, then wait for tests to re-run.  

## Code Challenge Class02

Use the Array.prototype.map() method.  
Review MDN for details.  
Similar to .forEach() except it creates a *new array* populated with the results from the prototype function.  

```javascript
const myMap = myArr.map(x => x * 2);
```

