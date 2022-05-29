# Weds 27-Apr Morning Notes

## Preview

Need to finish Read-14 tonight to get points!  
Tomorrow is the assessment.  
Today is *prepare for assessment* day over most everything else (except the lab and then the reading).  

## Code Challenge Review

Will have a video prepped by end of week that will go through Challenges 13-15.  
Just submit the minimum requirement on these then turn them in and get back to Lab and assessment preparation.  

## Discussion

Includes() and Array.prototype.Every()

### Array.prototype.Every

Similar to Array.prototype.Includes() but for all items in the collection.  
If everything passes the conditional within an array: return true.  
Any other condition? Return *false*.  
So must be *an exact match for the entire array*.  
[Array.prototype.Every()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every)  

## Code Review

1. Always run `npm i` when you clone code from the internet/github.  
2. Ensure the `.env` file has the correct settings: FE - backend API URI; BE - DB Server connect string and server API port.  
3. *Seed* the db (assuming seed.js exists, and server/nodemon is shut down): `node seed.js`  
4. Startups: fe - `npm start`; be - `nodemon`  
5. To show a Modal: onClick calls a click handler that calls setState that changes Modal property ?`hideModal`? to false true.  
6. Submit vs Button: `type=submit` changes the event handling and could require `event.preventDefault();`  
7. Async functions in React should look like: `methodName = async (params) => { codeblock }`  
8. Use the 'spread operator' to add item(s) to an existing array `[...this.state.books, newArrItem]`. Creates a 'deep copy' of the data within the array, making a *new array* which is what React State wants.  
9. MongoDB adds a custom '_id' to every record that is added to it. If the server is configured to return the resulting json object, an '_id' will be included for the client to consume.  
10. Server-side routes can be named the same but *must have different REST verbs* so they are unique.  
11. Server must have `app.usee(express.jason());` in order to digest json body POST requests (because that's just how it is designed).  
12. Model: from mongoose; Schema: sent to Model so properties can be set to create an instance of the Model. This is for validation purposes i.e. 'required' fields etc.  
13. Add an error route on the server (see below) to handle error(next) calls.  
14. In React, when state is updated it causes a re-render event automatically.  
15. When passing a parameter from within a rendered React component, use an anonymous method `onClick={()=>thingyHandler(this.thing._id)}` to be sure the context of the currently selected item is sent to `thingyHandler()` *and* so `thingyHandler()` isn't executed on render.  
16. Path parameter: Different from a query search. Similar to `/books/?id=nnn`
17. Using a question mark implies a question placed to the server, whereas an :id implies the client knows what it is looking for.
18. When using `app.delete('/path/:id...')` the server code will be `let id=request.params.id;` because the id is a 'params' object from the URL. Params are used with a `:id` where 'id' becomes the parameter name, containing the string that follows in the URL. Remember 'id' is *implied* in the URL!  
19. When using a query string URL, use `let location = request.query.location;`  
20. PARAMS and QUERY are two separate objects within a REST call from client to server: Params object will be everything within the 'id' portion of the URL; Query object will be everything added in (wait for it) 'query parameters'.  
21. Model takes in the schema, and brings the functionality needed to work with the database records.  
22. When changing the DB name it will have to be edited in the '.env' file. The name of database is identified within the string like `...mongodb.net/my_database_name?retry...`. Username and Password might also have to be updated depending on which server you are connecting to.  
23. Console logs: Try to get into the habit of removing these completely, rather than just commenting them out.  

### Error Handling in Express

```js
function errorHandler (err, req, res, next) {
  if (res.headersSent) {
    return next(err)
  }
  res.status(500)
  res.render('error', { error: err});
}
// Note: error-handling middleware should be defined after
// the other app.use() and routes calls (see References)
```

### Demo: Deploying to Heroku

1. Create new Heroku project
2. Name it and select the region (US)
3. Add environment variables (if required): Config Vars => Key=DB_URL, Value={mongo_db_connection_string}
4. Find the [Heroku-cli instructions](devcenter.heroku.com/aritcles/git) to get it installed and configured *for an existing application*
5. On back-end: heroku login
6. Execute: `heroku git:remote -a {name-of-my-app}`
7. Perform `git status` to verify you are on main prior to the next step
8. Verify '.env' files are in .gitignore
9. ACP to *origin*
10. Create a PR to main in GH and merge it in
11. Change back to main branch and git pull from *origin*
12. Now push to heroku `git push heroku main`

### Demo: Deploying to Netlify

1. On your *dev environment* local: ACP all changes and push to origin
2. Login to Netlify
3. Import an existing project, providing it a name
4. Update variables with Heroku Server URL: key='REACT_APP_SERVER' and value='URL_TO_SERVER' and remember to *remove the final slash* from the URL_TO_SERVER
5. GitHub: Create a PR and stage it, waiting for the Netlify jobs to complete
6. GitHub: Accept and merge the PR to main. Netlify will build on main and display the page when done

## REST UPDATE

### Overview of Commands

```text
Crud    Mongoose              Rest
----    --------              ----
Create  .create()             POST
Read    .find()               GET
Update  .findByIdAndUpdate()  PUT
Delete  .findByIdAndDelete()  DELETE
```

### Details

#### Clear

Clear function: Opposite of seed => deletes everything from the DB.  
Utilizes `Mongoose.deleteMany();`
Not required for Lab (or exam, presumably).

#### PUT (Update)

Back End:

```js
app.put('/cats/:id', putCats);

async function putCats (req, res, next) {
  let id = request.params.id;
  // data about the updated cat will be in request.body
  try {
    // mongoose findByIdAndUpdate() takes 3 args:
    // ID of thing in DB; updated data; options{}
    // the options object is what differntiates a PUT from a PATCH
    // here we will use a PUT rather than PATCH
    let updatedCat = await Cat.findByIdAndUpdate(id, req.body, {new: true, overwrite: true});
    response.status(200).send(updatedCat);
  }
  catch(err) {
    next(err);
  }
}
```

Thunder Client:

1. Select PUT as the verb type
2. Add Json Content to the Body for an existing cat
3. Add the _id value to the URL to identify the item that will get updated (remember `/route/:id `)
4. Click Send
5. Do a GET /cats to get all cats and verify the properties of the cat._id are indeed updated

Front End:

Put in a method to update a cat.

```js
// remember: a Form or button will be necessary to start the update workflow from the UI
updateCat = async (updateCat) => {
  try{
    let url = `${SERVER}/cats/${updateCat._id}`;
    let updatedCat = await axios.put(url, catToUpdate);
    // we have an updated cat so replace the old version with new
    // before we push it into state
    let updatedCatArray = this.state.cats.map(existingCat => {
      return existingCat._id === catToUpdate._id
        ? updatedCat.data
        : existingCat;
    });
    this.setState({
      cats: updatedCatArray,
    })
  }
  catch (err){
    console.log('An error occurred: ', err.response.data);
  }
}
```

Inside the render method return():

```html
<>
  <Button onClick{()=>this.setState({showUpdateForm: true})}>Update</Button>
  { this.state.showUpdateForm && <Form here>} // use this to allow inserting a form
</>
```

Add a click handler for the Update button.
Recall that the passed-in methods and params will be `{this.Component.props}`
You will need to pre-load the existing values into the Form to avoid an update error on the DB site.
Remember that a textbox that is an empty string is falsey, so use a logical OR '||' to check for null then apply the existing value if true.

## Lab 13 Overview

Add 'Update' to the functionality.  
Add a Form to the FE to allow user to edit an existing item details.  
Ensure the page updates according to the response.  

## Exam Details

### Rules

1. Allowed to Google
2. Allowed open-book
3. Allowed to ask TA's about setup issues with deployments
4. Generally speaking, if everything is working and the system is deployed, you are on the right path to pass
5. Everyone sits at their own tables in Remo
6. 4-hour time limit from the time the materials are emailed in which to complete it
7. Deploy to *both* Heroku and Netlify
8. Class videos are *allowed*
9. NOT allowed to chat with neighbors

### Database To Use

Will be associated with a DB that is temporal and non-persistent (so don't shut it down).  
Can use the same Mongoose methods (create, find, etc).  
Use Thunder Client to get data *in* and *out* of the database, because the DB UI will not be available.  

### Exam Refs

Use the cats project demoed in classes as the go-to reference.  
Not tricky code - mostly like what we've written this week.  

## References

[Express error handling](https://expressjs.com/en/guide/error-handling.html)  

## Footer

If the *schema* changes on the MongoDB, the '__v' property should be incremented.
Write down any Q's about today's work and tomorrows exam, for review Thursday morning.  
