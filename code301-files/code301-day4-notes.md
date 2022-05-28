# Day 4 My Brain Is Broken

## Warmup

Class 4 warm-up exercise: Find the bad React code.

export App is incorrect: `export default App;`  
counter: counter++ is bad to use in an arrow function should be `counter: counter +1`  
constructor needs to have a parameter list with 'props' in it.  
Return statement can only return a single object, use fragment elements or other containing parent element.  
Surround variables in JSX with braces `{}`  
When adding to what is in state, use `this.state.varName`.  
Component filenames should be Capitalized in the file system *and* when imported.  
Render function needs a return statement.  

## Code Challenge

Class03 Challenge: Challenge 6 - Snorlax Data with .filter  

snorlaxData is an object with a stats property that contains an array of properties.  
The stats[n].stat property is an object (KVP).

### Filter Details

You can just return the filter statement to get results from within a code block.  
A callback (aka Arrow Function) is inside the filter parameter list.  
The argument list for the callback is a parameter that retains each individual element within the array, upon each automatic iteration.  
Callback expression will be the *conditional statement* that is tested against each element within the array, and only positive (truthy) results are returned.

## Code Review

Abdulahi shared his code.  
App.this.state needs to hold: boolean showModal, string title, string imgurl, and string description.  
openModal arrow function takes three parameters (enough) to make a Beast, then it calls this.setState({params...}) to set the state of App including params: showModel to true, and all of the Beast properties to the parameters list, accordingly.  
Pass props: The selected beast properties should be passed to a new SelectedBeast component using props i.e. `<SelectedBeast title={this.state.title}... />`  
Access to PROPS is *automatic*.  
Every Component has to have a constructor if the Component needs to declare STATE properties.  
Abdulahi created a new SelectedBeast.js component and *built a return* that included `<Modal>` elements and just stuffed those Modal elements with `this.props.property` syntax.  
There is one more thing to pass down to selected beast: A reference to the functional logic to close the Modal.

*See the graphic* of the lab in the class repo.  

## Todays Code Challenge

Using 'Sort'.  
Videos and Demos are available from the assignment.  

`Array.prototype.sort()`  

Over-writes the input array with the sorted element version of the array.  

### Goofy Sort Behavior

- lower-case and upper-case alpha strings are sorted in their own buckets.  
- single-digit and multi-digit Numbers are sorted in their own buckets.  

### Resolving Goofy Sort Behavior

Add a helper function!

```javascript
months.sort((a,b) => {
  if (a.toLowerCase() < b.toLowerCase()) {
    return -1;
  }
  if (a.toLowerCase() > b.toLowerCase()) {
    return 1;
  }
  return;
});
```

### Advice

Start simple to get Code Challenges to pass.  
Once the challenge passes, then shoot for complexity.  
Remember that console.log() *can be called* at the top of a React render function!  
Object Deconstruction: `{ item1, item2, item3 }`  
Use object deconstruction in an import statement to grab multiple components from a larger, parent library like Bootstrap.  

## Todays Lab

Goals: Use Forms in React and Filter beasts by number of horns.  

### Create React Project steps

1. npx create-react-app name-of-project  
2. remove logo, reportwebvitals, setuptests, and app.tests  
3. remove the import statements that referenced these files  
4. remove code that utilizes those removed import statements  
5. change App.js from functional to class-based components  
6. add `class App extends React.Component {}` which declares this as a Class Component of React.  
7. add `export default App;`  
8. add a render function  
9. start adding JSX within the render return function to get the App to display something
10. import json data or make other imports as necessary  
11. download Bootstrap from terminal: `npm install react-bootstrap bootstrap`  
12. import the Bootstrap minified css file (no label needed)  
13. import the specific Bootstrap component(s) needed for this React Component  

*Note*: Always check the "bootstrap" version number in package.json otherwise it could break.  

### ListGroup

Import ListGroup to use it: `import ListGroup from 'react-bootstrap/ListGroup';`  

Within the render return block:  

- Add the `<ListGroup>` tag to the render return statement  

