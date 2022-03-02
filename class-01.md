# Summarized topics

## From the Duckett HTML book

- Introduction (pp.2-11)   
The internet is a global network connecting computers together. Computers have unique IP addresses (like a home street address) allowing other computers to find them. A naming system called DNS is like a directory that provides a lookup of human-readable names like www.microsoft.com into ip addresses like 192.168.123.10. Web servers on the internet are like special file servers, hosting special files that web browsers can process and display on a users screen. Web browsers interpret HTML to display text on the page, arranging text elements into different parts of the page or with different styles. Cascading Style Sheets (CSS) are used to describe the layout and design details of the web page to a greater degree than HTML can do. CSS can change website colors, text properties like fonts and colors, and more. HTML5 is the latest revision of the HTML specifications.   

- HTML Chapter 1: “Structure” (pp.12-39)   
HTML pages are comprised of plain-text documents decorated with HTML Tags and HTML Elements. HTML Tags are identified '<' and '>' and are usually in pairs. An opening tag example is `<head>`. A closing tag example is `</p>`. Between opening and closing tags is where content lies, for example: `<h1>Header H1</h1>`. Pairs of HTML tags are refered to as Elements.   
Attributes are key-value pairs that help describe content stored within HTML elements. An example attribute is `lang='en-us'` *[Duckett, pg.25]*.   

- HTML Chapter 8: “Extra Markup” (p.176-199)   
HTML 4 was released in 1997, XHTML (based on XML) was released in 2000, and HTML5 was initially released in 2008 - it is now considered a *living standard* (see [Wikipedia](https://en.wikipedia.org/wiki/HTML5)). The most widely used browsers keep up (or ahead) of these releases of HTML, and website developers must know how to tell the browser which version they are coding in. 'doctype' tells the browser the html version, and HTML5 is identified with the following code: `<!DOCTYPE html>`. Comments are used to store developer notes within the code like section beginnings and endings, and do not appear on the rendered page, but are visible to anyone that uses a browser's built-in ability to 'view code'.   
The ID attributes is global and can be applied to any html element, so it must be unique on each web page. Usage: `<p id="id_name">text</p>`. ID Attributes are used to allow styling elements differently than others on the page, by using CSS. JavaScript can leverage ID attributes to work with HTML elements.   
Class attributes allow identifying many attributes within a page by applying CSS to the class-named elements. Usage: `<p class="blue_font bold_font"> text</p>`, which will make the P element content font take on the CSS featured programmed for that class name (presumably **bold** and blue).   
Block elements cause content to always appear on a new line, whereas Inline elements continue on the same line as neighboring elements (and their content).   
`Block elements include: <h1> (etc), <p>, <ul>, <li>, and <div>.`   
`Inline elments include: <a>, <b>, <em>, <img> and <span>.`   
DIV element allows grouping elements into a block-level box. Use an ID or CLASS attribute to set spacing or change appears of all elements contained within the DIV.   
SPAN eleemnt contains a section of text or any number of in-line elements. Use them to control the appearance of in-line content using CSS. Use with ID or CLASS attributes to target them.   
IFRAME: Short for Inline Frame. Forms a window within a larger document to place images, video, or other information. SRC is used to point to the source content and other properties like height, width, and seamless are used to control the size and whether or not there is a scroll bar within the IFrame.   
META tags: These live in the HEAD element and are not rendered in the browser, but they should  have descriptive information for the browser or Search Engines to use, such as Author, description, published, etc.   
The tags look like this: `<meta http-equiv="pragma" content="no-cache"/>`   
or this: `<meta http-equiv="robots" content="nofollow"/>`   
There are Search Engine properties, cache-controlling properties, and a viewport property to control the size of the page depending on what type of client is rendering the page.   
Escape Characters allow display of reserved HTML characters like the less-than sign or angled-bracket: `<`. Use `&lt` or `&#60` to display that character, otherwise the browser might not be able to render the page at all. There are many other characters and special symbols like currency, the copyright symbol, and soome punctuation. **Advice:** If the wrong character (or nothing) appears in the spot where a reserved HTML character is expected, try changing the Font to see if that fixes the problem.   

- HTML Chapter 17: “HTML5 Layout” (pp.428-451)   


- HTML Chapter 18: “Process & Design” (pp.452-475)   

## From the Duckett JS book

- Introduction
- JS Chapter 1: “The ABC of Programming” (pp.11-52)

# Remember To...
[ ] Bookmark additional resources
[ ] Present material as if to someone new to the industry
[ ] Cite sources with links when directly quoting

### Updated: 2-Mar-22