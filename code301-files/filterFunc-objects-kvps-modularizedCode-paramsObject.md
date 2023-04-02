# Day 9 Notes

## Thoughts and Contemplations

Chaining methods. Works with String.prototype and others. `String.prototype.split().slice(number).join();`

When you see `.then()` this is a hint that chaining methods are in-use (or needed).

Consider how you organize your variables and data in your projects.

Come up with componentized structures that are _very simple_, and keep variables close to where they are needed.

## Code Challenges

### CC8 Number 6

When using .filter(), the right-side of the arrow function needs to have a comparison statement that returns boolean.

When an arrow function returns 'true' to a .filter() method, the currently selected item is taken.

Conversely, when 'false' is returned, the currently selected item is ignored.

### Code Challenge 9 - Objects

Object literal: `let fido = { species: 'dog', ...};`

To KVP an object literal: `let entries = Object.entries(fido);`

To extract the Keys: `let keys = Object.keys(fido);`

To extract the Values: `let values = Object.values(fido);`

## Lab 09

### Plan

Refactor your code.

Finish features from previous.

Modularize your server code.

Follow the variable names the Trello Cards suggest.

### WRRC and Modularization

All code currently in server.js.

As more features get added, modularize the functionality and processing into separate js files: movies.js; weather.js.

### Steps to Modularize

"I want to move processing from the '/photos' route to a separate file to clean up my server code.'

Route definitions rely on callback functions in-line. So why not just call a separate file from the route and move all the processing code there?

Processing code _is the second parameter_ to the route definition.

Write the function like:

```javascript
async function getPhotos(req, res, next) {
  //  this is no longer an arrow function
  //  all the same code is as before
}
```

Modularlized code (moved into a different js file) must be imported:

```javascript
const getPhotos = require('./photos.js');
```

Modularized code _must have an export statement_.

In the new JS file with the moved code you must:

- export using `module.exports = getPhotos;`
- import dependencies such as axios.
- move any Class definitions to the new JS file.
- remove any unneeded requires from the file from server.js

## Error Handling

There are a few different ways to write them, one example: `Promise.resolve().then(()=>{throw new error.message);}).catch(next);`

To avoid using try-catch blocks, try chaining:

```javascript
//  inside a function with req and res in the parameters list
axios
  .get(url)
  .then((PhotoResults) =>
    PhotoResults.data.results.map((pic) => new Photo(pic))
  )
  .then((grommedPhotos) => res.status(200).send(groomedPhotos))
  .catch((err) => console.error(err));
```

## Code Review Lab08

- Various environments will use different '.env' files so sticking with the given naming scheme will be important.
- AXIOS takes a response and assembles a large object with many parameters. The data returned by the server is in the 'data' parameter of the Axios return.
- An API should only return enough data that the client needs, and nothing else (except error messages). This is where API documentation is critical, so the client can understand what data an API endpoint will return.
- Some APIs have a SEARCH endpoint that will help get the target entity from the API.

### Lab09 Final Comments

- Use Trello Cards, refactor if possible, get weather and movie modules created, make substantial progress on entire city-explorer project.
- DO NOT worry about the error chaining notation, not a requirement.
- Weather component should be named something like WeatherDay.
- Ask questions if you get stuck.
- If behind, submit multiple TA tickets to get help to get caught up.
- Code-review should be quick (10 mins tops).

### Using a Params Object

```javascript
let url = "https://api.unsplash.com/search?";
let params = {
  client_id: clientId,
  query: searchQuery
}
axios.get(url, { params })...
```

See the class repo for the full example.

## Footer

Return to [root readme](../README.html)
