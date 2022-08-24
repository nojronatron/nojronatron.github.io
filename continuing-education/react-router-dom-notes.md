# React Router Dom Study Notes

There are two versions of React Router:

- React Router Dom
- React Router Native

These notes will be focused on React-Router-Dom, for webapp usage.

## Install and Import

1. Install: `npm i react-router-dom`
1. Import into index.js: `import {BrowserRouter} from 'react-router-dom';`
1. Wrap the entire App in BrowserRouter, within index.js (see example below).

```javascript
// import statements and root definition...
root.render(
  <React.StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </React.StrictMode>
)
```

## Set Up Routes

1. Go into App.js.
1. Include the `<Routes>` component and the `<Route>` component.
1. Add the actual path to each 'Route' tag and define the target compoennts within the 'element' attribute.

```javascript
// header imports etc...
function App() {
  return (
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="/about" element={<AboutUs />} />
    </Routes>
  )
}
```

## Add Navigation

Use a `<Link>` component.

Technically an Anchor Tag under the hood.

Instead of using 'href' use `to="/"`.

This allows changing Components on a click from a Header-based NavBar, for example.

```javascript
// imports etc
function App() {
  return (
    <>
      <nav>
        <ul>
          <li>
            <Link to="/">Home</Link>
          </li>
          <li>
            <Link to="/about">About</Link>
          </li>
        </ul>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<AboutUs />} />
      </Routes>
    </>
  )
}
```

Define routes inside the Routes component.

## Router Types

### Browser Router

`import { BrowserRouter } from 'react-router-dom'`

Most commonly used.

What will be discussed in these notes.

### The Hash Router

`import { HashRouter } from 'react-router-dom'`

Instead of storing a URL as a normal URL, it stores a hashed-version of a URL.

A URL that includes a `#` hash character is not really a route, but Hash Router allows and manages it properly.

Not recommended by Kyle *[of WebDevSimplified]*, but it exists.

### The History Router

`import { unstable_HistoryRouter } from 'react-router-dom'`

Enables using Back and Forward routing buttons to navigate the webapp.

Most of the time this is not necessary *and* it is unstable (currently Aug 2022 version).

### Memory Router

`import { MemoryRouter } from 'react-router-dom'`

Stores everything related to browser clicks in memory.

Does NOT change the URL in the browser.

Useful for testing where a browser is not included in the testing system.

### Static Router

`import {StaticRouter} react-router-dom/server`

Specify a location attribute to each `<StaticRouter location=''>` Component.

Tells the server to render the specific page.

Only use this when doing server-side rendering in React, ensuring the correct page is rendered.

### Native Router

`import { NativeRouter } from 'react-router-dom'`

Must install 'React Native Router' library.

## Using Browser Router

### Render individual items by ID

`path="/items/:id"`

Use a custom hook 'useParams()' which returns custom object parameters.

'useParams()' is helpful to pull an ID param from a collection of items, which can then be referenced by the Router directly.

### Hardcoded Route ID

1. Create a component that enables creating a new item.
1. Update the Link element to point to the hard-coded route e.g. `<Route path="/items/new" element={<NewItem />} />`

### Using both ID and Hardcoded Path

The hardcoded path will be selected over the `:id` version of the path by default.

If two routes match, then the hardcoded one will be selected by Router, because it is *more specific*.

This eliminates worry about the order of routing (at least in version 6 - previous versions still must be ordered correctly, top to bottom).

### Redirect to 404 Page

1. Create a route to the star symbol `*`
1. Assign an element pointing to a `<NotFound >` Component (page).

```javascript
// ...inside the <Routes></Routes> tags within the return statement...
<Route path="*" element={<NotFound404 />} />
```

Make sure this is last in the list.

### Route Nesting

Related paths should be nested.

Parent path Route needs to be defined, without any element.

Nest child Route tags and specify the element in each one e.g. `...path=':id' element={<PageComponent />} />`

Assign an 'index' route to tell Router to use the Parent route as the "Index" page for each child route.

A Parent Route *can* have an element that points to a Layout as defined in a Component, which will force Router to allow the targeted Layout to be displayed on the routed page.

### Advanced Route Nesting

#### Layouts For All Child Components To Share

Think of this as a sub-navigation architecture for a group of pages.

Copy-pasta code to each Component that needs those links? *no*

Instead, create Layouts that all child components share:

1. Create an ItemLayout.js functional Component that imports Link. This will contain *only* the navigation.
1. ItemLayout.js returns a fragment with `<Link ...>` entries for the sub-navigation that is needed across multiple pages.
1. Update the Component that displays the page where shared links will end up rendering to it will only return what you need that page to show (Kyle's example: `<h1>blah</h1>`).
1. Wrap the Layout Component around all other components within the Route definition.

```javascript
// wrap the Layout Component around the components within a route definition
// imports etc above this return statement:
return (
  <>
    <nav>
      <ul>
        <li>
          <Link to="/">Home</Link>
        </li>
        <li>
          <Link to="/about">About</Link>
        </li>
      </ul>
    </nav>
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="/items" element={<ItemLayout />} >
        <Route index element={<Items />} />
        <Route path=":id" element={<Item />} />
        <Route path="new" element={<NewItem />} />
      </Route>
      <Route path="/about" element={<AboutUs />} />
      <Route path="*" element={<NotFound404 />} />
    </Routes>
  </>
)
```

But wait, *there's more*!

1. Import component 'Outlet' from react-router-dom.
1. Add the component to the bottom of the ItemLayout component fragment.
1. No attributes or args are necessary.

When the Layout renders, Outlet component will display which route (page) is currently selected!

*Note*: Only child components to the '/items' path will have this child-list of links, per the Routes list!

#### Multiple Routes Share Same Layout, but Different Path

Simple solution: Remove the 'path=""' attribute and retain only the 'element={}' attribute!

Remember though, if the components *do share the same path*, do not make this edit.

Also, this technique will support child nesting, as discussed in the previous subsection.

#### Outlet Context

Attribute Context can be added to the Router Outlet component.

```javascript
// within the return fragment of a Layout Component
  <Outlet context={{ hello: "World" }} />

// in another component, capture the context as defined in Outlet
const ctxt = useOutletContent();
```

Works like a React context.

Allows passing down a value from another Component.

The Outlet Component will return a KVP and any Component that uses 'useOutletContext' can capture that data and use it!

This can be useful when there are several components and shared layouts.

## Footer

Return to [conted index](./conted-index.html)
