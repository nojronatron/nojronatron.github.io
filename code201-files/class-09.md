# Notes from Duckett HTML and JS Books

Notes taken from Ducketts HTML book:  
Chapter 7: “Forms” (p.144-175)  
Chapter 14: “Lists, Tables & Forms” (pp.330-357)  

Notes taken from Ducketts JS book:  
Chapter 6: “Events” (pp.243-292)  

[Back to index in readme](./README.md)  

## HTML Chapter 7 Forms  

### Forms Basics

Forms are used to capture user information.  
Many *controls* can participate with a Form: textual inputs, radio buttons, checkboxes and drop-down boxes, buttons, and a file-upload control.  
All controls within a form participate in capturing data that is to be processed by the website.  

### How Forms Work

Usually a SUBMIT button launches the processing code.
The web page could process (or pre-process) the user-input data, and could return a response to the user.  
Back-end server could participate in user-input data processing, and might even return a response.  
Data is captured into "Name: Value" pairs.  

### Form Structure

The `<form>` element surrounds other controls, creating the form, and the browser knows all these controls (and their data) are related.  

Form attributes: action; method; id.  
Text input: `<text> type="text"`: name, size (deprecated), maxlength.  
Password input: `<input> type="password"`: name, size/maxlength. Will cover text with asterisks.  
Text Area: `<textarea>`  
Radio Button: `<input> type="radio"`  
Checkbox: `<input> type="checkbox"`  
Drop Down List Box: `<select> name="name"` followed by `<option value="value">` representing selections the user can make.  

- Add the attribute `multiple="multiple"` for a multi-select drop-down list.  

File Input: `<input type="file">`  
Submit Button: `<submit type="submit">`  
Image Button: `<input type="image" src="" ...>`  

### Button and Hidden Controls

The Button element supports nesting elements within it.  
The 'type="hidden"' attribute will hide a form control (browser will not render it).  

### Labeling Form Controls

`<label>`

Use one for each form element, and bind them together either through nesting or using the `for=""` attribute.  
The `for=''` attribute binds the label with the input via the input elements `id=''` attribute.  

```html
<!-- nested -->
<label>First Name: <input type='text' name='firstName' /></label>

<!-- using for attribute -->
<label for='lastName'>Last Name:</label>
<input type='text' name='lastName' id='lastName' />
```

#### Best Practice for Placing Labels

Place the label above or to the Left of the input element:

- Text Input
- Text Areas
- Select Boxes  
- File Uploads  

Place the label to the right of these input elements:  

- Checkboxes  
- Radio Buttons  

### Grouping Form Elements  

`<fieldset>`  

- Groups sets of Form elements together.  
- Helpful especially with longer forms.  
- Use CSS to style the fieldset default look-and-feel e.g. change the border type and color, etc.  

`<legend>`  

- Immediately follows `<fieldset>`  
- Used to describe the form in its entirety.  
- Text appears as the form title when rendered.  

### HTML5 Form and Input Concepts  

Form Validation: Browser applies code to the form and if rules of input are not met a message can be displayed telling the user what is expected or needs to be corrected.  
Short-circuits user-input so it does not reach a back-end server before being validated.  

`<input type="date">`: New to HTML5, able to process a date input. Visual look and date style vary by browser.  

`<input type="email">` or `<input type="url">`: New to HTML5, allows entry of email and web addresses. Validate occurs within the browser via HTML5 support.  

`<input type="search">`: New to HTML5, adds rounded corners, and a "placeholder" attributes enables putting placeholder text into the search box. Older browsers treat this as a standard text input.

### Forms Example  

Duckett Pg.171-172 have example code of Form features and usage.  

