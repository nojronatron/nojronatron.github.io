# Day 7 Notes

## Jons Questions and Comments

What does 'contextual this' mean really (from the quiz)?  

Why didn't I use the advice to 'Think Like a React Developer' while creating Lab06 yesterday? This would have prevented me from over-utilizing 'state' in the App Component.  

## Warm-up

Is a Java warm-up but was skipped due to time limitations.  
class-07/warm-up.md

## Code Challenge 06

If a function *returns a new value* then the operation *must be returned*.  
Don't overthink these, keep it simple.  
When something is being passed-in to a function, the it is easy to simple concatenate something to the end.  

## Code Review

GitIgnore: In VS Code, when a file is in the filesystem view and is not tracked, it's name will be greyed out.  
In the case of City Explorer and LocationIQ, the 1st result (index '[0]') is *most of the time* the correct result.  
Environment Variables in React:  

- For React to recognize a global variable, it needs to be prefixed 'REACT_APP_'.  
- To assign the reference to a variable so it can be used in the Component, prefix the .env Variable Name with 'process.env.'

```javascript
let myApiKey = process.env.REACT_APP_CUSTOMNAME;
// or
let result = await axios.get('https://www.somedomain.net/v1/search.php?key=${process.env.REACT_APP_CUSTOMNAME}/etc');
```

React-Bootstrap: FormControl component is equivalent to html5 `<input>` element.  
Anonymous Inline Method: DO NOT use an anonymous function without a parameter, *even inside an onEvent type in-line event registration* will fire *every time the render occurs*.
In a React App when capturing user-inputs that will be submitted:  

- Set the user's input to state using `onChange(e)=>{setState{}}`  
- When `onSubmit` is called it shoudl interrogate this.state.property to get the inputted value(s).  

React State: You *cannot* access state properties *immediately* after setting them with a setState code-block.  
Bootstrap Form: When using a Submit type button, the `onSubmit={callback}` *must be defined in-line as a Form (property thing)*  
API Calls:  

- Generally speaking, don't make these from the front-end.  
- One of the common query parameters in the GET request is 'format' which is a *request to the API to send back data in that format* e.g. `&format=json`  

When to use State vs Props vs a local variable? It's all in where you are going to use it.

## Code Challenge 07

String Methods:

- Split: Takes a string apart, turning it into an array.  
- Join: Takes an array and puts it together into a string.  
- Slice: Insert and cut things in place (check this!).  
- Splice: (check the docs!).  

## Lab 07

### The Process

1. Use Express.js to create a Server.  
2. Add dotenv.  
3. Add cors.  
4. Deploy server to Heroku.  
5. Connect React App on Netlify on the backend at Heroku.  
6. Use classes to simplify bulk-importing incoming data.  

### Tools

Node: JS Runtime that is NOT in the browser.  
NPM: Node Package Manager for installing Node packages.  
Express.js: An NPM Package used to build a server.  
Json Formatter: Add-on for Chrome, adds 'raw' and 'parsed' views to the window.  

### Node Is A Runtime Environment

Node allows us to create a server.  
For Code301 we will be team 'server.js' endpoint.  

### Create Your Own Server

#### Overview

1. Create the GitHub Repo, add readme, choose MIT license.  
2. Clone to your development workstation.  
3. npm init: Creates a package.json file by following the prompts, and change entry point to 'server.js'.  
4. npm install `<pkg>`  
5. Create a `server.js` file.  
6. Copy `.gitignore` and `.eslintrc.json` from `./configs` to the root of the project.  
7. Open vscode and select 'workspace' (this project) and search 'color theme' to select something that speaks to you and says "this is the server-side project". This creates `.vscode` file, which *can* be added to `.gitignore`.  
8. When writing server files, add `'use strict';` and `console.log("hello world");` for simple proof-of-life.  
9. Add a `requires` section instead of import. This is a simple list of required *somethings*.  
10. Add a `use` section that will call the `requires` items.  
11. Add a `routes` section to define endpoints.  
12. Add an `errors` section for error handlers.  
13. Add a `listen` section that will start the server.  
14. Add a `.env` file and add `PORT=3001`
15. Add dotenv to project using `npm install dotenv`???  
16. Add local data (e.g. json file) with `let data =require('./{filepath}');`  
17. Create a class within server.js that has a constructor with a parameters list, and sets properties from the params. Now use new customObject with params to instantiate it. This will enable building a small, refined JSON file that can be stuffed into a response.  

#### Express.js

