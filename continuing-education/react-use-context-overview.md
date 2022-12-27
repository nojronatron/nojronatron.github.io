# React UseContext

## Overview

Props:

- Provider: Wrap all code that needs the information in the Context
- Value: Whatever the value of the Context as you define it.

Context:

- A function that can be referenced everywhere else within a React App.
- A global state that allows passing Props easily to all children of the Provider.

## Context API

When passing props to deeply nested components, props can become more difficult to manage, passing props through many children to the place the data needs to go in the hierarchy.

Context API allows specifying pieces of data available to all components without having to pass data through each component.

React.createContext:

- Provider variable: Provides a value to all components nested inside of it.
- Consumer variable: Expects a function as that provides a value with Context as the only argument. JSX can be returned based on that argument.

In React Class Components, Context components must wrap the child components and the function variable must be passed-in (and out) of the Context Provider and Consumer, respectively.

In React Function Components, `useContext` hook allows bypassing the Component wrapping, which simplifies code.

## UseContext Hook

Pass your custom Context to 'useContext' hook:

- First: `const { theme, setTheme } = useContext(ThemeContext);`
- Later: `<p>{theme}</p>` and `...onClick={()=>setTheme('light')}...`

This bypasses having to wrap Components in Consumer and Provider elements.

## Notes

- Import useContext from react.
- Pass-in the custom context to the useContext react hook.
- Use Functional Programming to export a function leveraging useContext(yourImportedContext) and returns an element. This avoids the render-based Element Wrapping [see Reactjs documentation](https://reactjs.org/docs/legacy-context.html#referencing-context-in-stateless-function-components).
- Consider `useContext` as an interface for consuming context.

## Reference

Examples were borrowed from videos and the [WDS Blog](https://blog.webdevsimplified.com/2020-06/use-context/).

[WebDev Simplified - useContext in 13 Minutes](https://www.youtube.com/watch?v=PKwu15ldZ7k&ab_channel=WebDevSimplified).