When using Map or other iterators in React, a key is required i.e. `data.map((num, idx) => {return <ListGroup.Item key={idx}>{num}</ListGroup.Item>)});`
Render the result of the Map (or iterator) by adding `{mapResult}` within the `<ListGroup>` open and close elements.  

### Forms in React

There are some tricky things when using Forms with React.  
Forms will be used often for the next few weeks.  

- React requires single-line elments like `<input>` to be self-closed  
- Add a form using `<form>` elements  
- When adding `<input>` elements add 'type=' and 'name=' attributes so that the input can be grabbed when submitted  
- Remember to add `<label>` elements to input items  
- When using a `<select>` element with `<options>`, apply a `<legend>` and add content that describes the name of the Selection list for the UI  
- For submitting data use button e.g. `<button type="submit"></button>`, where the submit type is highly recommended to avoid future issues  
- To get a handle on the submission, there are options (see below)  
- Instead of the label 'for' keyword, use 'htmlFor' to bind labels to textboxes by ID for accessibility.  

### Submission Handlers

Event handlers can be used, as in Code 201.
Here we will be using onSubmit.

1. Add `<form onSubmit={this.handleSubmit}>`  
2. Add the event handler `handleSubmit(){}` function  
3. Include 'submit default' settings change e.g. `handleSubmit = event => { event.preventDefault(); //other code; }`  
4. Use event.target.property.value  
5. Utilize React State to store the form elements properties (see below)

```javascript
// set up React State in the Component
constructor(props){
  super(props);
  this.state={
    name: '',
    howToSort: ''
  }
}
// also this.setState to an event handler to store the event.target.property.value
```

*NOTE*: DON'T SET SOMETHING IN STATE AND EXPECT TO BE ABLE TO USE IT IN A FUNCTION IMMEDIATELY  

### Filter Results and Display in React App UL

1. Store data in Component.state  
2. Use onChange event listener on the Select element  
3. Write an eventHandler e.g. `onChange={this.handleSelect}`  
4. Create handleSelect as an arrow function (see example code below)

```javascript
handleSelect = (event) => {
  let selected = event.target.value; 
  if(selected === 'even') {
    let newData = data.filter(num => num % 2 === 0);
    this.setState({filteredData: newData});
  } else if (selected==='odd') {
    let newData = data.filter(num => num % 2 !== 0);
    this.setState({filteredData: newData});    
  } else { // return original array 
    this.setState({filteredData: data});  
  } 
}  
```

*Note*: Event type that is attached to a Select element does NOT need to use the name property to ID which event is being targeted.  
*Note about State*: Perform calculations on the original data within a function, and then replace the state data entirely after the calculation, which will cause a re-render.  

### Bootstrap Forms

Bootstrap => HTML5  
Form.Group => FieldSet  
Form.Label => Label  
Form.Control => Input  
Form.Select => Select with child `<option>` element(s)  

Form.Group: Pass an attribute 'controlId="' and wrap the Form.Group around the Form items that need to be grouped together, and it will take care of all of the htmlFor and other bindings for you. Also, use the controlId name when capturing the event data e.g. `event.target.{controlId}.value`  

#### REVIEW event target property value

Form onSubmit creates an event object.  
The 'event' keyword is *free* for use by event handlers!  
The event.target.{property}.value is the property provided via the 'name=""' attributes within the form.  

## Class Feedback

The Lab: Class 03 definition says:

"""
Feature #1: Display a Modal
Why are we implementing this feature?
As a user, I want the image to be displayed in a larger size and with the description shown so that I can view the details of a single image.
What are we going to implement?
Given that a user wants to view the details of the image
When the user clicks on an individual image
Then the image should render larger on the screen with the description displayed
"""

Sheyna asserted the goals of the Display a Modal feature is:

"""(sic)
When a user clicks on an image it will load the modal and increment favorites for that beast.
"""

This is not helpful to the learning process. It makes me feel like I might not be able to meet the goals of the lesson when the goals are not clearly stated and in-sync between instruction and reference materials/definitions.  

## Morning Discussion

## References

Check out [InvisionApp](https://www.invisionapp.com)  
Remoting-in to Linux from Windows: Built-in "Windows Remote Desktop Connection" on the Windows side, "XRDP" on the Linux side. *[Allen Brazier]*  
