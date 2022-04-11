# Read01 Assignment - Intro to React and Components

Read and take notes from the following resources:  

- Component Based Architecture [Article](https://www.tutorialspoint.com/software_architecture_design/component_based_architecture.htm)  
- What are props and how to use it [Article](https://itnext.io/what-is-props-and-how-to-use-it-in-react-da307f500da0#:~:text=%E2%80%9CProps%E2%80%9D%20is%20a%20special%20keyword,way%20from%20parent%20to%20child)  
- React Tutorial through Passing Data Through [Props](https://reactjs.org/tutorial/tutorial.html)  
- React Docs [Hello World](https://reactjs.org/docs/hello-world.html)  
- React Docs [Introducing JSX](https://reactjs.org/docs/introducing-jsx.html)  
- React Docs [Rendering Elements](https://reactjs.org/docs/rendering-elements.html)  
- React Docs [Components and Props](https://reactjs.org/docs/components-and-props.html)  

## Component Based Architecture

See [components-react.md](./components-react.html).  

## Props and How To Use Them

See [components-react.md](./components-react.md).  

## React Tutotial Passing Data Through Props

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

### Tips and Tactics

- To ensure an onClick or other event are called only when the event occurs (instead of when rendering), use an Arrow Function as the onClick() parameter.  
- Install ReactDevTools to add the ability to inspect React Components and to Profile the React application.  
- Avoid modifying an existing array, instead call 'Array.slice()' to create a copy of the array and then use the values as necessary.  

## Footer

Go back to [Readme.md](../README.html)  
