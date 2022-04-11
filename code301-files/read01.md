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

### Tips and Tactics

- To ensure an onClick or other event are called only when the event occurs (instead of when rendering), use an Arrow Function as the onClick() parameter.  

## Footer

Go back to [Readme.md](../README.html)  
