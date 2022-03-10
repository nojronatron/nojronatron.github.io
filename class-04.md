# Notes from Duckett HTML and JS Books

HTML Book Chapters 4 and 15  
JS Book Chapters 3  

## HTML Book Chapter 4 Notes - Links

Many reasons to link, usual suspects are:

- Bookmark an area within the same page to rapid jump-ahead or return.  
- Link to another page on the same website, like in a nev menu.  
- Link to another (external) website, like for a reference.  

### Structure

```html
<a href="">content</a>
```

- An anchor ('a') tag requires a closing tag.  
- Some content is expected between opening and closing tags.  
- 'href=' points to the URL aka the target of the link.  
  - Should be a full, absolute url for external sites.  
  - Should be relative url for internal "bookmark" links.  
- The content between opening and closing tags is rendered in the browser window.  
- Clearly displaying links to users (helps keep them around).  
- Write good link text (also helps keeps them around).  
- Anchor links 'shortcut' users around a site structure (e.g. nav links).  

URL construction will depend on whether the link is internal or external:

- External: Use the fully qualified URL to the *page* (usually the home page) of the external site.  
- Internal: Use *relative* URLs. There are some rules and tips to get these right:
  - Same-level link: enter the page filename.  
  - Parent to child: Add the hierarchy into the link like `child/page.html`.  
  - Parent to grandchild: Add the hierarchy like `child/grandchild/gcpage.html`.  
  - Child to parent: Reverse the hierarchy like: `../index.html`.  
  - Child to grandparent: Similar to P-to-GC but go UP the tree: `../../index.html`.  

### Email Links

```html
<a href='mailto:person@domain.org'>Email me!</a>
```

### Open Link In New Window

```html
<a href='https://www.google.com' target="_blank">Google Search</a>
```

### Linking to Specific Parts of a Page

Same Page:

- Use `id="bookmark_name` as the tag ID that surrounds the target content.  
- Point the anchor tag to the id like: `<a href="bookmark_name">here</a>`  
- The browser will scroll the window to put the tag in the viewport.  

Other Page:

- Use an ID in the target tag on the target page, like `<div id="SummaryLinks"><div>`  
- Point the anchor tag to the relative or fully-qualified URL and include the id like:

```html
<a href="http://my-site.com/#SummaryLinks">Summary Links on my site</a>
```

## HTML Book Chapter 15 Notes - Nnnn

### Positioning Elements

The BOX concept defines how elements act, and where elements get placed, within a web page.  
Boxes can be block-level or in-line.  
Block-level elements start on a new line.  
Inline elements flow inbetween surrounding text.  
Nested elements are refered to, contextually, as parent and child(ren), where the parent is the containing element.  

Controlling the position of elements can be achieve with:

- Normal flow: basicallyl top-to-bottom, vertically stacked elements.  
- Relative Positining: Assign a position based on another point on the page.  
- Absolute Positioning: Place a child element based on its parent elements positioning.  
- Fixed positioning: Assign a specific anchor point on the page.  
- Floating elements: Floating an element takes is *out of the normal flow* of page positining, and place it to the left- or right-side of a containing box.  
  - "Floated elements become a block-level element around which other content can flow." *[Duckett, pg.364]*  

*Note*: Use the Z-index to set the "bring to front" and "send to back" equivalent effect on a box.  

FLow Details:

- Normal Flow: `position: static;` Causes a top-to-bottom layout of elements.  
- Releative Positioning: `position: relative;` Moves an element relative to 'normal flow' positining.  
  - Set in px, '%', or em  
- Absolute Positioning: `position: absolute;` Takes box out of normal flow and offsets it to absolute location. Must include a width settings.  
- Fixed Positioning: `position: fixed;` Similar to absolute, relative to the *browser window* rather than another element. Similar offset property settings to Absolute.  

Overlapping Elements:

- Has the effect of 'stacking' elements on top of each other.  
- Use the Z-index to define which one is in front.  

Floating Elements:

- Any text in the parent box will flow around the floated element.
- Usage: `float: right;` to push the box to the right-hand side of the parent box.  
- Floated boxes can be placed side-by-side, see *[Duckett, pg.371]* for details.  
- Clearing Floats: Stops contained boxes from touching the Left or Right sides of the parent element.  