[Back to top](#notes-from-duckett-html-and-js-books)  

## HTML Chapter 14 Lists Tables Forms  

### List Styles

Many CSS properties target Lists, Tables, and Forms.

List Type: `list-style-type`: decimal; decimal-leading-zero; lower-alpha; upper-alpha; lower-roman; uppoer-roman.  
Image Style: `list-style-image`: url("image-file-path"). Use `margin:` property to change whitespace between list items (usually vertically).  
Position: `list-style-position`: inside or outside. Positions the list-style-image inside (indented) or outside the block of text that follows. Think of outside as left-justified text with hanging icons, and inside as indented text with in-line icons.  
Short-hand List-Style: `list-style`: Consolidate all properties from type, image, and position, into a single css statement.  

### Table Styles

There are many table properties that can be set, customizing the look of table elements.  
Below is a list with important to-do items highlighted:  

- width: Table width.  
- *padding*: Around cells.
- *text-transform*: Converts text up upper-case.  
- letter-spacing & font-size: Applies to header cells.  
- border-top and border-bottom
- *text-align*: cell-level property aligns text left or right within the cell. *Numbers to the right* and *alpha to the left*.
- *background-color*: Apply this to header row/columns to make them stand out.  
- `:hover`: Highlights a table row when moust hovers over a cell.  

Also:  

- Use bold fonts for header rows/cols.
- Set tr.even{} and tr.odd{} selectors to alternate row shading.  

#### Additional Table Styling Properties

`empty-cells: [show | hide];`: Show, hide, and inherit.  
`border-spacing`: Controls gap in px between adjacent cells. Use Ypx and Xpx where Y-axis separation and X-axis separation need to be different.
`border-collapse: [collapse | separate];`: Border is collapsed into single border where applicable.  

### Styling Forms

Forms have a bad reputation: Nobody likes to fill them out.
As a developer it is your job to make the form more interesting (or less boring or annoying) for users.
Making forms look consistent across browsers is difficult, especially for `<select>` elements.  

Reference: Check out form consistency styling code at [Formalize Me](https://formalize.me/).  

#### Stylizing Text Inputs

Several CSS properties are commonly used to style inputs type=text:

- font-size
- color
- background-color
- border
- border-radius
- :focus Pseudo-class enables changing CSS properties to change appearance when input has focus (is being used)
- background-image will place an image within the input and should be carefully designed to help the user understand the purpose of the input element

#### Stylizing Submit Buttons

Input button element inherits styles applied to the parent form.
Other CSS styling properties commonly used are:

- color
- text-shadow
- border-bottom
- background-color: Can also utilize gradients to further stylize
- :hover pseudo-class enables changing the appearance of the button when the mouse passes over the button

#### Fieldsets and Legends

- width
- color Controls TEXT color within the fieldset or legend
- background-color
- border
- border-radius
- padding Adds space within the fieldset and leged elements

Tips of aligning form items:

- Place `<div>` elements with class CSS selectors between the form elements.
- Use `<span>` with a class CSS selector as a labelling mechaism *prior* a group of radio buttons.
  - The Label element is still required and needs to be wired-up via the `for=''` attribute.
  - Both span and label elements should have a class CSS selector set to the same style properties and settings.
- Set all `<input type='text'>` elements to the same width (if possible).
- Use `float` property to move elements horizontally to get them into alignment.
- `text-align` can be used to set the titles to the left or right, to set consistent spacing between the titles and the form controls.
- Apply styles to the `<div>` elements containing each row of the form to fix their widths and create vertical space between rows, and to ensure any buttons (e.g. `<button type='submit'>`) is aligned. Suggestion is to align it to the right-hand side of the form.

#### Cursor Styles

Commonly used values for the `cursor: n;` property:

- auto
- crosshair
- default
- pointer
- move
- text
- wait
- help
- url(path)

### Web Developer Tools

Duckett refers to a downloadable toolset for browsers, however modern browsers already have highly capable developer tools natively.
Use the developer tools to view:

- site structure
- css application
- javascript results

...and many more DOM and BOM properties and settings.

[Back to top](#notes-from-duckett-html-and-js-books)  

## JS Chapter 6 Events  

Preview:

- Actions or state changes in the DOM are raised as an 'event' type.
- An event type can be detected using a special asynchronous method.
- The async method calls an event handler method that executes code.

### Types of DOM Events

#### UI Events

UI Events occur when the user interacts with the browser user interface:

- load
- unload
- error
- resize
- scroll

#### Keyboard Events

Keyboard Events occur when keyboard keys are manipulated:

- keydown
- keyup
- keypress

#### Mouse Events

Mouse Events occur when the mouse input interacts with the UI (i.e. move or click):

- click
- dblclick
- mousedown
- mouseup
- mousemove
- mouseover
- mouseout

#### Focus Events

Focus Events occur when a pointer (cursor) moves over a UI element:

- focus or focusin: Element gains focus.
- blur or focusout: Element looses focus.

#### Form Events

Form Events occur when Form Elements are changed or are interacted with:

- input: Value has changed in `<input>`, `<textarea>`, or any element with a `contenteditable` attribute.
- change
- submit
- reset
- cut
- copy
- paste
- select

#### Mutation Events

Mutation Events occur when the Document Object Model is modified:

- DOMSubtreeModified: Change has been made to the document
- DOMNodeInserted
- DOMNodeRemoved
- DOMNodeInsertedIntoDocument
- DOMNodeRemovedFromDocument

### Three Steps To Triggering JS Code

1. Use DOM queries to get a reference to an element.
2. Configure which event to listen for.
3. Target a function to call when the event is raised.

#### Bind an Event to an Element

Use HTML Event Handlers.

- These are HTML element attributes.
- Do *not* use these as it is not considered bad practice.

Use DOM Event Handlers.

- Can attach a single function to a single event handler.
- Create a reference to the element to listen to which can then be bound to a function to execute.
- Call the function to execute using the syntax elementRef.on*event* = *function_to_execute*;

```javascript
let elementRef = getElementById('click-me-button'); //  get a ref to the element
elementRef.onclick = function_to_execute;           //  select action member to ref element then assign the function name to execute
```

You can do the following when defining DOM Event Handlers

1. Use a named function or anonymous function when the event fires.
2. Acquire a reference to the target element using `.getElementById('')`.
3. Omit the parentheses following the method name to ensure it does not run upon script load.

DOM Level 2 (yr.2000) Event Handlers
These are preferred and described in detail, below.

##### DOM Events and Keyword 'this'

Most browsers allow using the 'this' keyword as the context of the event is carried with the function call.  
*Note*: IE 8 and earlier select the wrong context when the keyword 'this' is used.

### DOM L2 Event Listeners

Newer style, considered *best practice*.  
Not supported in older browsers.  
Can trigger multiple functions per listener.  

Example DOM L2 Event Listener:

```javascript
let elName = document.getElementById('id_name');
elNameaddEventListener(`event`, functionName [, Boolean]);
```

Components of an event listener:

1. Acquire a ref to the element to bind the listener to.
2. Define the listener: 'element to target'.'addEventListener_method'('event-name', 'function-to-call-no-parens');

Example usage to check users input on a form *[Duckett, pg255]*:

```javascript
function checkUsername() {
  var elMsg = document.getElementById('feedback');
  if (this.value.length < 5) {
    elMsg.textContent = 'Username must be 5 characters or more.';
  } else {
    elMsg.textContent = '';
  }
}

var elUsername = document.getElementById('username');
elUserName.addEventListener('blur', checkUsername, false);
```

*Note*: The last parameter of .addEventListener, "false" is optional and refers to a state called "capture" which will be addressed later.  
*Also Note*: Prefix keyword 'on' is not used in L2 DOM Event Listeners.  
*Key Detail*: Use DOM "Level 2" Event Listeners, not the previous methods.  

### Remove An Event Listener

Built-in member '.removeEventListener()' is used to accomplish this.

### Event Listeners, Parameters, and Anonymous Functions

When binding a function to an event listener, parentheses are not allowed, otherwise the called function is executed immediately.  
An anonymous function allows passing arguments to an event handler:

```javascript
/*  replaces elUserName.addEventListener('blur', checkUsername, false); */
el.addEventListener('blur', function() {
  checkUsername(5);
}, false);
```

*Key Concepts*:

1. Event handlers can take zero, or many parmeters - they are just a regular function after all.
2. Binding an event listener to an element does not allow adding parameters.
3. Add an anonymous function, and include the necessary parameters within the anonymous function so they get passed to the event handler when the event listener fires.

Reminder: How to build an anonymous function that supplies parameters to, and calls another function:

```javascript
/*  a named function can be called and can take parmeters */
function FooBar(param1, param2) {
  return `${param1} to the ${param2}`;
}
/*  anonymous functions have no name and are called immediately  */
let foo = function() {
  let param1 = 'foo';
  let param2 = 'bar';
  return FooBar(param1, param2);
};
/*  call and return the result  */
console.log(foo());
```

To implement this with event handlers *[Duckett, pg257]*:

```javascript
/* global variables */
let elUsername = document.getElementById('username');
let elMsg = document.getElementById('feedback');

/* create the function to be called when the event handler fires */
function checkUsername(minLength){
  if (elUsername.value.length < minLength) {
    //  Set the error message
    elMsg.textContent = 'Username must be ' + minLength + ' characters or more';
  } else {
    elMsg.innerHTML = '';
  }
}

/* create an event listener with an anonymous function that passes params to checkUsername */
elUsername.addEventListener('blur', function() {
  checkUsername(5);
}, false);
```

#### IE 8 and Event Listeners

*not supported*  
Use 'attachEvent()' instead.  
Work-around: Test to see if `.addEventListener` is true or false, then take approprate action.  
Example from *[Duckett, pg258]*  

```javascript
if (el.addEventListener){
  // codeblock using el.addEventListener like before
  } else {
    el.attachEvent('onblur', function() {
      checkUsername(5);
    });
  }
```

### Event Flow

HTML element nesting effects how events flow.  
Event flow is the Bubbling (up from element to Document) or Capturing (down from Document) of events as seen by elements (bubling) and by listeners (capturing).  
Firing an event on a child element also fires an event on the parent element(s) all the way up to the DOM.  
Event Listeners can be bound to DOM *and* the Window object, *in addition* to the specific element declared in its binding statement.  
Event Flow matters when handlers bound to an element *and one of its ancestors*.  
The '.addEventListener()' method allows configuring of the phase the eventListener will respond to: Capturing or Bubbling:  

- Seen earlier as 'Event Flow Boolean'.  
- true: Trigger events during Capturing Phase of event flow => From the Document level to the Target Element.  
- false: Trigger events during the Bubbling Phase of event flow => From the Target Element to the Document level.  

The event object has properties that describe when and where the event was raised:  

- target (srcElement in IE8): The targeted element in the binding.  
- type: The event type that was raised.  
- cancelable (not in IE8): Enables canceling the default element behavior.  

Event object methods:

- preventDefault() (returnValue in IE8): Cancels default event behvior if cancelable is true.  
- stopPropagation() (cancelBubble in IE8): Stops event from bubbling / capturing further down the event flow.  

Event Listeners can get a reference to the event object in the following ways, with or without parameters:  

```javascript
// No parmeters
function foo(e) {
  var targetOfEvent = e.target; // gets target of event
}
var el = document.getElementById('el_id');
el.addEventListener('blur', foo, false); // call foo() and block bubbling
}
```

```javascript
// With parameters
function foo(e, param1) {
  var targetOfEvent = e.target; // gets target of event
}
var el = document.getElementById('el_id');
el.addEventListener('blur', function(e) { // define anonymous function to execute
  foo(e, 5);  // call function foo with parameter of 'e' and 5
}, false);  // execute anonymous function with args and block bubbling
```

### Event Object Differences in IE

Internet Explorer 5 through 8 use a slightly different model.  
Event object is not automatically passed around, instead a reference to 'window.event' must be initialized, then the properties can be accessed to use the event payload.  
See Duckett, Pg. 264 for examples.  

### Event Delegation

Event flows allows listening for events on parent elements.  

- Reduces the number of listeners you need to create.  
- Reduces memory consumption.  

Place event handlers on a containing element.
Use 'event.target' property to find child that event happened on.  
For example, place the event listener on the `<ul>` element rather than each `<li>` item!
This is called Event Delegation.

Benefits of Event Delegation:

- New DOM elements inherit the parent in their event bubbling path.  
- IE 8 doesn't support the 'this' keyword. With delegation the event.target is explicitly filtered.  
- Write fewer functions in JS and still get desired effects.  

### Changing Default Behavior

preventDefault (returnValue in IE8): Blocks default behavior of some elements that would normally refresh a page or open a new one after firing a click event (like a Form).  
stopPropagation (cancelBubble in IE8): Once an event is handled in code, stopPropagation() should be called so no other elements have to respond to the event bubbling.  
Optional (popular, not necessarily the best choice): 'return false;'. This tells the executing code to exit the current function, which effectively stops bubbling *and* default behavior, but it also forces the code to jump to a parent function, which might not be the best path for code execution at that time.  

### Using Event Delegation

Step by step instructions (1-13) are listed in Duckett pg.268.
Example HTML and JavaScript captured on Duckett pg.269.

*Use the above as a guide to implement Event Delegation*.

### Which Element Did An Event Occur On

First look to the 'target' property of the event object.
Optionally, use keyword 'this', which points to the event.target property automatically, but only works when no parameters are passed.  
When parameters must be passed, pass them via an anonymous method and also pass a reference to the event.target element as an additional element. This was the event.target context can still be acquired at the called method.  

### Different Types of Events

Events are defined in: W3C DOM spec; HTML5 spec; Browser Object Models' specs.  

#### W3C DOM Events

DOM events provide information about the source element of the event, keyboard key info, and mouse location and state info.  

#### HTML5 Events

Browsers are programmed to respond to HTML5 specified events.

- Form submission events: submit; input; change.  
- Some newer events that might not have wide browser support: readystatechange; DOMContentLoaded; hashchange.  

#### BOM Events

The Browser Object Model is also supported by the browsers.  
BOM events are usualy events that are not yet covered by the W3C specifications.  
Touch-screen events are relatively new and might be in BOM rather than HTML5 event specs:  

- touchstart
- touchend
- touchmove
- orientationchange

*Note*: The newer to event (within whichever model), the less likely all browsers will support it. Try to implement back-up functions for unsupported event types so your website does not break.  

#### User Interface Events

Interaction with the browser window will fire UI events:

- load: Web page has finished loading.  
- unload: New page has been requested and current page is removed.  
- error: JS errors on non-existent assets.  
- resize: Browser window has resized.  
- scroll: Entire page or page segment scrolls by the user/mouse/keyboard.  

Utilize the 'load' event on early-running scripts to trigger things like:  

- cursor placement into a form input element.  
- animation or other "you made it" type of messages or interactive messages or activities.  

Listen for these events by attaching an event handler method to the Window model.  

*Note*: Waiting to run the script at the bottom of the HTML might result in unintended concequences like moving a user's cursor after they've already filled out a form element or two.  

### Focus and Blue Events

Gaining focus is when a cursor is over the area of another element on the web page.
Focus-oriented events fire when the cursor enters or leaves the element's view.  

Event - Trigger - Flow  
focus: Element gains focus. Capture flow.  
blur: Element loses focus. Capture flow.  
focusin: Element gains focus (except maybe FF). Bubble and Capture flow.  
focusout: Element loses focus (except maybe FF). Bubble and Capture flow.  

focus and blur are good events to add UI features like ToolTips or other hints.
focus and blur are also good events to add or remove color, shadow, or other effects to UI elements.  
focus and blur can also be used to fire 'validation code' in the background so the user gets quick feedback on whether they need to correct form entries prior to hitting 'submit'.  

### Mouse Events Revisited

These fire upon mouse movements and clicks.

click: Fires when primary mouse button is clicked. Source is the element that has focus. A screen tap is equivalent to a Click event.  
dblclick: Two rapid-succession clicks. Single event. Otherwise same as click.  
mousedown: Any mouse button is depressed. touchstart is equivalent.  
mouseup: Any mouse button is released. touchend is equivalent.  
mouseover: Mouse cursor enters the border of an element. Same in touch.  
mouseout: Mouse cursor leaves the perimeter of an element. Same in touch.  
mousemove: Fires repeatedly when cursor moves near an element. Same in touch.  

*Note*: Preferrable to use ':hover' pseudo-class instead of mouseover or mouseout to style elements on those actions.  

### Where Events Occur

Screen: Cursor position values within the *screen* are stored in properties screenX and screenY.  
Page: Cursor position values within the entire *page* are stored in properties pageX and pageY.  
Client: Cursor position values within the *viewport* are stored in properties clientX and clientY.  

*Note*: Check out the JavaScript example leveraging screenx and screeny in *[Duckett, pg.279]*.  

### Keyboard Events Revisited

input: When `<input>` or `<textarea>` elements are changed this event is fired. Use 'keydown' as a fallback for older browsers.  
keydown: Fired when a key is depressed. Multiple fires will occur when key is held down.  
keypress: Only fires when the user is typing a key that would result in text being added to an input. Arrow keys etc are not included.  
keyup: Fires when a keyboard key is released, but only *after* it is released fully.  

There is a hierarchy with the properties beginning with 'key':

1. keydown fires 1st.
2. then keypress if user pressed a key that adds content to the page.  
3. keyup when the user releases the key that was pressed.  

#### Which Key Was Pressed?

ASCII keycodes are used under the hood to encode and decode keypress values.  
Event property keyCode is included when the firing event is from keydown or keypress.  
'keyCode' returns an ASCII code representing the key value that was pressed.  
Use the String method 'String.fromCharCode(event.keyCode)' to get the key value.  

### Form Events Revisited

Three events are generated from Forms:

- submit: Happens when the Form is submitted. Attached to the Form element.  
- change: Generated when a selection box is changed, or a radio button or checkbox are clicked. *Preferred over click event detection* because most elements can be operated by keyboard input only, in addtion to mouse actions.  
- input: Occurs when an `<input>` or `<textarea>` element are changed.  

*[Duckett, Pg.283]* has a full page example of code showing how to use Form Events.  

### Mutation Events and Observers

A structural change in the DOM generates Mutation Events. They include:

- DOMNode Inserted  
- DOMNodeRemoved  
- DOMSubtreeModified  
- DOMNodeInsertedIntoDocument  
- DOMNodeRemovedFromDocument  

Relying on mutation events can cause your code to operate slowly when it is making many changes to teh DOM.
*Mutation Observers* wait until the script has completed before firing the Mutation Event(s).
*Note*: Browser support for Mutation Events might be lacking, check the latest MDN Documentation for up-to-date info.  
*[Duckett, Pg.285]* has a full page example of code showing how to use Mutation Events.  

### HTML5 Events Revisited

Three new HTML5 events have been implemented:

DOMContentLoaded: Event generated when the DOM Tree forms. Event could be attached to Window or Document object. Timing issues between page load and script execution should be mostly resolved by this.  
hashchange: If URL changes (non-refresh) this event is generated. This event's handler is attached to the Window object with properties of 'oldurl' and 'newurl'.  
beforeunload: Generated and attached to Window object, prior to a page being unloaded. Only use to help the user prior to page unloading, such as "are you sure" type of interactions like leaving the site.  

[Back to top](#notes-from-duckett-html-and-js-books)  

[Up one level](./README.md)