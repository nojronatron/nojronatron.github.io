# Monday 18 Apr 2022

Componentization: Breaking down larger code into smaller components. Think of the way React is designed.

## Discussion

Canvas: Not a good alternative available at this point. Send feedback to Canvas.  
Readings: Try to get a basic, overview understanding, but don't worry about deep understanding on a single reading.  
1-on-1: Ask Sheyna how she can help me make the best of my experience in Code301.

## Portfolio Project Review

- Use VSCode Search: Helps to find places where components, variables, etc, are defined and used, in code that you did not write.
- Use Browser Developer Tools: Helps identify styles, console log output, etc.
- Use the Components Tab (Chrome Store) in DevTools: Identifies which Component is highlighted in the tabbed view, to help determine the source of the rendering.
- SCSS: Look for $variables that define styling, like color and background-color.
- Testing Styles: Within the Inspector, select the CSS element to change and just change it! The setting won't stick, but is a good trial-run method to test out ideas.
- Background Image: Find where the section (e.g. Header) is defined in CSS/SCSS, and implement a `background-image: url()`.

Working with other people's code is:

- A skill honed over time.
- Sometimes a bit of a scavenger hunt.

Content Agnostic: Design components so they will work with multiple types of content. "Generally specific" variable assignments and references.

_Note_: ALWAYS check your Node -v before utilizing create-react-app to scaffold a new project. Use `nvm use nn` to change to the connect Node version for the React version and scaffolding requirements.

## Code Challenge 6 Preview

Passing by value and passing by reference.  
Javascript is going to be 'weird' about this.

> When copying let variables, they copy the value as assigned.  
> When copying objects (arrays and object), a _reference_ is copied, _not the value_.  
> Shallow copy => a reference is copied to the source value.  
> Deep copy => values are copied to the new object instance.

Ways to push deep copy: map, for-each, for loop.
_Better_ way to deep copy: Use the spread operator `[...srcArr]`

### Lab 6 Preview

Make a request from our front-end to an API.

- Use Axios.
- Use parameters in a URL.
- Need an API key.
- Protect API key with referrers and .env files.
- Handle errors.
- Deploy to Netlify.

#### WRC

Web Request Response Cycle.  
FE: Our own computer. A user interface. Example: A website.  
BE: Some other computer. A service that responds to requests. Example: A database.  
An API helps another app 'run better'.  
Use an API to get data from a remote server, rather than a local file.

#### REST

GET: Ask for data and either get it or get an error.  
We will focus on GET this week.  
POST, DELETE, and PUT are also used in REST.  
Next week will add POST, DELETE, and PUT.

#### REST URL Anatomy

Base URL: The http address of the server that hosts the API.  
Endpoint: A keyword like 'search'.  
Query Strings: Start with a '?' followed by a key=value.  
Query String Concatenation: Performed with the `&` symbol.  
Multiple Query Strings: `?key=value&anotherKey=value`
Requests are Objects: Objects are made of key:value pairs.  
Requests are composed of 1 or more query strings concatenations.

#### Axios

- Built-in methods we can use to do the heavy lifting when making an API call.
- Promise is an enclosing object for PromiseResult.
- In Axios, PromiseResult will have a property 'data' which will hold the data.
- Note that REST API calls might _take some time to complete_.
- Keyword: 'async' tells javascript to allow time for the request response to come back. Place this keyword in the method definition.

##### Critical Keywords

- async: Preface the method that holds an Axios API call.
- await: Preface the actual axios.get() call.
- data property: This property in the response that holds the requested data. Use keyword 'result' to drill-down to the objects collection, e.g. `variableName.data.result`.

#### Star Wars API

swapi.dev
Single-response, or multiple response (collections) are possible.

#### Walk-thru

Import Axios so it can be used: import axios from 'axios';
Set the state, using an empty array.  
Create an event handler e.g.:

```javascript
// after the constructor (and state) and before render(){}
handleSubmit = (event) => {
  event.preventDefault();
  let swData = axios.get('https://swapi.dev.api.people/?page=1');
};
```

Assign an output variable in the render() function like:

```javascript
let swListItems = this.state.starWarsData.map((char, idx) => {
  return <li key={idx}>{char}</li>;
});
```

Create a UL element and pass-in `{swListItems}` to add the JSX 'li' items.

## NPM Review

npm -install: download dependencies.  
npm -i packageName: Adds packageName to the node_modules folder.  
npm start: run the project.

## API Keys

Do not share API keys with others - IT IS YOURS and is used like a billing register (for some APIs).  
my.locationiq.com (go get registered).  
Request an API Key via API Access Tokens.  
API Keys have properties that can allow/deny list via:

- Authorized HTTP Referrers: Paste-in URL to your website so that only requests from that website are allowed. '_localhost_' will allow any site request that contains 'localhost' in it.
- Authorized IP Addresses: Add a list of IP's (optional).

Update .gitignore to block '.env' (it will be greyed-out in VSCode).

When making an API call that requires an Access Token, using Axios, use a 'template literal' to insert the key value.

- Use `${}` for the API_KEY.
- Pass-in method `process.env.REACT_APP_CUSTOMNAME_API_KEY` inside the braces.
- Use `${}` for the 'search string'.
- Pass-in `this.state.city` inside the braces.
- Add `async` to the handleSubmit method label.

_Restart Node Server_ whenever you've updated a '.env' file otherwise the key will not be found, resulting in a http 401 error return.

### Update Env File

Provide a name to be able to refer to the API Key, like this:

`REACT_APP_CUSTOMNAME_API_KEY=pk.keykeykey` => This results in a variable name that matches the all-caps name above.

Remember to check for these conditions when there are errors:

- Referrers not allowing requests from particular URL/s?
- Has the server been restarted since referrers or API key change/s?

### Env Sample File

Similar to the '.env' file but will tell users how to enable _their own api key_ to test or use your code.

`REACT_APP_CUSTOMNAME_API_KEY=<your-key-here>`

### React Stuff

When collecting user input in a form with an in-line onChange event handler:

- Set State with the data that comes from the onChange eventHandler call.

When a Submit button is clicked on a form, the onSubmitEventHandler function needs to do two things:

1. Disable event.preventDefault()
2. GET the data from state (user-input stored earlier) then process it.
3. Determine whether to use the zero-th index item as the important object to store (depends on the data and the purpose of the app).

### Lab Details

Use the Trello board.  
Follow the cards for today's assignment.  
Complete each Card, item by item, as you do them.

### Error Handling

try-catch  
An error-handling if-else type statement.  
If the code within the try codeblock fails, the catch code block is executed.  
To capture the error message in the catch block, pass-in an argument to it and then drill-down with dot notation to get the detail of the error object that you want/need.  
Catch-block should not return the entire error to the user, rather a helpful message that means something to the user without giving any code or data secrets away.

### Setting Up Variables

Open Netlify.  
Open deployment settings.  
Add a Site Variable for the API_KEY.  
Redeploy required.

_Always_ edit environment variables well before you push a build.
