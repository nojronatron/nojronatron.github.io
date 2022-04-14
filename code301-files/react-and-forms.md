# Reading Notes

## React Docs - Forms

Reference: [Reactjs.org](https://reactjs.org/docs/forms.html)  

### Forms

Html5 forms natively store state and load a new page when submitted.  
For React this could be a problem (or it might be *exactly* what you want).  
To manage the submit event in React, use a technique called "Controlled Components".  

### Controlled Components

Mutable State in React is kept in the 'state' property.  
Input Form Elements that rely on React Components 'state' property are called Controlled Components.  
Use of an event handler that calls `this.setState({...})`  
React State will always drive the input value when using a Controlled Component.  
An event handler needs to be written for *every way the data could change*. A React Component must be used to capture all the resulting input state.  

### Controlled Components in React

textarea Tag: Uses a value attribute instead of its children.  
select Tag: Uses a value attribute on the root select tag instead of selected attribute on a specific option element.  

*Note*: Arrays can be passed into the value attribute.  

*Also Note*: Elements that use other APIs for their input (like input type=file) are handled differently in React.  

Multiple Inputs: Add a 'name' attribute to each element. The handler function will choose what to do based on event.target.name value.  

### React Forms Questions

What is a ‘Controlled Component’?

> Input elements that rely on Component State.

Should we wait to store the users responses from the form into state when they submit the form OR should we update the state with their responses as soon as they enter them? Why?

> Depends on the input type and the desired result in the UI. For example, it would be good to update the form when using the `<select>` and `<option>` elements so the user gets feedback upon slecting an item in the drop-down list. In another scenario using a textbox, UI feedback telling the user how complex their password is might be another reason to provide immediate feedback. React Components re-render when their state is changed.  

How do we target what the user is entering if we have an event handler on an input field?

> Use `event.target.name`

## The Ternary Operator

Operates like a compact IF statement.  
Like an if statement, some code will execute based on whether the test expression returns true or false.  
An If statement could consume 3 to 5 lines of code (or a lot more) depending ono what it is doing.  
The Turnary / Conditional Operator handles simple this-or-that decisions in a single line of (elegant and succinct) code.  

Example IF vs Ternary:

```javascript
// with an if code block, extra code is necessary.
if (true){
  return = "yes";
} else {
  return = "no";
}

// with a turnary statement, a single line is not too obscure
// and gets the job done
return (true) ? "yes" : "no";
```

### Turnary Nesting

Yes, this is possible.  

```javascript
return isIlluminated ? 'The room is now illuminated.' : isSmoky ? 'The room was burnt by fire, no electricity!' : 'Someone turned out the light!';
```

### Multiple Operations

Separate multiple result operations using a comma.  

### Turnary Reference

Brandon Morelli on Codeburst.io [The Conditional Operator Explained](https://codeburst.io/javascript-the-conditional-ternary-operator-explained-cac7218beeff)  

### Ternary Op Questions

Why would we use a ternary operator?

> Simple, elegant, single-line-of-code alternative to the IF statement and codeblock.  

Rewrite the following statement using a ternary statement:  

```javascript
if(x===y){
  console.log(true);
} else {
  console.log(false);
}

// turnary style
console.log((x===y) ? true : false);
```

## React-Bootstrap Forms  

Notes taken while reading through [react-bootstrap.github.io/forms/overview](https://react-bootstrap.github.io/forms/overview/)  

### Bootstrap Forms

`<FormControl>` Renders a bootstrap-styled form.  
`<FormGroup>` Wraps a form with spacing, adds a label, and includes validation state.  
`<FormGroup controlId...` and `<FormLabel>` should be used to ensure accessibility.  
Uncontrolled FormsControls values can be acceessed by attaching a 'ref' to it and calling `ReactDOM.findDOMNode(ref)` and use that to get the values.  
Attribute 'disabled' is a boolean that controls input capability and fades the input somewhat as a visual queue. Can also be applied to a `<fieldset>` to disable all controls.  

### Importing Forms

Add import statements at the top of your Component or HTML file to use them.

```javascript
import Form from 'react-bootstrap/Form';
```

*Note*: The above import statement also imports Form.Label.  

## Conditional Rendering

Reactjs documentation on [Conditional Rendering](https://reactjs.org/docs/conditional-rendering.html)  

### Generally Speaking

React Components can be built for specific functional purposes that only render depending on a current state.  
Buttons and other HTML elements can be stored in variables.  
*JSX is magic*  
Elements can be added conditionally - enclose the test conditional, add two amp's `&&` and then the html elements to render if true, within braces.  

*Remember This*: In javascript, the following behavior is expected:  

```javascript
(true && expression) == expression;
(false && expression) == false;
```

Use turnary/conditional statement to set text within elements, *or elements themselves*.  

*Note*: Components can be prevented from rendering. See the reference link for details on how to code this functionality.  

## Additional Resources

Brandon Morelli on CodeBurst [Ace your JS interview](https://codeburst.io/ace-your-javascript-interview-learn-algorithms-data-structures-dabb547fb385)  

## Footer

Go back to [Readme.md](../README.html)  
