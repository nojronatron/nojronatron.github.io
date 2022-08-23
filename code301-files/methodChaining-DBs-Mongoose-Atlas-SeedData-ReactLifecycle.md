# Class Notes 25-Apr

## Warm-up

Not today.  
Do it on my own time I guess.  

## Code Challenge

No review from CC10.  
CC11 should be *low priority* compared to the Lab.  

Intro to CC11:

- similar to Promises
- method chaining e.g. `let result = str.split('').join('-').toUpperCase();`
- can be written is waterfall format (see below)  
- when using method chaining, you are implying a Promise that the chained methods *will return something*  

```js
let result = str.split('')
  .joing('-')
  .toUpperCase();
```

## Lab 10 Review

Roger took one for the team [GitHub](https://github.com/RogerMReyes)  

Important Tidbits:

- Server `.env` file must include API Keys as well as the PORT for server to run on.
- Think about using Accordians for viewing search results or long lists.  
- Export: Can be used to export an entire Module, or just a function within a Module.  
- Object[key] returns the value stored in object Object at index or property 'key'.  
- Avoid using 'awaits' by using `.then( arrow => function)` because it causes js to WAIT for the prior command to complete before running the code block or expression that follows in parentheses. It is an *asynchronous* indicator.  
- The 301 final exam will *not* include the complex code seen in the 'code samples' from Lab10.  

## Lab 11 Can Of Books

1. Use starter code.  
2. Create db that retreives data using Mongo and Mongoose.  
3. Create a data model aka schema.  

### Databases

Are a place to store data.  
For this project, still using REST Verbs.  

### Relational vs Non-Relational

Non-relational for this project, to avoid having to teach a relational db system.  
Relational: Tables of data, organized by variable names as headers, and IDs used as record keys.  
Relational: Relationships can be made between tables for navigation aka referrers.  
Non-Relational: Just JSON data (documents), made up of unrelated data.  
JSON Documents: Not really structured. JSON objects can have all sorts of different properties within them.  

### ODM

ODM: Object Document Modeling?
Provides some structure to non-structured DBs.  
There are also ORM systems: Object Relational Mapping.  

### Mongoose

Used as an ODM.  
Schema: Diagram or template of what the data will look like.  
?? (there is more here that I missed)

### Why Not Use an RDBMS

Right now everything is javascript (FE, BE, and DB).  

### Mongo Cloud DB - Atlas

Database View: Shows overview, real time, metrics, collection, profiler, and more.  
Connect: Database => Connect button => driver: node.js v4.0+. Copy the line of code into a `.env` file.  

```md
mongodb+srv://rumseytoor:<password>@cluster0.0gxux.mongodb.net/myFirstDatabase?retryWrites=true&w=majority
```

Edit the IP Access (Allow) List by adding: (0.0.0.0/0 == ANY).

### Create a New Project Using MongoDB

1. Rough-in server.js on an Express server and make sure to add PORT in the `.env` file, and remember to include cors.  
2. Do 'proof-of-life' test with the Express server.  
3. Create some files: `touch seed.js clear.js`  
4. Add Mongoose to the project: `npm i mongoose`  
5. Add require statement to server.js: `const mongoose = require('mongoose');`  
6. Bring in a schema to server.js: `mkdir models touch models/cat.js`  
7. Bring in a schema to cat.js: See code block(s) below.  
8. Bring-in the schema to the server.js file: `const Cat = require('./models/cat.js');`  
9. Check the class repo for details on how Mongoose is implemented in server.js.  
10. Connect mongoose: `mongoose.connect(process.env.DB_URL);`. Add this to '.env' file with full URL from MongoDB Atlas configuration site.  
11. DB Access > Edit > Password > Edit PW > Autogenerate > Copy, then paste into '.env' and remove the angle brackets.  
12. Set up DB name (see class notes) and start nodemon and message in console should indicate Mongoose is active or failed.  
13. Check Mongo DB Atlas to see the new DB that is created in the cloud.  
14. Seed some start data.  

Mongo Cluster: The target to the DB instance in cloud.mongodb.

#### Bring In Mongoose and Create Model

```js
//  bring in mongoose
const mongoos = require('mongoose');
//  extract schema property from the mongoose object
const { Schema } = mongoose;  //  object deconstructor
//  create a cat schema defining how cat objects will be structured
const catSchema = new Schema({
  name: {type: String, required: true},
  color: {type: String, required: true},
  spayNeuter: {type: Boolean, required: true},
  location: {type: String, required: true},
});
//  define model to provide functionality and predefined schema to shape the data
const CatModel = mongoose.model('Cat', catSchema);

module.exports = CatModel;
```

*Note*: Property 'required' is ...optional.  

#### Seed Data

1. Edit 'seed.js' and include the codebock example (below)  
2. Execute 'seed.js' to load the data: `node seed.js`  
3. Create a Cats route and call a method called getCats (an async function): `app.get('/cats', getCats);` etc  
4. Add the async function getCats() with params (req, res, next) and include a try-catch(err).  
5. Make a call to DB from within getCats using await. `await Cat.find({}) // all documents`  
6. Send results with an http 200: `response.status(200).send(results);`  

```js
//  this file only needs to be run once
'use strict';
require('dotenv').config();
const mongoose = require('mongoose');
mongoose.connect(process.env.DB_URL); //  CONNECT
//  add the Cat model
const Cat = require('./models/Cat.js');
//  make this async
async function seed() {
  //  structure the same as Cat Schema from mongoose prototype method
  await Cat.create({
    //  having a Model and Schema allow using the .create() method
    name: 'Spike',
    color: 'orange tabby',
    spayNeuter: true,
    location: 'Seattle',
  }); //  Properties MUST be passed-in AS AN OBJECT using braces
}
seed();
mongoose.disconnect();  //  DISCONNECT or lose cash
```

### Front-end

Define a request to get the data from your custom API server.  
Define a method to render the results using the _id that Mongoose supplied *for free*: `<h1 key={cat._id}>{cat.name}></h1>`  
There needs to be a trigger (or event) that causes the call to the DB happens.

### Use the React Lifecycle

When this Component loads, trigger a get DB data and puts it into State, which updates the Render method.  

```js
//  when component loads it has all it needs
//  data will be put in state and rendered
componentDidMount() {
  this.getCats();
}
```

### Lab 11 Setup and TODOs

New Trello Board (clone so items can be checked-off and make it public).  
Week-long partner.  
Create a cooperative strategy to work on this lab (similar to 201 Final Project).  
Remember to *use starter code for both FE and BE*! GitHub "Use This Template" is the key.  
Wednesdays Code301 repo has a Bootstrap Carousel should be the guide for the FE.  
One of each per team: BE Repo, FE Repo, Trello Board. One person will own at least one of each of these. Use FORK to get locally up-to-date versions of other repos. Be sure to agree on who will update the Trello board.  
Definitely *do paired programming* throughout this project.  
Timebox lab work to 4 hours then submit whatever you have accomplished.  
If time permits after timebox and other assignments are completed *then* additional Lab work can happen.  
Make your partners *GitHub Collaborators* so there is a single-truth repo everyone will work on.  
Do *not* clone partners repo until end of the week.  

### CRUD

Functionality needed to have a fully functional database.  

Create: Add a new record to a DB, similar to 'POST'.  
Read: Similar to REST 'GET'.  
Update: Change a value within an existing DB record, similar to 'PUT' (update or replace) or 'PATCH' (modify).  
Delete: Remove an existing record from a DB, similar to 'DELETE'.  

## Jon TODOs

- Review Promises: They force an async behavior and return either 'response' or 'error'. A Promise is fulfilled and data is stuffed (as a parameter) via a Promise.resolve() function, otherwise Promise.reject(e) should be returned using a try-catch construct (handling a '.catch( arrow-func-to-handle-error-return )).  
- Review: https://masteringjs.io/tutorials/mongoose/create  
