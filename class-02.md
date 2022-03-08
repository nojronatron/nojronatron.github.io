# Notes from Duckett HTML and JS Books

## HTML Book Chapter 2: Text

Focus of this chapter are structural markup and semantic markup.  

### Structural Markup

Headings:  

- `<h1>` through `<h6>`  
- Require ending tags too  
- Exact size of headings will vary from browser to browser  

Paragraphs:  

- `<p></p>`  
- Browsers render each paragraph as a new line  

Bold and Italic:  

- `<b></b>`  
- Bold is good for use of *keywords*  
- `<i></i>`  
- Italics indicate the word(s) are said in a different way e.g. technical terms, names of ships, foreign words *[Ducket, pg.45]*  

Superscript and Subscript:  

- `<sup></sup>`
- Superscript applies to e.g. `9th` or in math when denoting 'to the power of'  
- `<sub></sub>`
- Subscript applies to characters often used in chemical notation like 'CO2'  

White Space:  

- Largely ignored beyond the first whitespace character  
- 'White space collapsing' causes multiple space characters to be compressed down to one in html text  

Line Breaks and Horizontal Rule:

These are 'empty elements' and require the closing tag character `/` within these single-tag elements.

- `<br />`
- Forces a line break  
- Content following this will be on a new line, similar to the paragraph tag but can be used within it  
- `<hr />`
- Causes a horizontal line to be drawn at the location the element is placed  

### Semantic Markup

These add information to a web page, and are used by screen readers and other assistive tools.

Strong and Emphasis:

- `<strong></strong>`  
- Indicates important content  
- `<em></em>`  
- Subtle change in meaning to the sentence  
- Text will appear italicized in the browser  

Quotations:

- `<blockquote></blockquote>`  
- Use these when quoting a large amount of information, like an entire paragraph or page of content  
- Render indented compared to a paragraph element  
- `<q></q>`  
- Use for shorter quotes like single or small number of words or amount of content  
- Meant to add quote marks `"` by browsers but IE does not  

Both blockquote and q include an optional `cite` attribute that should be configured with the URL of the source of the quotation

Abbreviations and Acronyms:

- `<abbr></abbr>`  
- attribute 'title' is used to add the fully unrolled term  
- html4 used an acronym element but html5 does not

Citrations and Definitions:

- `<cite></cite>`  
- Reference a piece of work when used for research, a book, etc  
- The enclosed content will be rendered as italicized  
- `<dfn></dfn>`  
- Used when explaining terminology  
- "Indicates the defining instance of a new term" *[Duckett, pg.54]*  
- Browsers could render as italicized content, but is not guaranteed  

Author Details  

- `<address></address>`  
- Use for contact details  
- Browsers render as italics  

Changes to Content

- `<ins></ins>`  
- shows content that has been inserted and is rendered with an underline  
- `<del></del>`  
- adds a 'strikethrough' to the content between the tags  
- `<s>`  
- indicates an inaccurate or deprecated content  

## HTML Book Chapter 10: Introducing CSS

CSS is like a set of rules the browser follows to layout, colors, size and shape of the content.  
CSS terminology:

- selector: an element, class, or id that the CSS declaration will apply to  
- declaration: the CSS code that will apply to the selector  
- property: the CSS attribute that is getting configured  
- value: the value the CSS attribute will take on

### External CSS  

- href: set the path to the external css file  
- type: defines the document type, for example `text/css`  
- rel: short for relationship, mates the HTML page with a linked resource  

Web sites can reference multiple external stylesheets.  
Pages can share the same style sheet.  
Single place to edit style information for the entire site.  
Inline CSS rules can be eliminated (or minimized) thus cleaning-up the code.  
Is a best practice.  

### Internal CSS

Set CSS style rules for the current page.  
Usually stored in the `<head>` element, and/or in-line with html elements.  
Single-page websites might use internal css to keep everything together.  
Apply a few rules to a page with an external CSS ref, for specific situations (not a best practice).  
For code examples in a learning textbook like Duckett's HTML and CSS boook.  

### Selectors

Several portions of this were lifted from *[Duckett, pg238]*  

- Universal: all document elements in the current page  
- Type: matches element names like `<h1>` etc  
- Class: matches class atribute of one or more elements, starts with a period like `.elClass`  
- ID: matches id attribute of an element, prefixed with the hash symbol like `#elId`  
- Child: matches direct child attributes. Selector usage: `li>a {}`  
- Descendant: matches element that is descendant of primary element. Selector usage: `p a {}`  
- Adjacent Sibling: matches element that is next sibling of another. Selector usage: `h1+p {}`  
- General Sibling: matches elemnt that is sibling of another. Does not have to be the direclty preceding element. Selector usage: `h1~p {}`  

### How CSS Rules Cascade

CSS Rules have an order of precedence:

- Last Rule: the latter of duplicate selectors takes precedence  
- Specificity: the more specific rule takes precedence  
- The `!important` indicates the rule is higher precendence than other rules that apply to the same element  

### Inheritance

Several portions of this were lifted from *[Duckett, pg240]*  

- some properties are inherited by child elements, and therefore the declarations can be simplified  
- some properties are NOT inherited by child elements such as border and background-color  

### Different Versions of CSS and Browser Quirks

CSS Definitions and releases overview:  

- 1996: CSS1.  
- 1998: CSS2.  
- Current, ongoing standard: CSS3.  

Meanwhile, there are many browser makes and models, and releases.

- Not all CSS declarations or properties will function as expected in all browsers  
- Always test every change when working with CSS  
- Use online tools  

Browser Quirks aka CSS bugs: A CSS property that displays in an unexpected way.  

Online CSS Validation Tools Reference *[Duckett, pg.242]*

- [Browser Cam](https://www.browsercam.com)  
- [Browser Lab](https://www.browserlab.adobe.com)  
- [BrowserShots](https://www.browsershots.org)  
- [CrossBrowserTesting](https://www.crossbrowsertesting.com)

CSS Bug Sites Reference *[Duckett, pg.242]* 
 
- [PositionIsEverything](https://www.positioniseverything.net)  
- [QuirksMode](https://www.quirksmode.org)  

## JS Book Chapter 2: Basic JavaScript Instructions

## JS Book Chapter 4: Decisions and Loops (up to switch statement)
