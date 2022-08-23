# Class Notes

Wednesday 13-Apr-2022

## Morning Warm-Up

Reviewed a simple Python file and it went well.  

## Code Challenge Review

1. get into the correct directory => javascript  
2. npm run get-challenge nn  
3. get to work!  

### Code Challenge 4

I chose the for loop after failing to get for...in to work properly.  
Sheyna chose for...in to solve this.  
The key takeaway seems to be pushing return value to a new array to get something back out.  

## Code Review

### Building and Launching

Use npm -i ?? when downloading React repo from a foreign source

### Imports

To pull-in data from a json file named data.json: `import data from './data.json';`
Use lowercase to assign data import file data.
Use PascalCase for the Components.  
Files that are '.js' extensions in the Imports section *do not need to specify* their extension.
File extensions other than '.js' *must* be specified.  
Component imports can just be their Capitalized name, without specifying '.js'.  

### Component State

Special function `this.setState()` allows changing data within that component instance.  
A Component's constructor is constantly listening for state changes, so using 'setState' in the constructor causes an infinite loop, and should be avoided.  

### Bootstrap Gridding

Use `import bootstrap/dist/css/bootstrap.min.css;` to add baseline styling.  
Also import Card and ListGroup if using those.  
Import `<row>` and `<col>` by using `import Row from react-boostrap/Row;`  
Add a `<Col>` to the Main.render code block and include a key attribute.  
Import Container using `import {Container} from react-boostrap/Container;`  
Apply a `<Container>` to surround the Component to render.  
Apply a child `<Row>` with some attributes (in Bootstrap-React) to set the grid.  
Each individual card is wrapped within a `<Col>`.  

- xs={1} the number of cards to appear on a small viewport.  
- sm={2} ...not as small.  
- md={3} ...medium sized.  
- lg={4} Four cards for large viewport size.  

Issues with card height inconsistencies:  

- Try the 'shuffle bootstrap' that will add various stylings.  

Multiple Imports can be done but it causes *all* of Bootstrap to download before extracting the ones you've selected within braces.  

Resource: [HackerThemes](https://hackerthemes.com/bootstrap-cheatsheet/)  

### NPM Install Note

Install multiple libraries at a time: `npm install component1 component2... ...`  

## Code Challenge For Today

Code Challenge: Class 03  
"Filter"  
An array method.  
Create a new array with all elements that 'pass a test' implemented by the provided function.  
Will return an empty array if nothing matches the filter argument.  

## Lab Material Discussion

"People of 301 Project" as a demo.  

Lab goals:  

- Add a bootstrap modal.  
- pass functional logic as props in React.  
- Pass State as props.  
- Send data from child component back to parent component.  

### State Problem Statement

Child Component has a click event that needs to change data in another Component, possibly in a completely different branch of the React DOM tree.  
Only a the Component itself can change its own state.  

#### Find Shared Ancestor

Add value and state infomation to the common ancestor Component.  
Add a handler in the common ancestor Component.  
When common ancestor render function fires, it needs to send info down the React data flow.  

### Prepare to Pass Data

In the common Parent:

1. Create a constructor and include the props parameter.  
2. Remember to add the super(props) statement.  
3. Within the super braces include: `this.state = { propertyName: value, };`  
4. Add an event handler function i.e. `evtHandler = () => { this.setState({ propertyName: this.state.propertyName + ' '}) } // string concatenation`  
5. Send the function to the child within the return statement by naming the function and setting it into the props of the Component attributes.  

In the child with the event:

1. Add the property to the Component as it is being pushed to the array in the render statement using the property name `this.props`.  
2. Add an onClick and call using props i.e. `onClick={this.props.addHearts}`.  

#### Arrow Functions

They inherit the context of where they are declared.  

### Bootstrap Modals

Modals are dialogs for notifications and user-directed messages.  
Self-contained within the Window in which they are launched.  

- Scrolling is disabled.  
- The rest of the window is greyed-out.  
- Clicking outside of the modal will close it.  
- They are *unmounted* when closed.  
- Can only use one at a time.  

#### Functional Components

Code401 teaches this, but in Code301 we will continue using Class Components.  
So *don't* just copy-and-paste from resources without looking at how it works.  

#### Create a Modal

[React Bootstrap Modals](react-bootstrap.github.io/components/modal/)  

Add a property to App.js to boolean show/hide a Modal.  
Import Modal from Bootstrap `import Modal from 'react-bootstrap/Modal';`  
Add a Modal component inside the App.render's return codeblock.  
Supply attributes `show={this.state.showProperty}` and `onHide={this.hideModelHandler}`.  
'show' and 'onHide' attributes are built-in to the Modal Component.  

There are buttons, footers, bodies, and other properties that can be set on a Modal.  

#### Pass the Source Data

Moving the data.js file into App.js forces you to:  

1. Import the file at the top of App.js
2. Pass the data down the chain in the render return statement.
3. Update the Child Component to re-use the data loop and Component rendering function to point to 'props' (because it is data passed-down the React tree).  

### Remember To

Before deploying a React app:

1. Ensure the Console output is clean of errors.  
2. Could be a good idea to also remove console.logs.  
3. ACP then wait for Netlify Tests to complete.  
4. Merge to main.  

## Resources

[EmojiFinder](emojifinder.com)  
