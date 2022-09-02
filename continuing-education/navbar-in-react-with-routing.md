# Creating a Navbar in React with Routing Notes

Key takeaways and code samples from the video.

## Example navbar

Is a header with a site title and nav items in it.

1. Create a functional component called Navbar
1. In the return statement return a `<nav>` element enclosing an anchor tag to root for the title of the site
1. Create an unordered list
1. Add list items that contain the name and href to the target page
1. Once the navbar is done create pages to navigate to

## Using React Router

In the top-level component (e.g. App) add `window.location` to get the URL of the page that was navigated to.

Review Console output, Location member, to see properties *href*, *origin*, and *pathname*.

Using a switch statement on `window.location.pathname` and set cases for each literal path:

```javascript
import Navbar from "./Navbar.js";
import Home from "./pages/Home.js";
import Contentpage from "./pages/Contentpage.js";
import About from "./pages/About.js";

function App() {
  let Component;
  switch (window.location.pathname) {
    case "/":
      Component = Home;
      break
    case "/contentpage":
      Component = Contentpage;
      break
    case "/about":
      Component = About;
      break
  }
  return (
    <>
    <Navbar />
    <Component />
    </>
  )
}
```

## Marking Links as Active in Navbar

Make the currently selected Nav item highlighted after clicking:

1. Create a function (rfc) called CustomLink
1. Configure for 3 parameters, and put them in braces e.g. `function CustomLink({href, children, ...props}) { return() }`
1. Add a path variable: `const path = window.location.pathname`
1. Configure the list item tag in the return statement className attribute to be "active" or empty string on `path === href`
1. The LI child anchor tag will have attributes as so: `href={href} {...props}`
1. Anchor tag content will be `{children}`

## Without Any Router At All


## Navbar CSS Styling Suggestions

Use UL and LI elements to create the set of links for the nav bar.

Add styling for nav elements:

```css
.nav {
  background: #color;
  color: #opposite-color;
  display: flex;
  justify-content: space-between;
  align-items: center;  //  try 'stretch' if alignment still isn't quite right
  gap: 2rem;  // space between
  padding: 0 1rem;  // space to edges
}
```

Prettify the links:

```css
.nav ul {
  padding: 0;
  margin: 0;
  list-style: none; // eliminate extra spacing and the bullet icon
  display: flex;
  gap: 1rem;
}
```

Style the nav anchor tag:

```css
.nav a {
  color: inherit;
  text-decoration: none;
  height: 100%; //  ensure link is as tall as its container content area
  display: flex;
  align-items: center;
  padding: .25rem;
}
```

Style the links so they change appearance when hovered vs. non-hovered:

```css
.nav li.active {
  background-color: #some-background-color; //  when selected or tabbed changes the background color for contrast
}

.nav li:hover {
  background-color: #different-background-color;  //  when hovered alters the background color for contrast
}
```

## Pages to Navigate To

Suggestions:

- Each is its own component
- Might/not be in a subfolder e.g. './src/pages'

## Footer

Return to [conted-index.md](./conted-index.html)
