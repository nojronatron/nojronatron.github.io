# Day 8 Notes

## Thoughts and Contemplations

## Warm-Up

Skipped for today due to workload.

## Code Challenges

### CC7 Challenge 6

in class solution included:

recipe.ingredients.forEach((ingredient) => {
  let withoutAmount = ingredient.slice(ingredient.indexOf(' ') + 1);
  let withoutUnits = withoutAmount.slice(withoutAmount.indexOf(' ') + 1);
  results.push(withoutUnits);
});

the indexOf(' ') returns the idx of the space character

### Today's Code Challenge

RegEx: Regular Expression  
Not very intuitive.  
Variety of uses but gist is:  

- Website form: How to verify user entered a phone number?  

Pattern is used to compare if all or part of a string matches the patterns.  
RegEx is very literal, so lower-case vs upper-case matters, etc.  

#### Regex Methods

Returns true or false: `regex.test(str)`  
Returns an array if there are matches, or null: `str.match(regex)`  
Returns a *new string* with the matches replaced by the provided replacement: `str.replace(regex, replacement)`  

#### Regex Flags

Flags are used

Global: 'g' => Don't return after first match, run against entire input.  
Multi Line: 'm' => Single-line test.  
Case *in*sensitive: 'i' => Does *not* pay attention to case.  

#### RegEx Examples

Sheyna used ReplIt and regex101, both will be linked to the class repo.  

1. Create a variable to represent the *pattern* `let regex = /pattern/;`  
2. Assign the regex output to a variable: `let result = regex.test('test string');`  

#### RegEx Returns

If regex does *not* find any matches it returns null.  
Use a Logical-Or to evaluate a null return to an empty array instead: `var result = str.match(regex) || [];`  

#### Terminology

Greedy: Selects one or more matches between one and unlimited times as many times as possible, giving back as needed.  

## Code Review

Abdulahi strikes again!  

Notes:

Remember to add the variable `REACT_APP_SERVER=http://localhost:3001` to the FE .env.  
When cloning other code, add a .env file and set the server listening port and restart the server.  
Error Handling: Some types of error conditions will not trigger a try-catch (probably because it is happening outside of it).  
Require the dotenv file with `require('dotenv').config()`.  
dotenv is necessary to 'pick up' stored variables from a flat file.  
If server is unable to access dotenv file or the PORT value within it, then the server will be on the 'alternate port' e.g. 3002.  
Express.js is a node-based Server using javascript.  
CORS must be requied so the server can share with multiple computers.  
CORS is 'middleware'.  
Putting multiple API calls within a single try-catch within a single method is frowned upon, instead:  

1. Move separate calls to separate try-catch blocks.  
2. Move the try-catch blocks to their own functions.  

Concatenate the URL.  
Get the Path to the image.  
Make the request for the weather data.  

## Lab08

Axios, CORS, Express exercise!  
Use our existing front-end application.  
Create a backend that will find items on the internet and then send them back to the requesting front-end client.  

Steps

1. Create a new back-end server.  

### Create a New Server

Different this time.  

1. Make a new directory to hold the back-end code and name it closely to the front-end project.
2. Create needed files using touch: server.js; .env; .env.sample  
3. Copy from ../configs/: .eslintrc.json; .gitignore  
4. Initialize a node project with a YES (to avoid the menu questions): `npm init -y`. Verify that the resulting package.json file *is correct* especially "start" and "main", so that nodemon will work.  
5. Install nodemon if not already installed globally.  
6. Install other dependent projects: `npm i express cores dotenv axios`. Yes, axios too!  
7. Update vsCode workspace color theme so it is identifiably different than the front-end project.  
8. Implement the server in server.js: use strict; requires; use; routes; classes; errors; listeners
9. Edit the '.env' file with PORT=3001  
10. Get required API key(s) and review API Documents

#### To Talk To An API

API Key.  
End Point URL and the VERB i.e. 'GET'.  
The parameters (required, optional, and exclusive) to make a valid request.  

#### Requires

```javascript
require('dotenv').config();
const express = require('express');
const cors = require('cors');
const axios = required('axios');
```

#### Instantiate Required Dependencies

```javascript
const app = express();  //   express server
```

#### Use

```javascript
app.use(cors());
```

#### Configure

```javascript
const PORT = process.env.PORT || 3002;
```

#### Routes

```javascript
//  root route
app.get('/', (req, res) => {
  res.status(200).send('Ehlo owrld.');
});

//  a route to handle searching for photos
app.get('/photos', (req, res) => {
  //  see the class repo for the notes
  //  basically: process the request => send an axios => 
  //    ...process axios reply => format data into a class instance => 
  //    ...use res.status(nnn).send(processed_data)
});

//  catch-all route MUST BE LAST
app.get('*', (req, res) => {
  res.status(404).send('Nothing here');
});
```

#### Listeners

```javascript
app.listen(PORT, () => console.log(`Listening on port: ${PORT}`));
```

#### Error Handling

```javascript
app.use((err, req, res, next) => {
  console.log(err.message);
  res.status(500).send(error.message);
});
```

#### Classes

```javascript
//  server-side
class Photo {
  constructor(pic) {
    this.src = pic.urls.regular;
    this.alt = pic.alt_description;
    this.artist = pic.user.name;
  }
}
```

### Thunderclient

A VSCode extension.  
Install it GLOBALLY.  
Use it to make REST API calls.  

### Create, Configure Heroku Project

1. Register with heroku.com.  
2. Create a new REPO in GitHub and follow the 'already exists' steps meaning (just create w/o adding anything in the GH Repo setup screen).  
3. Git => Be on 'main' with all merges completed then: remote add ...; ACP to the new repo.  
4. In Heroku, create a new app, named (something appropriate for the project).  
5. Login from the terminal `heroku login` (it helps to already be logged in to the website on the same workstation).  
6. Find the "add an existing project" instructions and follow them to publish the *back-end server* app to Heroku, pointing it to the newly created and ACP'd GitHub. [See](https://devcenter.heroku.com/articles/git).  
7. *Publish* ACPs should be `git push heroku main`  
8. Add environment variables for Server location: KVP for the API (take out the slash!), port is not necessary.  
9. Add environment variables for APIKey, allowing server to call remote API.  
10. Code changes will require a `git push heroku main`.  

### Request Workflow

FE makes axios call to BE Server.  
BE Server captures call, takes data, makes an Axios call to remote API.  
Remote API response is transformed by our BE Server then responds to FE.  
FE server processes response to display results.  

## Lab 08 Discussion

Use next section of Trello Board.  
Make two calls to two APIs, to get real data from WeatherBit.io API.  

## References

[RegEx 101](https://regex101.com) - Use ECMA Script setting  
MDN [RegEx in javscript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)  
Unsplash [API](https://www.unsplash.com/)  
