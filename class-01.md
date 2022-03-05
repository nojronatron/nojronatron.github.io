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

OVERVIEW
The chapter covers a process for creating a new website, and includes suggestions for the design process. It is important to get to know your website visitors (current and potential), why they would visit the website and what they are looking for, and how the website will get them what they need. Information can be organized and stylized in ways that helps visitors meet their goals, as well as produce a professional and functional website.   
   
WHO IS THE SITE FOR?   
Determine who wants to use the site, but understand it cannot serve everyone. Acquire information from target audience, including demographics, to help design the site organization and design.   
- Are the visitors individuals?   
   Ask questions about age, gender (and ratio thereof), where they live.   
   Also consider income, education level, martial status and occupations.   
   Also consider how long individuals would want/need to be on the site, and the device(s) they might use.   
- Are the visitors Companies/Organizations?   
  Ask questions about the size of the organizatino or department, and positions within the company.   
  Also determine the buget of the organization and whether visitors are using the site for themselves or for someone else.   

Develop a matrix of the above information so questions about what the website should look like, the information it will contain, and how the website will operate can be better answered during the design process.   

WHY VISIT THE WEBSITE?   
Visitors sometimes find wesites by chance, other time there are motivators and goals that drive users to a website. These should influence the design and content of the webiste.   

- Motivators can be:
  - General entertainment  
  - Acheiving a personal or professional goal  
  - Essential or luxury use of the site  

