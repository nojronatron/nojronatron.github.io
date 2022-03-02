# Summarized topics

## From the Duckett HTML book

### Introduction (pp.2-11)   
The internet is a global network connecting computers together. Computers have unique IP addresses (like a home street address) allowing other computers to find them. A naming system called DNS is like a directory that provides a lookup of human-readable names like www.microsoft.com into ip addresses like 192.168.123.10. Web servers on the internet are like special file servers, hosting special files that web browsers can process and display on a users screen.   
Web browsers interpret HTML to display text on the page, arranging text elements into different parts of the page or with different styles.   
Cascading Style Sheets (CSS) are used to describe the layout and design details of the web page to a greater degree than HTML can do. CSS can change website colors, text properties like fonts and colors, and more.   
HTML5 is the latest revision of the HTML specifications.   

### HTML Chapter 1: “Structure” (pp.12-39)   
HTML   
- HTML pages are comprised of plain-text documents decorated with HTML Tags and HTML Elements.
- HTML Tags are identified with '<' and '>', and are usually in pairs surrounding the element name. 
- Examples:
  Opening tag `<head>`  
  Closing tag `</p>`    
- Between opening and closing tags is where content lies:   
  H tags: `<h1>Header H1</h1>`   
  Pairs of HTML tags are refered to as Elements.   

ATTRIBUTES   
Attributes are key-value pairs that help describe content stored within HTML elements. An example attribute:   
  `lang='en-us'`*[Duckett, pg.25]*.   
   
