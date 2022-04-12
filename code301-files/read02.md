# Read01 Assignment - Intro to React and Components

Read and take notes from the following resources:  

## React Lifecycle Events

Source: Joshua Blankenship on [Medium.com](https://medium.com/@joshuablankenshipnola/react-component-lifecycle-events-cb77e670a093)  

### What Are React Lifecycle Events

When you define components as classes or functions, the methods used are called 'lifecycle events'.  
Methods can only be called on components during their 'lifecycle'.  

### Three Phases of Liceycle

Mounting: Creating a component instance and adding it to the DOM. Various built-in and required methods are executed automatically at this phase (lifecycle events).  

Updating: State changes cause re-rendering, aka Updating. Various built-in and required methods are executed at this phase (lifecycle events).  

Unmounting: Removing a Component from the DOM. Method 'componentWillUnmount()' is called (the last lifecycle event).  

### Notes

Avoid usint `this.setState()` in a constructor: It is unnecessary and could produce unexpected side effects. *However* it can be called within componentDidMount() to force a re-render event.  
There are *unsafe lifecycle events* that should be avoided. Review the medium.com article (linked above) for details on these.  

### Q and A

Based off the diagram, what happens first, the 'render' or the 'componentDidMount' lifecycle event?
> render. componentDidMount is called during the last phase, the 'mounting' phanse and 'commit' sub-phase.  

What is the very first thing to happen in the lifecycle of React?
> constructor is called (in the 'mounting' phase and 'render' sub-phase).  

These things happen in this order:  

1. constructor  
2. render
3. componentDidMount  
4. componentWillUnmount
5. ReactUpdates

What does componentDidMount do?
> It is a place to load network requests or make DOM initialization calls. It is a good place to subscribe to (events?) and make API calls.  

## Props and State YouTube Video Notes

What types of things can you pass in the props?  
> Props are a lot like arguments to a function.  
> Values to initialize a component's state, or data that the component can render.  

What is the big difference between props and state?  
> Props are passed between components, and must be updated OUTSIDE of the component.  
> State is data within the component, and can be updated WITHIN the component.  

When do we re-render our application?  
> When the component *state* changes.  

What are some examples of things that we could store in state?  
> Values that change, and the change should be rendered to the UI.  
> User-updated values, like from a Form, where the UI might need to update based on the state change.  




## Footer

Go back to [Readme.md](../README.html)  