On the server, run `npm -i express`
Continue to configure the Express.js server:  

```javascript
'use strict';
console.log('ehlo');
const express = require('express'); // imports express.js
require('dotenv').config(); // grabs dotenv config file entries
const app = express(); // defines the app and executes it
const PORT = process.env.PORT || 3002; // usable because dotenv is installed and adds a fallback port if .env file cannot be read
app.listen(PORT, () => console.log('listening on ${PORT}')); // method built-in to Express to start the server takes a port and a callback method

// routes
// the slash route aka default route
app.get('/', (req, resp) => {
  resp.send('ehlo from app.get');
}) // 2 params: url, callback
app.get('/sayHello', (req, resp) => {
  resp.send(`Hello ${req.query.name}`);
})
app.get('*', (req, resp) => {
  resp.send('this is not the url you are looking for.');
}) // the catch-all method should always be last
app.get('/pet', (req, resp, next) => {
  try {
    let species = req.query.species;
    let result = data.find((item) => item.species === species); // works a lot like filter
    resp.send(result);
  }
  catch (error) {
    next(error);
  } // will catch most if not all errors within the try block
}) // a handle pets route

// error handling
app.us((err, ?))
```

#### Server Start or Stop

Stop: CTRL+C  
Start: npm start

Every time a change is made to the code, the server *must* be stopped nad started.  

*OR* just use NODEMON.  

#### NodeMon

Listens for code changes and restarts the server automatically.  

Install NodeMon globally with `npm i -g nodemon` to use it on all applications on my dev workstation.  

Then execute with `nodemon` at the root of the server project.  

#### Port Killer

To close an open (conflicting) port: `npm kill-port {num}`  

### Heroku

Deploy back-end servers here!  

1. Register at heroku.com  
2. Create a new App.  
3. New name has to be unique across all of heroku, try e.g. 'pets-api-301d84'  
4. Connect it to GitHub and authorize Heroku.  
5. Follow steps on [Heroku devcenter](devcenter.heroku.com/articles/git)  

### Axios and LocalEnv

1. Install axios: npm i axios  
1. Import axios to React Component: import Axios from './axios';  
1. Use 'async' and 'await' keywords when making Axios requests.  
1. Create a '.env' file and name the variable `REACT_APP_SERVER = http://localhost:3001`.  
1. *Always* remove the last slash when referencing URLs in React or Axios configs.  
1. In React code to leverage the server url: `let thingy = '${process.env.REACT_APP_SERVER}...'`  
1. *Always* add `.data` to get into the object response from an API.  

### CORS

Cross Origin Resource Sharing. For example, a server at domainA.com makes an XMLHttpRequest to domainB.com/data.json.  

Install CORS with `npm i cors`  
Require CORS in server.js: `const cors = require('cors');`  

## Lab Assignment 07

Custom Servers with Node and Express.  
Draw the WRRC with partner, timeboxed to 15 mins.  
Move to building the server, and getting weather data, given a city name.  
*Note*: For now get wx data by using *just the search query* without the Lat Lon parameters.  
Create a class 'Forecast' to capture date and description data.  
*Note*: NUKE THE SLASH when setting the server URL in any properties or environment variables.  
Trigger Deploy: Required after changing Env Vars in Heroku (and Netlify I'm sure).  
Aim to: Get the front-end and back-end correctly linked up.  

## One on One Meeting Today

Revelation: I need to do more planning before coding.  
How can Sheyna help me?

- Confirm my thinking that I need to target a specific job at a specific company to get the most out of the job-hunt and these classes.  
- I assume that my comfort level with javascript will improve.  

### What I Submitted in Canvas

My goals in this class include gaining proficiency in building interactive websites. I see this as an all-around useful skill to have, and learning React and interaction with APIs and Servers/Databases will only make it better and more valuable to my future.  

One area of concern is (again) Canvas. Code Fellows should make sure the assignment text and goals are clear and up-to-date. This is a minor nit-pick and is non-blocking day to day so far.  

Right now my top strength is my ability and willingness to help out my team members and make network connections. I don't know what clicked in my head but networking has become much easier in the last few weeks. Two months ago it was nearly impossible for me to reach out to strangers (or long-lost acquaintances) but I have since re-connected with two prior professional contacts, and reached out to several fellow students to get connected with them. The challenge for me now will be maintaining those links.  

I think maintaining my professional links is one of the areas where I need to improve on. Figure out a way to promote my maintenance of these links, beyond immediate needs.  

That's all for now.
