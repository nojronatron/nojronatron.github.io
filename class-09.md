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

### Grouping Form Elements  

`<fieldset>`  
`<legend>`  

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

..

[Back to top](#notes-from-duckett-html-and-js-books)  

## JS Chapter 6 Events  

..

[Back to top](#notes-from-duckett-html-and-js-books)  

[Up one level](./README.md)  