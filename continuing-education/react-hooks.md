# React Hooks

Review React Hooks to learn what they are, and how and when to use them.

Provide links to additional references as well as code snippets where possible.

## Table of Contents

- [Overview](#overview)
- [Migrating From Class to Function Components](#migrating-from-class-to-function-components)
- [UseState](#usestate)
- [Context](#context)
- [UseEffect and Side Effects](#useeffect-and-side-effects)
- [Custom Hooks](#custom-hooks)
- [Moving to Hooks](#moving-to-hooks)
- [useRef](#useref)
- [Support](#support)
- [Developing with Hooks Going Forward](#developing-with-hooks-going-forward)
- [References](#references)
- [Footer](#footer)

## Overview

Hooks are new in v.16.8 and provide Functional Components similar capabilities to what React Class Components are borne with.

- Hooks allow using React Features without writing a fully-blown class component.
- Sharing stateful logic is difficult and often requires wrapping Components with other Components in order to get desired results.
- Refactoring a working component to implement a wrapper causes code churn that React Hooks can help to avoid.
- Enable "reuse [of] stateful logic without changing your component hierarchy." *[Reactjs.org API Documentation]*
- Components can become complex especially when imported into React Lifecycle Methods, which makes code harder to understand, maintain, and is more likely to contain bugs.
- Classes don't minify well, are more difficult to write and understand.
- Hooks allow using features without new Class components.
- Sticking with functional components simplifies minification and keep React efficient.
- Hooks were built with functional components in mind, allowing use of React features without having to build a Class to do so.
- Hooks can be adopted into existing code with minimal rewriting.
- ReactJS intends to favor Hooks over class components going forward.

Hooks features include:

- State
- Lifecycle
- Context
- Refs

Other Hooks benefits:

- Hooks can help reduce nesting in a React Tree.
- Hooks allow accessing State from within a Functional Component.
- Hooks can be reused within a Component.

Components should just be Functions, and Hooks are simply function calls. Therefore, "custom Hooks" can be created for your specific needs.

*Important!*: Do NOT call a Hook inside of a conditional. They must be called at the top of the Component.

Hooks as proposed by ReactJS: *[React Conf 2018 Presentation]*

- Use all React features without a class.
- Reuse stateful logic between components.
- Opt-in and 100% backward compatible.

## Migrating From Class to Function Components

This is necessary in order to use React Hooks (or create your own). Follow these general steps to get going rapidly:

1. Change the Component signature from `export default class MyFunction extends React.Component...` to `export default function MyFunction()`
2. If the class received props from a parent Component update the signature to be `export default function MyFunction({prop, ...})` to include the actual parameters passed-in by the parent.
3. Any `this.props` statements need to be renamed. Functional Components do *not* support `this` so these props need to be renamed and set in step 2.
4. Remove the `render(){}` code blocks. All `render` code is now just code-block within the Function.
5. If enforcing PropTypes, include the definition *just after the last Functional Component closing brace*: `MyFunction.propTypes = { propa: PropType.object, ... };`
6. If the Component was updating `state`, then import `useState` and refactor the `setState()` function calls to use the appropriate `setN` array item instead.
7. Remove the `{ Component }` import statement, it is no longer needed.

## UseState

Import: `import React, { useState } from 'react';`

Leverage the Hook:

```javascript
export default function MyFunction(props) {
  const [name, setName] = useState('MyName');
  // declares a State with properties 'name' and 'setName'
  // initializes 'name' with a value 'MyName' to start
}
```

Reference an event handler:

```javascript
export default function MyFunction(props) {
  const [name, setName] = useState('MyName');
  
  function handleNameChange(event) {
    setName(event.target.value);
  }
  // no longer necessary to bind the event handler
  // to a class in order to get access to it
}
```

## Context

Reading Context.

Like global variables for a subtree.

Allows reading current user language or visual theme.

Import: `import { ThemeContext } from './context';`

Enables using: `<ThemeContext.Consumer>` component.

Example implementing a theme from a CSS file:

```javascript
import { ThemeContext } from './context';

// inside of a class component...

  return (
    <ThemeContext.Consumer>
      {theme => (
        // theme is just a css class
        <section classname={theme}>
          // more jsx here
        </section>
      )}
    </ThemeContext.Consumer>
  );
}
```

Similarly, `<LocaleContext.Consumer>` enables setting end-user language.

UseContext Hook simplifies this somewhat.

```javascript
import React, { useContext } from 'react';
import { ThemeContext } from './context';

export default function MyFunction(props) {
  const theme = useContext(ThemeContext);
  // this reads context AND SUBSCRIBES to changes!

  // more code
  return {
    <section className={theme}>
      // more jsx here
    </section>
  }
}
```

## UseEffect and Side Effects

Import: `import React, { useEffect } from 'react';`

Declare the effect inside the component definition to allow access to State/useState.

UseEffect to display a variable to the active browser tab aka 'document title':

```javascript
import React, { useEffect } from 'react';

export default function MyFuction(props) {
  const [name, setName] = useState('Alpha');
  
  useEffect(()=>{
    document.title = myNewTitle;
  });

  function handleNameChange(e) {
    setName(e.target.value);
  }
}
```

Multple useEffects statements can be made for unrelated data properties.

Any effect can optionally return a function. Call the function using an arrow function to encapsulate functions like `window.removeEventListener(name, callback)`.

This of useEffect as 'componentDidMount', 'componentDidUpdate' among other lifecycle events.

## Custom Hooks

1. Develop a function as you normally would: `function useFuncname(){ ... return result }`
2. Add a new const variable to store the output in the calling function: `const customResult = useFuncname();`

Convention:

- Call the function a custom hook by prefixing 'use'.
- Assume the 'use' prefixed function is going to maintain some sort of State.

Custom Hooks are javascript functions:

- Can take zero to many arguments.
- Can return one or zero types.

Create your own abstractions without adding to "wrapper hell".

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

React Conf 2017 [video on YouTube](https://www.youtube.com/watch?v=dpw9EHDh2bM)

## Footer

Return to [continuing education index](./conted-index.html)
