# Tuesday 26-Apr Morning Notes

## Challenge Review

```js
//  Sheyna's code
const divisibleByFiveTwoToThePower = (input) => {
  return input
    .map(row => {
    return row
      .filter(cell => typeof cell === 'number' &&
        cell % 5 === 0)
        .map(num => Math.pow(2, num));
  });
}
```

## Code Challenge for Today

Do your best but ensure Lab and Assessment are *top priority*.  
RegEx part 2 today.  
Utilize regex101.com:  

1. Change 'flavor' to javascript/ECMAScript  
2. Make sure 'Quick Reference' is visible  
3. Remember to pay attention to the flags (global, multi-line, etc)  

### The Pipe Symbol

Logical OR

```js
let pattern = /^(206)|^\(206\)/;
let noParens = '206-123-4567';
let withParens = '(206) 123-4567;
//  returns 206 or (206)
```

## Lab Assignments

Liesl, Darius, and Gina shared their team repos.
When React returns a 'Key error' then look for a Map function that is rendering the component and ensure map(item, idx) is being used and applied properly: `key={item._id}`  
Note that Mongo applies its own index to every record, so that should be used (as a property) instead of the Array id of the state items themselves.  
To Do Routes:

1. Between `<switch>` statements will determine the target page that will be rendered.  
2. Also use `<Link to='/path'>` so users have something to click on.  

## Lab Work Today

Add CRUD methods, REST methods, and Mongoose methods.  

CRUD, Mongoose, and REST

Create => .create() => Post
Read => .find() =>  Get
Update
Delete => .findByIdAndDelete()  =>  Delete

### POST

Use App.Post: `app.post('/route', postRouteName);`  
The Request parameter will now have data in it, rather than just a URL with keywords and characters.  
Use ThunderClient to select POST verb to test POST operations.  

### DELETE

Use App.delete: `app.delete('/cats/:id', deleteCats);`  
Using `:id` allows extracting the path parameter.  

```js
// server-side
async function deleteCats( req, res, next) {
  let id=req.params.id;
  try {

  }
  catch (err) {
    next(err);
  }
}

// client-side
deleteCat = async (id) => {
  try{
    let url = `${SERVER}/cats/${id}`;
    await axios.delete(url);
    let updatedCats = this.state.cats.filter(cat => cat._id !== id);
    this.setState({
      cats: updatedCats,
    });
  }
  catch(err){
    console.log('An error occurred in delete route: ', error.response.data);
  }
}

import Button from ('react-bootstrap/Button');
// add to the Form a register handler to the deleteCat method
// e.g. onClick={this.props.deleteCat()}
// then also use 'open-parens-arrow-function' to keep it from firing
onClick={() => this.props.deleteCat(this.props.cat._id)};
```

### CREATE

Front end: Create a Form to submit entry of a new item.  
In a submit handler function include `event.preventDefault();`  
Get value from checkbox: event.target.checkBoxName.checked (boolean).  
Create a new item *but do not put it into state*, instead just pass it to the Post function.  
Utilize async and await around and in the method that uses an Axios call.  
Remember to call '.data' on the object that Axios returns in order to actually use the returned data.  
After creating a new object in the DB, request a copy of it back from the DB so the front-end has the _id of the object as created by the DB server.  

### Request Params vs Request Query

Request.params: The item following the '?' in the URL.  
Request.query: Subsequent items in teh URL?

#### CORS

Cross-origin Scripting.  
If we want to see JSON data from a request, CORS must be utilized, and express.json 'middleware' must be injected:  

```js
app.use(cors());
app.use(express.json());
```

### Authorization

Utilize on delete or other 'dangerous' methods and/or on 'protected' data.  
Not required until Friday, where Auth0 will be taught, and implemented in Can Of Book.  

## Footer Notes

React: When nesting Components in the same file, the parent component might pass 'state' into the child component, which would refer to the passed-in variable(s) as 'props'.  
React State: When adding to an array variable in the setState{} code block, use the following:  

```js
this.setState({
  cats: [...this.state.cats, cat],
})
```
### Jon TODOs

[ ] Update .env and .env.sample TO MATCH in Lab Front-end code.  
[ ]Fix-up componentDidMount() to only call the getBooks async function, rather than have it doing the setState itself.  
[ ] Verify we are using `react: ^17.0.1`  
[ ] Review *hoisting* because this is becoming a common item to *know* in order to avoid problems with ordering methods and calls to those methods in React.  
