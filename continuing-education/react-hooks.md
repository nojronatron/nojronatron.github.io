# React Hooks

Review React Hooks to learn what they are, and how and when to use them.

Provide links to additional references as well as code snippets where possible.

## Overview

Hooks are new in v.16.8. Most recent project I am generally working with v.18+.

Use React Features without writing a fully-blown class component.

Sharing stateful logic is difficult and often requires wrapping Components with other Components in order to get desired results.

Refactoring a working component to implement a wrapper causes code churn that React Hooks can help to avoid.

Enable "reuse [of] stateful logic without changing your component hierarchy." *[Reactjs.org API Documentation]*

Components can become complex especially when imported into React Lifecycle Methods, which makes code harder to understand, maintain, and is more likely to contain bugs.

Classes don't minify well, are more difficult to write and understand. Hooks allow using features without new Class components. Sticking with functional components simplifies minification and keep React efficient. Hooks were built with functional components in mind, allowing use of React features without having to build a Class to do so.

Hooks can be adopted into existing code with minimal rewriting.

ReactJS intends to favor Hooks over class components going forward.

Hooks features include:

- State
- Lifecycle
- Context
- Refs

Hooks can help reduce nesting in a React Tree.

## Moving to Hooks

- Constructor: Not needed in Functional Components. Use 'useState' call instead, or pass a function to `useState()`.
- `render()`: Functional component body.
- `useEffect()`: Can express 'componentDidMount', 'componentDidUpdate', and 'componentWillunmount' lifecycles, in any combination.

There are more in the [faq: From Classes to Hooks](https://reactjs.org/docs/hooks-faq.html#how-do-lifecycle-methods-correspond-to-hooks)

## useRef

Enables:

- DOM references.
- Referencing mutable, generic container references such as a class instance property.

Do/Nots:

- Do NOT set ref during rendering.
- DO modify ref in event handlers.
- DO modify ref in effects.

## Support

React 16.8+

React Native 0.59+

Unittesting: Treat like a Functional Component. Check out these [testing recipes](https://reactjs.org/docs/testing-recipes.html)

Linting:

- Mostly supported (some false-positives likely).
- Any function starting with 'use' followed by a capitalized alpha-character 'is a Hook'.
- Calls to HOoks are in a PascalCase function.
- Hooks are called in same order upon every render.

## Developing with Hooks Going Forward

Recommend developing Functional Components with Hooks, instead of Class Components going foward.

Functional w/ Hooks is fully compatible with Classes in the same React Tree.

## References

Reactjs.org [Hooks at a Glance](https://reactjs.org/docs/hooks-overview.html)

Reactjs.org [Hooks API Reference](https://reactjs.org/docs/hooks-reference.html)

## Footer

Return to [continuing education index](./conted-index.html)