*The zero pixels tall problem*: Some browsers might treat Floated elements as if they were zero pixels tall. To solve this:  

```css
div {
  overflow: auto;
  width: 100%;
}
```

### Multi-column Layouts with Floats

You Must Define These rules to `<div>` elements to enable the 'column' box behavior:

- `width:`  
- `float:`  
- `margin:`  

### Screen Size, Resolution, and Pages

Various computers, hand-helds, phones, etc will have different screen sizes.
Take screen-size differences into account when designing a website.  
Screen resolution varies from device-to-device as well, which impacts an absolute setting like px.  
Page sizing is important, and good sizing decisions will help all users view a well-desgined page.
*Recommendation*: Stick with page widths of around 960-1000 px.  
Try to capture user attention within the first 500-700px vertically on the page, and let them know there is more 'below the fold' and entice them to scroll down.  

#### Fixed Width Layouts vs. Liquid Layouts

Fixed-width Layouts

- Pros: Pixel values good for positioning; direct control over design of layout; Content 'line lengths' can be controlled, regardless of viewing device; Static image sizing.
- Cons: May show unexpected gaps between elements; Text can be reduced to a hard-to-read point size; Text might not fit within layout if font size is increased; Works best on desktop-computer sized screens, not so in smaller screen devices; Often times more vertical/scroll space is consumed than might be wanted.

Liquid Layouts

- Pros: Fills entire screen; Page will contract to accommodate smaller screens; Can accommodate end-user changing font-size.  
- Cons: Controlling the width is critical otherwise might get very unexpected layout results; Content text lines can get too long to easily read on larger screen devices; Text may stack vertically on smaller screens; Images could overflow text if the screen size is reduced.  

### Layout Grids

- Create continuity in layout, between pages.  
- Predictably layout locations for boxes.  
- Allows consistent content additions, simply.  
- Enables collaborative design in a consistent way.  

The book talks about the 12-column layout design where spanning columns is used to set box widths, thereby creating an interesting, consistent layout of elements on the page. Column widths are set specifically, and evenly to provide consistency when designing box layout.

The book also links up a pre-defined CSS file "960.gs" as a starter for designing a Layout Grid for your site.  

Advantages:

- Reduces repeating code for similar tasks.  
- When tested across browser versions can provide consistent results.  

Disadvantages:  

- Use of many class names that are used only for style and layout, but do not describe the content.  

### Multiple Stylesheets

Use `@import` in your stylesheet to reference another stylesheet.  
Reference multiple stylesheets using the Link element `<link rel="stylesheet" type="text/css" href="css/mystyle.css" />` statements.  

*Note*: When using multiple stylesheets, rules of precedence can make determining final applied style more complicated.

## JS Book Chapter 3 Notes - Functions

*Only cover pgs. 86-99  

Functions: Perform specific actions with a block of code.  
Objects: User-created items that store data in a specified format, sometimes providing properties about the data or manipulate data.  
Built-in Objects: JavaScript provides some objects with members that are commonly used to perform tasks.  


## Reading: 6 Reasons for Paired Programming

Personal notes while reading the Code Fellows blog article about [Paired Programming](https://www.codefellows.org/blog/6-reasons-for-pair-programming/)  

Blog Author: *[Allie Grampa]*  

Key takeaways:  

- Pair Programming is a common, agile workspace activity.  
- Two developers share one screen and develop, together.  
- Develops skills and encourages collaboration.  
- Driver: The dev on the keyboard. The mechanic of code, text editors, handling files and version control.  
- Navigator: The guide, with a higher-level perspective on the project, design questions like how to convert algorithm to code, and also bug watcher. Could also be the reference librarian, looking up resources, but is not necessarily writing any code.  

Learning to Code:

Core skills are put to work:

- Listening  
- Speaking  
- Reading  
- Writing  

Lab sessions for pair programming will take place at Code Fellows to learn and practice Paired Programming skills and processes.  

Benefits include:

- Effeciency in coding. Arguably slower, but code quality usually higher in design, idiomatic style, and fewer bugs.  
- Enhanced collaboration within the team.  
- Additional learning opportunities between paired programmers, as they learn from each other.  
- Build communication, collaboration, and other social skills.  
- Preparedness for job interviews and on-the-job expectations or processes.  