- Goals can be:   
  - Perform general research or look for specific detailed information, product, or service   
  - An expectation by the users that they do (or don't) know how the website works and whether they might need to get introduced to it  
  - Time sensitivity to the information they seek, such as breaking news or financial information or looking up historical information   
   
WHAT ARE VISITORS TRYING TO ACHIEVE?   
ID the key motivators and goals to help design the website appropriately for intended audience.   
Create a list of reasons for various imaginary users to come to the website and use this as a guide in the design.   

WHAT INFORMATION DO VISITORS NEED?   
- Think about additional information that might be helpful to your visitors.   
- Determine what each visitor needs to meet the goals of their visit.   
- Determine the most important information vs least important, and apply those priorities to the design.   
- Failing to provide visitors with information they need could prompt them to leave.   
- How familiar are the visitors with the product and/or information on the site, or the brand?   
- What site features are most critical to what the site offers, and does it differentiate from other, similar sites?   
- After a visitor achieves their goal for visiting the site, what common information will they be interested in? For example, a shopping cart will provide an estimate for when a completed order will arrive and by what shipping service.   
   
HOW OFTEN WILL PEOPLE VISIT?   
Sites offering time-sensitive information or regularly changing information might see more users that other types of sites.
The cost and effort to update a site regularly should be considered in site design to make it easy to update especially for higher-traffic sites.
Consider settings scheduled site updates (quarterly, daily...whatever fits the goals of the users and purpose of the site).
Regularly or often updated pages could see benefits over pages that are not updated as often.

For goods & services sites: *[Duckett, pg.460]*  
>	How often do same people return to purchase from you?  
>	How often is your stock updated or your service changed?  
For Infomration sites: *[Duckett, pg.460]*   
>	How often is the subject updated?  
>	What percentage of visitors return for regular updates, compared with those that need the info just once?     
   
SITE MAPS   
- Organize the site to appropriately section the information, prioritizing user-goals to drive the design.   
- Diagram the site structure, naming the pages, and identifying the home page, primary topics, and sub-topical pages.   
- A user survey can help organize a useful structure.   
- Duplication might be required, if info is related to several pages across the site.   
- Appropriately groups pages will help site visitors navigate easily.   
   
WIREFRAMES   
- Sketches of key information for each web page on a site.   
- Get an idea as to what space is necessary and how it could be arranged.   
- Can ensure all necessary info get onto each page as intended.   
- Are information-focused, rather than style.   
- Can use these to get feedback from client/users, without worrying if they are judging style and look rather than layout and info.

Wireframe tools list from *[Duckett, pg.463]*:   
-	Photoshop templates from 960.gs  grid system   
-	Paper and pencil or whiteboard   
-	Illustrator, InDesign, or another graphics application   
-	[GoMockingBird.com](http://gomockingbird.com)   
-	[LovelyCharts.com](http://lovelycharts.com)   
   
DESIGN TO GET MESSAGE ACROSS
Content should have been sorted out already, sonow the design needs to organize and prioritize the content to guide users and lead users to what they are looking for. Use styles to make portions of the page distinct from other content, calling it out to the user. Can also draw a user's attention away from content items.   

Visual Hierarchy   
- >Helps users focus on the key messages that will draw ... attention, and then guide them to subsequent messages. *[Duckett, pg.465]*   

The book has a visual hierarchy example *[Duckett, pgs. 467-468]* that I have arranged into key statements, below:   
-	Use pictures and strong colors and larger regions to call attention to the primary message on the page.   
-	Add details below in more passive colors and arrangements.   
	--	Size: Larger get attention first.   
	--	Color: Pick fore- and background colors specifically for key messages, using bright sections to draw users eyes.   
	--	Style: Varying syles can make items stand out, even if size and color are the same.   
	--	Contrast: High contrast tends to draw attention, so put the highest priority content there.   
	 
Related content should be put into "blocks" or "chunks" to keep it simple to follow and understand.   
   
Use similar visual styles for similar content so users quickly associate the style with the purpose or information.   
-	Buttons or links   
-	Info on groupings and similarity on pages 469-470   
	-	Grouping chunks similar content throughout the page and separates different contents or types   
	-	Groups of groups buttons or information help the user understand the purpose of the information   
	-	Similarity is used to provide consistency between like-type elements and information e.g. icons and headings   
  
GROUPING AND SIMILARITY  
"Grouping related pieces of information together can make a design easier to comprehend." *[Duckett, pg.469]*   
  
Various ways to group information:  
-	Proximity: Close-together items are seen as related.  
-	Closure: There is a tendancy to imagine a recognizable pattern in a complex arrangement. Try to take advantage of that in the site design.  
-	Continuance: Items placed in a line are seen as related, and users will follow along the line.  
-	White Space: Gappage between items.  
-	Color: Make items pop by adjusting the background color to emphasize the foreground items.  
-	Borders: Lines drawn around related items, or between unrelated ones, can alter their groupings and releationship.  
-	Repitition:  
	-	Use same color, style, orientation, texture, font and/or shape to match content, and increase their priority or level of interest.   
	-	Consistency: A collection of items of the same type are easily identifyable as similar when they are styled consistently.   
	-	Headings: Concise info in a heading about what content is to follow helps the user identify content they are looking for (or not).   
  
SITE NAVIGATION   
Navigation design can help users find their way and understand what the site is about.   

Good navigation design principles:   
-	Concise: Limit options, down to 8 or less.   
-	Clear: Single-word links convey clues as to what info will be found at the link target.   
-	Selective: Point to primary content in the site, not additional info like legalease, login forms, etc.   
-	Context: Visual cues in the navigation helps user know where they are.   
-	Interactive: Change the color or some styling when hovered over or the link is clicked for visual cues.   
-	Consistent: Primary nav should be consistent across pages; secondary can change depending on where in the site the user is.
Primary, Secondary, and additional Navigation   
-	Primary Navigation is often along the top of a site. *[Duckett, pg.472]* on left-hand section of a page.   
-	Tertiary Navigation is often along the bottom of a page.   
-	Check out: How to implement search functionality for your site using Google Search (companion website content) *[Duckett, pg.471]*   
  
SUMMARY
The following list of items are quoted directly from *[Duckett, pg.475]*   
-	It's important to understand who your target auience is, whey they would come to your site, what information they want to find, and when they are likely to return.  
-	Site maps allow you to plan the structure of a site.  
-	Wireframes allow you to organize the informatin that will need to go on each page.  
-	Design is about communication. Visual hierarchy helps visitors understand what you are trying to tell them.  
-	You can differentiate between pieces of information using size, color, and style.  
-	You can use grouping and similarity to help siplify the information you present.  


## From the Duckett JS book   
   
### JS Book Introduction   
Goals of this book *[Duckett, pg.2]*:   
> 1. Understanding some basic programming concepts and terms...   
> 2. Learning the language itself ... vocabulary and how to structure your sentances.   
> 3. Becoming familiar with how it is applied ... today.   
   
JavaScript enables interactivity on a website. JS Can:   
1. Select text or elements, or find data input into a form.   
2. Modify items including text and attributes, and change proparties of items like images.   
3. Create rules for browser to follow, like: collect info, calculate a result, and then change webpage content.   
4. React, by taking action when something happens like a button click, textbox input change, page finishes loading, etc.   
   
The book will also address work-around for compatibility with older browsers and introduce JQuery.   
   
### JS Chapter 1: “The ABC of Programming” (pp.11-52)   
   
WHAT IS A SCRIPT AND HOW DO I CREATE ONE?   
Think of a script as a recipe or manual, that tells the computer what to do.   
When preparing to write a script, follow these steps: *[Duckett, pgs.17]*  
> Define the goal. What do you plan to achieve?   
> Design the script. Document smaller tasks and decision trees necessary to attain the stated goal.   
> Code each step. In this case, use _JavaScript_!   
  
Use flowcharts and lists to logically design the script:
- Flowcharts for decision-points.  
- Lists for small, appropriately detailed steps.  

*Vocabulary*: The keywords used in the script that a computer knows how to act upon.  
*Syntax*: A kind of sentance structure of vocabulary the computer can execute.  
*Programmatic*: Follow steps, one after another.  
  
HOW DO COMPUTERS FIT IN WITH THE WORLD AROUND THEM?  
Data Models: Represent what a thing is and what it can do.  
Objects contain Properties, Events, and Methods.  
Properties: Define what an object is, and contain data within the object like its color or state of being.
Events: Represent actions such as flipping a light switch in a room.  
Methods: Can take action on data, especially in response to events, such as a lamp illuminating when a light switch is flipped.  

PROPERTIES, ATTRIBUTES, and EVENTS  
An interesting note regarding properties and attributes *[Duckett, pg.28]*   
> The idea of name/value pairs is used in both HTML and CSS.
> In HTML an attribute is like a property:  
  - Different attributes have different names.  
  - Each attribute can have a value.  
> In CSS you can:  
  - Change the color of a heading by creating a rule that gives the color property a specific value.  
  - Change the typeface (a heading) is written in by giving the font-family property a specific value.  

Name-value pairs enable storing and acquiring property values. Example:
  A house can be painted a color. The property name could be 'paint' and the value could be 'yellow':  
  Object: House  
  Property name "color": value "yellow"  

Consider Events to be the interaction between objects or things. Some examples of events that could be acted upon:   
- When a user clicks a button or changes text in a form.  
- When a property of an object changes.  
- When a packet from a connected network is received.
Exactly what action to take when an event is "fired" can be defined by the developer. For example:
- When a user click the Submit button on a web page an event is fired and it can call a method that causes the form data to be stored in a database.  

METHODS  
A method defines what an object can do. It is a _capability_ of a thing.  
For example, when the user clicked the Submit button on the web page and that event was fired, the event can call a method that will show a popup message informing the user that the information was submitted successfully (or failed).  

PROPERTIES, EVENTS, and METHODS
When developing scripts and web pages with JavaScript:
- Define the _Properties_ that are involved.  
- Determine what _Events_ will happen and what (if anything) to do when they happen.  
- Create _Methods_ that will act on Properties based on Events.  
  
Back to the light switch example:  
1. The lightswitch object has a property ON that can be true or false.  
2. When the "flip switch" event occurs it will call a specific method to do some work.  
3. The called method changes the property from false to true, for example.  
  
WEB BROWSERS ARE PROGRAMS BUILT USING OBJECTS  
Primary objects are:  
 - Window  
   - Properties of the Window object include position on the screen, the size of the window, etc.  
 - Document: Represents an HTML page  
   - Represents the currently loaded web page.  
   - Properties include Title, lastModified, and URL.  
   - Has methods  like write() and getElementById().  
   - Has events like load, click, and keypress.  
  
_All major web browsers_ support a common set of objects:  
- Document Object (note: major browsers implement this the same way)  
- All elements on the page are represented by objects  
  
Browsers perform these steps every time the URL is pointed to a valid document:  
1. Download the file containing all the code.  
2. Create models of the document, and the elements within it, and store it in memory.  
3. Launch a rendering engine to display the web page on the screen.  

JavaScript is interpreted by a subsystem of the browser:  
- JS is an _interpreted language_ meaning each line of code is executed one by one.
- The web browser calls a JS interpreter to convert JS commands into tasks the browser can perform.  

**Key takeaway** *[Duckett, pg.43]*  
> To make web pages interactive, you write code that uses the browser's model of the web page.  

HOW JAVASCRIPT, HTML, AND CSS FIT TOGETHER  
- HTML: Content layer  
- CSS: Presentation layer  
- JavaScript: Behavior layer  

_Keep code files separate as much as possible_  
This will make sure that partial page loads will still give the user some of the expected experience and information, rather than none.  

CREATING BASIC JAVASCRIPT AND LINKING IT TO AN HTML PAGE   
JavaScript is plaintext, so create a new file, name it with a `.js` extension and add JavaScript commands to it.  
Create a simple web page and add the following element:
  `<script src="file-name.js"></script>`  
When the browser reads this line it will stop to look for `file-name.js` in the current directory and try to execute it using the JavaScript interpreter before continuing on, rendering the next line of code.

**Note**: There is a very simple example of HTML + JavaScript usage, copied from Duckett, pgs.46-47, in the folder called chapter1_files.  

HOW TO USE OBJECTS AND METHODS  
`document` is an object that represents an entire page, as implemented in the web browser.  
The 'document' model has several methods and properties, aka members.  
The write() member is a method and accepts a string of text as the data parameters.  
  
  

# Remember To...   
[ ] Bookmark additional resources   
[ ] Present material as if to someone new to the industry   
[ ] Cite sources with links when directly quoting   


### Updated: 4-Mar-22