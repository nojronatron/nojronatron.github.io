# Dive Into React

## High Level Overview of React Notes

### Table of Contents

- High Level [Points](#high-level-points)
- The [UI](#the-ui)
- React [Objects](#react-creates-objects)
- React is a [Library](#react-is-a-library)
- Component [Architecture](#component-architecture)
- [Data Flow](#component-trees-and-data-flow)
- Component Level [State](#component-level-state)
- [Quiz](#quiz)
- Information Source: Zac Gordon on [YouTube](https://www.youtube.com/watch?v=FRjlF74_EZk&ab_channel=ZacGordon)
- Setting up a blank [React Site](#blank-react-site-setup)

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

## Blank React Site Setup

ReactJS.org [Create New React App](https://reactjs.org/docs/create-a-new-react-app.html)

- Single-page webapp setup: Use NPX and NPM (see next subsection).
- Server-rendered App: [NextJS Official Guide](https://nextjs.org/learn/foundations/about-nextjs).
- Static React Website with React Components: [GatsbyJS Official Documentation](https://www.gatsbyjs.com/docs/).
- Other Toolchains: Neutrino, Nx, Parcel, or Razzle.

### Single-page Webapp Setup

Requirements:

- Node version 14.0.0 or newer.
- NPM version 5.6 or newer.

Do:

1. Execute: `npx create-react-app {dir}`
1. CD to 'dir'.
1. Recommended: `npm install` to ensure packages are up to date.
1. Execute: `npm start` and your single-page webapp will start!

To run in Production Mode: `npm run build` from the project root directory.

Note: There could be reason to execute `npm audit fix --force` to update some packages. This is up to you to figure out.

### Shortcuts

Key-combo => Code-generated

rfc => react function component
rcc => react class component

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

## Footer

Return to [README.md](../README.html)  
