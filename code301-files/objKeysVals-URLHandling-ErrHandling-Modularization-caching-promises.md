# Day 10 In Class Notes

## Warm-up

Was an express.js file will a dozen errors.  
Check the class repo for the solutions.  

## Code Challenge 09 Review

### Challenge 2

```js
const getCourseKeys = (obj) => {
  //  call Object.keys and the input is put in the params
  return Object.keys(obj);
}
```

### Challenge 6

Large array of characters, must use Object.values to determine if any character has children. Return a boolean.  

```js
const hasChildrenValues = (arr, character) => {
  //  only objects with children[] have children, otherwise it is a string. Array.map will expect every item in the array to contain something.  
  let kids = 0;
  arr.forEach(person => {
    if (person.name === character) {
      Object.keys(person).forEach((key, idx) => {
        // include an index to use it!
        if (key === 'children') {
          kids = Object.values(person)[idx].length;
        }
      })
    }
  });
  return kids ? true : false;
};
```

### Code Challenge 10

Use map, forEach, and filter now-a-days!

```js
'use strict';
let array2D = [
  ['D', 't', 'ab', 'B'],
  ['o', 'a', 'o', 'r'],
  ['n\'', 'l', 'u', 'u'],
  ['t', 'k', 't', 'no']
]
console.table(array2D);
for (let i in array2D) {
  let str = ''; //  accumulator
  for (let j in array2D[i]) {
    // for j in array2D at index i
    str += array2D[j][i];
  }
  console.log(str);
}
```

## Code Review

1. Clone code.
2. Front end: Leverage existing .env.sample, update with my key(s) and server urls (remove trailing slash), then rename to .env and save.'
3. Back end: Leverage existing .env.sample, update my key(s) and port setting(s).
4. Start nodemon on back-end.  
5. Start npm start on front-end.  
6. Stuff should work!

### Modularize

Add a 'modules' folder and put Module_Name.js files in there, and make sure the require statements call them from that folder. This helps to keep the code clean and code files tidy.  

### URL Handling

Declare URL on front end.
Axios call to back end includes a `?keyword`.
Server-side the route definition/handler hands-off the query as `keyword` to the processing code (in this case in a module).  
Request.query is built-in to the request, but the .variable at the end of that is actually the variable the server is looking for, so the client should configure when formulating its request.  
When instantiating Movie objects, use a ternary to set this.image (poster_path) e.g.: `this.image: poster_path ? poster_path : '';`  

- Also do a conditional-render `{test_item && <div>render_if_test_item_not_null</div>}`  

### Error Handling - Front End

Try-catch over a huge block of code over multiple requests will take down the entire site.  
Instead, try-catch over each request and directly associated code, so the rest of the code can execute so long as it has enough data to work with.  

> Consider using separate handler functions that manage each call, and they would each have their own try-catch blocks.  
> setState{} block: Always do this within the try block to set the results that did not throw. Also use setState in the catch(err) block to *reset appropriate state items*.  

## NEXT WEEK OVERVIEW

New project: Can of Books.
Can of Books Labs Mon, Tues, Weds, and Friday.  
Weds: BIG code review to prep for final exam.  
Thursday: Assessment e.g. final exam for Code301.
Learn AuthZero.
Final Project *must* use AuthZero.  

### Labs

Can of books will be completed with a partner.  

### Assessment

Given starter code that you have to do stuff with.
Does *not* include AuthZero.  
Zip-file will be sent that include FE and BE projects.

> Fix the bugs.
> Add specified functionality.
> Timed (4hrs).  
> SOLO - *limited* TA help allowed.  
> 80% to pass, based on strict rubrik.  
> Includes *deployment*  
> Open book!  

## Lab 10

1. Add cache to your server.
2. Work with some code that someone else wrote.

### Cache

#### Reasons to cache

1. More performant website/request pipeline.
2. Reduce costs when utilizing a 3rd party API.
3. Reduce likelyhood of API outage due to number of requests.

#### What To Cache and How Long

Weather data? Cache expire quickly.  
List of released movies? Cache expire over a longer period maybe weeks or months.  
DNS Lookup requests? Cache expire often (seconds to maybe a minute).  

#### Set Up A Cache

Server-side: `let cache = {};`  
What to use as a key? The search query term:

```js
let key = `${searchQuery}'Data';`;
```

Check the cache for data before working with it:

```js
// probably use .toLowerCase() to normalize the string
let oneMonth = 1000 * 60 * 60 * 24 * 30; // max age of cached item
// test this with something much smaller like 1000*30 (30 sec)

if (cache[key] && Date.now() - cache[key].timeStamp < {one_month_in_ms}) { // use bracket notation
  let result = cache[key];
}
else {
  // do your usual request to the api and store the .data in queryResult
  // then store the result in cache
  cache[key] = {
    data: queryResult,
    timeStamp: Date.now()
  }
  res.status(200).send(queryResult);
}
//in either case return the data for processing
```

### Takeaways

Caching in-memory does not require a lot of code!  
Does NOT have the benefit of surviving a server crash (like a remote cache or DB would).  

### Lab 10 Details

1. Keep your old js files by renaming them to my-*.  
2. Bring-in new code from the class repo folder (starter-code).  
3. Create a cache.js file and copy-in the starter code.  
4. Try running nodemon and look at the errors, debugging as you go.  
5. Try using ThunderClient to help debug routes.  
6. Weather.js => Start here, then copy the code and adapt it to make the Movies request. Could even use my version of Movies, it's up to me.  
7. DO NOT DO THE STRETCH GOAL unless your grade is already > 90%  

#### Pay Attention To

Promises.  
Class constructors.  
Variable naming that might not match the Lab10 stuff - just change *your code* to match the imported code.  

## TODOs

1. Review class notes to get the caching lesson down properly.
2. Complete working any labs this weekend.  
3. Complete any incomplete quizzes!  
