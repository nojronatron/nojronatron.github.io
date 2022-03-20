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

..

[Back to top](#notes-from-duckett-html-and-js-books)  

[Up one level](./README.md)  