# Notes from Duckett HTML and JS Books

Notes taken from Ducketts HTML book chapter 15 "Layout".  

[Back to index in readme](./README.md)  

## HTML Book Chapter 15: Layout  

### Building Blocks

Two primary types of boxes in a *flow* are *block-level* and *inline*.  

- Inline: The flow is horizontal: alongside and inbetween other elements and content.  
- Block-Level: The flow is vertical: Above and below other elements.  

### Containment

- Parent-child relationships are built when one box is created inside of another box.  
- Parent elements are referred to as *containing* elements.  
- Containing elements are always direct parents of the element they contain.  

### Controlling Position of Elements

Three primary positining *schemes* used to control layout:

1. Normal Flow (the default)  
2. Relative Positining  
3. Absolute Positioning  

*Box Offset Properties* are used to further refine where the box will be placed. They are:

- Fixed: Property of Absolute positioning. Position is relative to the browser window. Box become statically assigned to the viewport and *does not mingle with other elements in the flow*.  
- Floating: Converts the element into a block-level element and allows positioning *left* or *right* only.  

*Note*: Boxes taken out of normal flow gain a Z-index property that effects overlap (i.e.: bring to front).  

### Normal Flow

By default, block-level elements align themselves vertically, from top-to-bottom of the page or containing element.  

position:static

- Optional property that basically sets the 'Normal flow' behavior.  

### Relative Positioning

Element position is adjusted with relation to *normal flow*.  

Adjust relative position to Normal Flow using properties meaning "from the..." top, right, bottom, or left. For example:

```css
p {
  position: relative;
  top: 10px;
  left: 150px;
}
//  this moves the box within the flow 10px down and 150px right from its Normal flow position
```

### Absolute Positioning

Removes the element from Normal Flow and pins it into a specific location *relative to its containing element*.  

The `position:absolute` scheme causes the element to remain on-screen in the offset position identifies in CSS:

```css
h2 {
  position: absolute;
  top: 50px;
  left: 100px;
  width: 300px;
}
//  places the box to a position relative to the containing element by moving it down 50px, right 100px, and 300px wide.
```

### Fixed Positioning

Similar to Absolute Positioning but *relative to the browser window*.  

Use this to keep a header within view of the user while the user scrolls down the screen.  

This is also effective to keep a background image in-place while the content scrolls in front of it.  

```css
header {
  position: fixed;
}
```

### Overlapping Elements

Causes elements to overlapp one another along the Z-axis, or front-to-back.  

The 'z-index' is an integral-weighted property, so the higher-value number is more likely to appear "on top" of other lower-valued z-index elements.  

```css
article {
  z-index: 10;
}
```

### Floating Elements

These elements are allowed to 'float' horizontally as far left or far right as possible.  

This is used to display "insets" throughout magazine or blog articles.  

The content will *flow around* the floated element.  

Does *not* change vertical positioning of the floated element, but *can* impact positioning of other elments around it, depending on the floated element's content height.  

*Note*: A width property *must be designated* to enable the element to float.  

```css
div {
  float: right;
  width: 200px;
  font-style: italic;
  font-size: 1.2em;
}
// causes the div element to inset far to the right side of the parent element, possibly an article or section
```

One problem with floated elements is their positionings cannot always be assured due to content overall height.

Resolve *float problems* by using the 'clear' property.  

Clear tells the contained elements they cannot touch a left or right sides of a box.  

- `clear: left`: Left side of box cannot touch other elements within same parent.  
- `clear: right`: Right side of box cannot touch other elements within the same parent.  
- `clear: both`: Neither side of a box can touch other elements within the same parent.  
- `clear: none`: Both sides *are allowed* to touch other elements within the same parent.  

#### Parent of Floated Elements

*Zero-pixel Problem*: If a containing elements has only floated children, a browser could render them 0px tall.  

To resolve this problem set a width value and an overflow value to the parent elements:  

```css
#parentdiv {
  width: 100%;
  overflow: auto;
}
// solving the zero pixel problem within a parent element that contains only floated elements.
```

### Multi-column Floats

Place `<div>` elements next to each other to form a columnized layout.  

Assign width, float, and margin to the parent containers (i.e. div elements) to set the layout.  

