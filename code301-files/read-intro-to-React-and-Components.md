# Read01 Assignment - Intro to React and Components

Read and take notes from the following resources:  

[X] Component Based Architecture [Article](https://www.tutorialspoint.com/software_architecture_design/component_based_architecture.htm)  
[X] What are props and how to use it [Article](https://itnext.io/what-is-props-and-how-to-use-it-in-react-da307f500da0#:~:text=%E2%80%9CProps%E2%80%9D%20is%20a%20special%20keyword,way%20from%20parent%20to%20child)  
[X] React Tutorial through Passing Data Through [Props](https://reactjs.org/tutorial/tutorial.html)  
[X] React Docs [Hello World](https://reactjs.org/docs/hello-world.html)  
[X] React Docs [Introducing JSX](https://reactjs.org/docs/introducing-jsx.html)  
[X] React Docs [Rendering Elements](https://reactjs.org/docs/rendering-elements.html)  
[X] React Docs [Components and Props](https://reactjs.org/docs/components-and-props.html)  

## Component Based Architecture

See [components-react.md](./components-react.html).  

## Props and How To Use Them

See [components-react.md](./read-state-and-props.html).  

## React Tutorial Passing Data Through Props

[Demo starter code](https://codepen.io/gaearon/pen/oWWQNa?editors=0010)  

### What Is React?

Javascript library for building user interfaces.  
Allows composition of UIs from 'components'.  
React Elements are actually javascript objects that can be passed-around as parameters.  

### What Are Props?

Props is short for 'properties' and represents parameter-passing in React.  
Props are passed to child components using syntax that is similar to *html5 attributes*.  

### What Does React Do?

Efficiently re-renders components without a screen refresh.  
Utilizes Props as parameters to move data around.  

### What Is JSX?

Special React syntax that makes writing React Elements easy.  
JSX syntax can collapse a hierarchy of HTML tags down to a few lines of React statements.  
Any javascript expressions can be put within JSX brackets.  

### State

Capturing and using data represents a components state.  
Components hold their 'state' by setting `this.state`.  
Use a Constructor to initialize 'this.state'.

```javascript
class Example extends React.Component {
    constructor(props) {
        super(props);
        this.state = {
            value: null,
        };
    }
    //  other class properties and functions here
}
```

### Super

Call 'super' whenever defining a constructor of a subclass.  
For React components with a Constructor *always* start with a `super(props)` call.  

### Children Can Share Data

In order to share data between two sibling components, configure the Parent component to pass the state back down to both children by using props.  
Another way to think about this is 'keep child components in sync'.  
This is referred to as 'lifing state' into a parent component.  

### Controlled Components

Components that do not maintain their own state, but rather acquire it from their parent Component are called 'Controlled Components'.  

### Immutability

Changing data directly in an existing or passed-in variable is not always wise (or possible).  
Replacing the data using a new variable is preferred for the following reasons:  

- Detecting changes: Replacing an entire immutable object is easy because the *reference* can be tested, rather than testing every value within a tree.  
- When a change has been detected, rendering can be done right away. The longer it takes to detect the change, the longer it takes for rendering to happen, which can become a bad user experience.  

### Functional Components

Simple way to write components that do one thing: *render*.  
Do not hold or manage any state.  
Simply takes props input that should be rendered and renders it.  
If a component is built-out as a class, but only has one job, consider refactoring it to be a function instead. Remember to:

- Remove references to 'this' since the Class scope will no longer exist.  
- Verify no other state information is necessary other than the props to be rendered.  

### React and Keys

React reserves a property called 'key' for use in rendering.  

"When a list is re-rendered, React takes each list item's key and searches the previous list's items for a matching key. If the current list has a key that didn't exist before, React creates a component. If the current list is missing a key that existsed in teh previous list, React destroys the previous component. If two keys match, the corresponding component is moved." *[reactjs.org/tutorial/tutorial.html, section 'picking a key']*

Assign keys whenever building a dynamic list.  
Without a key, React throws a warning and uses the index as the key by default.  
Do *not* use `key={i}` (it will silence the warning but does not properly resolve the problem of missing, valid keys).  

```html
// a key can be as simple as a React prop
<li key={move}>
    <button></button>
</li>
```

## React Docs Hello World

React [Hello World](https://reactjs.org/docs/hello-world.html)  

### Simplest React Component

In an HTML document with only a div with id of 'root'...  
Add a ReactDOM.render method in javascript that inserts a header and makes a DOM call by element ID 'root'.  

### JSX

JSX is syntax that is basically a combination of initializing a javascript variable and assigning html elements to it.  
Use JSX with React when defining the UI.  
The result is a React "element".  
React 'separates concerns' by using components that contain both markup and logic, together.  
JSX has the benefit of allowing React to produce better error and warning messages.  

#### JS Expressions

Any valid JS expression can be contained with curly braces in JSX.  
JSX will also capture the result of calling a javascript function!  
When writing multi-line JSX expressions, enclose then within parenthesis and add a semi-colon after the closing paren.  
JSX *is an expression*, becoming regular javascript function calls.  
Use JSX inside of *if* statements and *for* loops.  

#### Attributes

Use quotations to specify string literals as attributes.  
Use braces to embed js expression in an attribute.  
JSX is closer to JS than HTML so use *camelCase* to name properties.  

*Note*: Do NOT use both quotations AND braces in JSX expressions in the same attribute.  

#### Specifying Children with JSX

Empty tags can be closed immediately like XML: `<img src={} />;`  
JSX can contain child tags:  

```javascript
const element = (
  <div>
    <h1>Title</h1>
    <p>Lorem ipsum...</p>
  </div>
);
```

#### JSX Prevents XSS Attacks

React DOM escapes embedded JSX values before rendering the compoennt.  
Components are stringified before rendering to help prevent executable code injections.  

#### JSX is a New React Element

`const element = (...);`

is equivalent to

`const element = React.createElement(...);`

React.createElement organizes the parameters you enter, into a new Class object with properties as assigned.  

## Rendering Elements

Elements describe what will be seen on-screen.

### Into The DOM

Apps built with React typically have a single root DOM node.  
Many, isolated Root DOM Nodes can exist in more complex applications.  

To render a React element pass the DOM element to createRoot method then pass the React element to the render method:  

```javascript
const element = <h1>Hello, world</h1>;
const root = ReactDOM.createRoot(
  document.getElementById('root')
);
root.render(element);
/* example taken from reactjs.org/docs/rendering-elements-html */
```

### Updating Rendered Elements

React elements:

- cannot be changed once created (Immutability).  
- Represent a portion of the UI at a single point in time.  
- Can be stateful components, to avoid calling root.render() over and over again.  

### Only Updates What Is Necessary

React DOM compares an element (and its children) and applies only updates needed to bring DOM up-to-date with the current React DOM representation.  
Duplicate tree nodes that haven't changes *are not rendered again*.  

## React Components

[React Components](https://reactjs.org/docs/react-component.html)  

### Overview

- React allows defining: Classes, Functions, and Components.  
- Extending React.Component creates a 'Component Class'.  
- *Must* define 'render()' in a react.Component subclass, all others are *optional*.  
- In React, code resuse is achieved through composition (instead of inheritance).  

Example of a simple, valid React Functional Component:

```javascript
function HelloWorld(props) {
  <h1>Hello World! Props are {props.name}</h1>;
}
```

Example of a React Class Component, build using ES6 Class:

```javascript
class HelloWorld extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}!</h1>;
  }
}
```

### Component Composition

Components can refer to other Components in their output.

The same Component can be used in a dialog, button, screen, or form.

Components can be split into smaller Components.

Name Components from 'their own point of view rather than the context in which it is being used' *[ReactJS.org, Components and Props]*.

### Rules

Always name Components with a starting capitalized letter.

DOM Tags start with a lower-case letter.

Props are *read only* so your Component can NOT edit them.

### Component Lifecycle

Lifecycle methods are included in many React components.

*Note*: They can be overridden.  

React Lifecycle Methods [Diagram](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)  

#### Mounting

Called in order when a component is inserted into the DOM:

1. constructor()
2. static getDerivedStateFromProps()
3. render()
4. componentDidMount()

#### Updating

These are called when a component is being re-rendered:  

1. static getDerivedStateFromProps()
2. shouldComponentUpdate()
3. render()
4. getSnapshotBeforeUpdate()
5. componentDidUpdate()

#### Unmounting

Called when a React component is removed from the DOM:  

- componentWillUnmount()  

#### Error Handling

Called when there is an error in rendering (or lifecycle method or constructor of a child component):

- static getDerivedStateFromError()  
- componentDidCatch()  

### Tips and Tactics

- React Elements are first-class javascript objects so they can be passed around as parameters.  
- To ensure an onClick or other event are called only when the event occurs (instead of when rendering), use an Arrow Function as the onClick() parameter.  
- Install ReactDevTools to add the ability to inspect React Components and to Profile the React application.  
- Avoid modifying an existing array, instead call 'Array.slice()' to create a copy of the array and then use the values as necessary.
- Even better than `Array.slice()` is to use the spread operator `[...]` to expand an array into a new variable and work with that. Once done, copy the new array into the original input array or just return the copied-and-edited-array to the calling function.

### Array Map

Consider Array.Map() to be equivalent to:  

```javascript
let myArr = [1, 2, 3];
for(let i=0; i < myArr.length; i++) {
  //  yield myArr[i];
};
```

Apply the following logic to define the Map function operation:  

- Use an Arrow Function to define an expression.  
- Arrow Function parameter is the currently selected item in the array.  
- Arrow Function performs expression using input parameter.  
- Map function captures each result into a new Array and returns it.  

```javascript
let myArr = [1, 2, 3];
console.log(myArr.map((i) => i * 2));
//  output: [2, 4, 6]
```

### Additional React References

React [Hello World](https://reactjs.org/docs/hello-world.html)  
React [Components](https://reactjs.org/docs/react-component.html)  

## Footer

Go back to [Readme.md](../README.html)  
