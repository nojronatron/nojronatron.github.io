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
