# Dive Into React

## High Level Overview of React Notes

Information Source: Zac Gordon on [YouTube](https://www.youtube.com/watch?v=FRjlF74_EZk&ab_channel=ZacGordon)  

### High Level Points

It is a UI Library. Create user interfaces for websites, etc.  
Has a component architcture.  
One-way data flow paradigm - not like usual two-way binding.  
Component State tracking (related to data flow).  

### The UI

Agnostic: No concern for *where* the UI will display.  
React doesn't worry about where final compeonts are sent.  
Used with a second library e.g. React DOM, etc.  
Modify according to where results are to be display.  

### React Creates Objects

React creates React JS Objects.  
Until React Objects are passed to a DOM, the React JS Objects are *not* DOM elements, but will 'become DOM elements'.  

### React is a Library

An *interface library*, specifically.  
Lightweight. Not as 'robust or big as Angular'.  
Use to design agnostic UIs, widgets (e.g. a search bar) and other webapp UI components.  

### Component Architecture

Typical high-level main component will be fairly short, and recognizable.  
Use export functions rather than object to put together the DOM HTML within a React component.  
Composing React Apps is done by breaking-up webapp components into React components that represent the DOM section(s) that compose the website UI.  

### Component Trees and Data Flow

Recall the DOM Tree.  
React Component Tree can follow a similar mode.  
*But* data flows *one way down the app*.  
Data in ReactApp will flow from the root down to through the branches.  
Data flow can be passed as parameters ("props") via functions.
Child branches can call a function in Root in order to update the data.

#### Component Level State

Passing data requires component (or tree branch) nesting.  
Data flow only passes *down* from a component to its children.  

## Quiz

Q. What is React?  
A. React is a Component Library used to create user interfaces like websites.  

Q. What is a component?  
A. Components are small segments of code that perform specific tasks. In React, its components represent portions of a DOM Tree i.e. a Header element, or other semantic elements like Section, or Main.  

Q. What is the dataflow of React?  
A. Data flows from a parent component to any nested child components, i.e. from a root to its branches.  

Q. How do we make a React element a DOM element?  
A. When React elements are passed through "React DOM" they are transformed into DOM elements.  

Q. React is a user interface _____?  
A. Library.  

Q. Which direction does data flow in React?  
A. One way: Data flows down from the parent to the nested children.  

Q. Every component manages its own _____?  
A. State, i.e. data in the component.  