### HTML Chapter 8: “Extra Markup” (p.176-199)   
HTML 4 was released in 1997, XHTML (based on XML) was released in 2000, and HTML5 was initially released in 2008 and is now considered a *living standard* (see [Wikipedia](https://en.wikipedia.org/wiki/HTML5)). The most widely used browsers keep up with (or ahead of) HTML standards, and website developers must know how to tell the browser which version they are coding in.   

- DOCTYPE   
  'doctype' tells the browser the html version. Example: HTML5 is identified with `<!DOCTYPE html>` as the first line in an HTML page.   
- Comments
  Used to store developer notes within the code like section beginnings and endings, and do not appear on the rendered page, but are visible to anyone that uses a browser's built-in ability to 'view code'.   

ID ATTRIBUTES   
These is global and can be applied to any html element, so each must be unique on each web page. Usage:`<p id="id_name">text</p>`. ID Attributes are used to allow styling elements differently than others on the page, by using CSS. JavaScript can leverage ID attributes to work with HTML elements.   

CLASS ATTRIBUTES   
Class attributes allow identifying many attributes within a page by applying CSS to the class-named elements. Usage:`<p class="blue_font bold_font">text</p>`. This will make the P element content font take on the CSS featured programmed for that class name (presumably **bold** and blue).   

BLOCK AND INLINE ELEMENTS   
Block elements cause content to always appear on a new line, whereas Inline elements continue on the same line as neighboring elements (and their content).   
- Block elements include: `<h1> ..., <p>, <ul>, <li>, and <div>`  
- Inline elments include: `<a>, <b>, <em>, <img> and <span>`  
- The DIV element
  Allows grouping elements into a block-level box.   
  Use an ID or CLASS attribute to set spacing or change appears of all elements contained within the DIV.   
- The SPAN element
  Contains a section of text or any number of in-line elements.   
  Use to control the appearance of in-line content using CSS but using ID or CLASS attributes to target them.   

IFRAMES   
Iframe is short for Inline Frame. It forms a window within a larger document to place images, video, or other information.
- `SRC=` is used to point to the source content.
- `height, width, and seamless` properties are used to control the size of the iframe, and whether or not there is a scroll bar within it.   

META TAGS   
These live in the HEAD element and are not rendered in the browser, but they should contain descriptive information for the browser and Search Engines to use, like `author, description, published'... etc.   
- META Tags
  `<meta http-equiv="pragma" content="no-cache"/>` or `<meta http-equiv="robots" content="nofollow"/>`   

There are Search Engine properties, cache-controlling properties, and a viewport property.   
- VIEWPORT
  Controls the size of the page depending on what type of client is rendering it.   

ESCAPE CHARACTERS   
Escape Characters allow display of reserved HTML characters like the less-than sign aka left-angled-bracket: `<`.   
Use `&lt` or `&#60` to display the `<` character otherwise the browser might not be able to render the page at all.   
There are many other characters and special symbols like currency, the copyright symbol, and soome punctuation.   
**Advice:** If the wrong character (or nothing) appears in the spot where a reserved HTML character is expected try changing the Font to fix the problem.   

### HTML Chapter 17: “HTML5 Layout” (pp.428-451)   
This chapter discusses layout elements, how to get old browsers to understand html5 elements, and how to stylize elements with css.

TRADITIONAL HTML LAYOUTS   
`<div>` Groups together related elements on the page.   
`class` or `id` These attributes indicate the role of `<div>` elements.

HTML5 LAYOUT ELEMENTS
These elements are named after sectional areas of common web sites and have specific purposes that should be closely followed:   
   
- HEADER   
  Named after the commonly known header portion of a page.

- NAV   
  Contains *major* navigational blocks such as priimary site navigation links.

- ASIDE   
  Nested within `<article>` elements: Should contain information that is related to the article but not essential to its overall meaning for example: a pullqoute or a glossary *[Duckett, pg.436]*.   
  Used outside of Article elements: Should contain information that releates to the entire page for example: Links to other sections or list of recent posts *[Duckett, pg.436]*.   

- ARTICLE   
  Use as a container for any section of a page that could stand alone and potentially be syndicated *[Duckett, pg.437]*.
  Can be nested.   

- SECTION   
  Groups related content together and each section element would have its own heading.
  Can contain several distinct `<article>` elements.
  Can be used to break up a long article into smaller sections.
  **NOTICE!** Do not use as a wrapper for an entire page unless entire page is a distinct piece of content.
  Alternatively, use `<div>` to wrap content that could be within one or more section elements.

- HGROUP
  Groups `<h1>` etc headings together. Use it as a stylizing tool for multiple header elements.   

- FIGURE and FIGCAPTION
  Contain content that is referenced in the main flow of the article or page.
  Could be images, videos, graphs, diagrams, code samples... etc.
  Should be supportive of the main article and not a critical component or integral to the meaning of the main article.
  Should contain a text discription of the figure element contents:   
  `<figure> <img src="" /> <figcaption>caption_this_text</figcaption> </figure>`   

- DIV   
  Previous to HTML5 Layout Elements this was heavily used to define headers, nav, and so on.   
  Now, use DIV only if layout elements do not fit their stated purpose.   
  If there is no suitable html5 layout element, use `<div>` and assign a CLASS or ID attribute to style and control it.   

LINKING Around Block-level Elements   
Html5 allows surrounding block-level elements with an anchor element. The entire block between the tags becomes an active link. Attempting this in previous html versions could result in rendering or the link not functioning.   

HTML5 ELEMENTS IN OLDER BROWSERS   
Html5 can be used in older browsers but will be treated as *inline elements*. Include a line of CSS that tells the browser the html5 elements should be rendered as **block** elements instead:   
  ```
  <!--[if lt IE 9]>
  <script src="http://html5shiv.googlecode.com/svc/trunk/html5.js"></script>
  <![endif]>-->
  ```

### HTML Chapter 18: “Process & Design” (pp.452-475)   


## From the Duckett JS book

- Introduction
- JS Chapter 1: “The ABC of Programming” (pp.11-52)

# Remember To...
[ ] Bookmark additional resources
[ ] Present material as if to someone new to the industry
[ ] Cite sources with links when directly quoting

### Updated: 2-Mar-22