Create more divs and assign css proprties float, width, and margin, to set their layout accordingly.  

```css
#leftdivcol {
  float: left;
  width: 6500px;
  margin: 10px
}
#rightdivcol {
  float: left;
  width: 250px;
  margin: 10px;
}
```

### Screnn Sizes and Resolution

Many screen sizes and pixel-depth view ports exist today, including but not limited to:

- Smartphone: 960x640  
- Tablet: 1024x768  
- Laptop: 1280x800  
- Desktop monitor: 2560x1440  

Due to the vast array of possible devices, it is good practice to target the smallest viewport to ensure a good layout.  

*Note*: Smart phones and tablets can be rotated between portrait and landscape modes, which could provide additional screen realestate for a particularly wide (or tall) page layout.  

### Fixed Width Layouts

Controlled size through pixel-count width settings.  
Great control over the layout and appearance since the width is pixel-precise.  
Various elements will always be the same, pinned to the pixel settings, regardless of the user device/view port.  
Images to not resize or scale due to window resize or different device/view port used.  

Achieved through settings width on main boxes on page set in pixels. Optionally, height set in pixels too.  

Specifically, set the width to px on these elements:  

- Body
- Div
- Section
- Article
- Specialized column layouts (using divs or other elements)

Unfortunately:  

- Layout can get gappy.  
- Text could become too small to read on a larger display.  
- Increased font size by the user could cause content to spill-over the elements.  
- Usually works best for laptop and desktop computer monitor pixel depths.  
- Additional vertical space might be needed to contain the content in the pixel-resticted space.  

### Liquid Layouts

Elements expand and contract in response to screen pixel depth / size.  
Less use of scrollbars to access content because it resizes instead.  
Allows user change of font size without detrimental effects like overflowing boxes.  

Acheived through settings *percentages* rather than pixels in width (and optionally height) properties.  

Specifically, set the width to percentages on these elements:  

- Body
- Div
- Section
- Article
- Specialized column layouts (using divs or other elements)  

However:  

- Developer must carefully dictact the width of page sections, else the layout could change in undesireable ways.  
- Very large (wide-window) displays could cause text to become too long to comfortably read.  
- Conversely, very thin windows will cause content to squish and line length will be very short, making it uncomfortable to read.  
- Images can overflow text if the parent item is shrunk down too small for the image height/width.  

### Layout Grids

Grid structures are used to help layout items on a page consistently, with controlled spacing and column counts and sizings.  
Users can more easily find information because the layout is very predictable.  
*spanning* columns allows widened boxes in which to place content.  
The 12-column example in the book layous out a 940px wide window containing 12 columns that span various numbers of columns that controls where the child elements appear on the page.  

### CSS Frameworks

Frameworks provide shortcuts and functionality that is otherwise difficult or not possible without them.  
They can generate code for you or otherwise encapsulate often-used or complex syntax into a simple command possibly with some parameters.  
Frameworks are heavily tested, and usually documented to get users up and running without having to test the solutions prior to utilizing them.  

Drawbacks:

Specifically for HTML and CSS, only the presentation portion of the work is done for you.  
Frameworks can contain a *lot* of code and be more than what your project needs (or you want in the codebase).  

### 960.GS Grid

Many frameworks utilize a grid system for managing layouts.  
A stylesheet is included with 960.gs to manage the layout for you - just link the HTML page to the 960.gs stylesheet.  
Setting the number of coumns and widths of columns is fairly simple by setting class attributes.  

Some other grid frameworks:  
[blueprintcss.org](https://blueprintcss.org)  
[lessframework.com](https://lessframework.com)  
[developer.yahoo.com/yui/grids](https://developer.yahoo.com/yui/grids/)  

### Multiple Stylesheets

Use `@import` or `link` to attach multiple stylesheets to the webpage.  

`@import`: Use in-line in the CSS page to import the targer stylesheet:  

```css
@import url("newsprint.css");
@import url("tinyprint.css");
```

`<link href="stylesheet.css">`: Use within html to link the page to a stylesheet.

*Remember*: The last loaded and most-specific rules take precedence.  

[Back to Top](#notes-from-duckett-html-and-js-books)