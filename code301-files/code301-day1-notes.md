# Class Notes

Morning Host: Dr. Robin Apparicio  
Instructor: Sheyna Watkins  

## Dr.Robin

Code Fellows is 9 yrs old  
Graduated over 1600 students  
Dr.Robin collects fountain pens (15 years)  
Instructor Sheyna likes researching ancestry  
Find Dr.Robin on Remo 6th floor!  
Also available via Slack.  
*Not too busy* for you, it is her job to help students!  

### Rules and Regs Reminders

Zero tolerance for CoC violations
Contact: coduct@codefellows.com
Be kind, be respectful  
Proper attribution is required when cutting/pasting code, work implemented by peers, etc  

### Expectations

Be available during core hours  
Video on, mic on, clothes on, mute if background noise  
Be kind to self and classmates  
Collaborate with classmates, participate in lectures
Set a schedule and stick with it
Respect working hours
Take breaks (food, water, 10-min cool-down)  
ASK FOR HELP: 15 minute rule  
REST  
Weekly surveys, be honest - good, bad, and ugly  
Use Slack, Remo... connect and network  
Communicate life issues, attendance, etc  
Participate in Partner Power Hours on fridays, every-other Saturday - use this to *network*  

### Emotional Intelligence

Bring your whole self to the process  
Be grounded emotionally  
Next level: People act on preconceived opinions that are not always based on facts

- These preconceptions get applied to people  

Bias: Prejudice in favor of or against one thing person or group compared with another usually in a way that is considered to be unfair.  
Stereotypes: Come from family, tv, religion, marketing, media/movies/news.  

#### How Do You Mitigate Bias

Avoid snap judgements.  
Self-reflect on our own opinions.  
We must be vulnerable.  
Implicit Bias: Not always conscious of it - the stories we make up of other people despite not knowing who they are.  
Conformity/Groupthink: Unfairly favor those that belong to your group. If something isn't working for you, say something.  
Confirmation Bias: Favor information that confirms to their own beliefs.  
Attribution Bias: Have a different rational for your own behavior vs that of others. Others making errors you yourself made but applying an error to the other person, not yourself.  
Micro-aggressions: Passive-agressive responses, usually non-verbal slights, snubs, etc.

Fixes:

- Be positive
- Increase contact with people that are different than you
- Be specific in your intent
- Change the way you do things
- Heighten awareness
- Take care of yourself

*Note:* We learn as we grow, and growth requires food.  

## Main

Shayna, ex CodeFellows student and 7yr developer.  

### Syllabus and Canvas

Module View: Shows planned assignments in class.  
Use the ToDo view for "what to work on next", items remove selves after submission.  
Sheyna *is* on Slack so use that for best results.  
Lecture: 9am to Noon/12:30ish.  
1pm - 2pm: Code Challenges.
2pm forward: Labs, reading assignment, etc.  

Readings: Timebox this as much as possible. Write a few notes, submit the assignment, then ask questions in class.  
Remo: *Sit with others*. Those that sit alone tend to not do as well in this class.  
Ask for help: More asks for help results in more TA's and helpers!  
Windows and React: If pwd results in 'mnt' or 'mount' in the path this could cause problems with React so get this resolved with a TA.  
Assignments: Turn-in assignments *before* deadline, so long as 20% of the work is done. Then, go back and re-work the assignment for up to full points.  
Readings: *No* point docking for late. Will lock at the end of each week.  
Code Challenges and Lab Assignments: Due at the end of every day by Midnight. 20% of score is docked if late. (Just like in Code201).  

- Timebox Code Challenges to 1 hour and then submit it! Next day will have time to discuss these.  
- Once that time is over, start work on the Lab(s) and get them submitted before Midnight.  

Retros: AKA Learning Journal. Reflect on what is and isn't working for me. Whatever I put into the Lab Assignment submission (comments, question responses) can be copy/pasted into that day's Retro.

*Assignments do not have to be perfect* in order to turn them in on time.  

Code:  

- eslintrc and gitignore are for server-side and are not useful for React-based work.  
- eslintrc and gitignore will *not* be needed until next week.  

### Prework Discussion

Remember to use 'use strict' to ensure 'this' is properly constrained. This will become important later on in this class.  

#### Hoisting

JS interpreter loads a code page from top-to-bottom twice.  
First run through: Only finds declared variables and vanilla JS Function definitions.
JS Function *expressions* are *not* loaded and therefore cannot be invoked *after* a variable is declared.  
Arrow Functions are not loaded fully either, so if they are invoked prior to read-thru, ES6 interpreters will throw a "ReferenceError: Cannot access 'name' before initialization".  

#### Arrow Functions

Keyword 'return' is implied.  
When braces are necessary, so is the 'return' keyword.  
Keyword 'this' is *dangerous* to use.  

- Refers to things *outside* of the context of the arrow function context.  
- Scope is *inherited*, rather than defined, by arrow functions.  

#### Classes

201 JS Constructor

```javascript
function Country(name, capital) {
  this.name = name;
  this.capital = capital;
  this.isAmazing = true;
}
```

301 Class Constructor

```javascript
class CountryClass {
  constructor(name, capital) {
    this.name = name;
    this.capital = capital;
  }
}
```

These examples result in the same thing, except Classes can be extended:

```javascript
class States extends CountryClass {
  // extend to create a states constructor
  constructor(name, capital, governor) {
    super(name, capital); // these are things it is getting from parent
    this.governor = governor;
  }
}
```

Extended functions cannot access be accessed by the parent class.  

### Code Challenges

Jon TODO: Find where I set this up (probably SPro7) and make sure the tests of work that I have to do 'fail' and start working on it.  

### For Each

Don't forget to `'use strict';`  
Create arrays: one with integers, another empty.  
Array object has its own forEach method: `Array.forEach();`  
For each has *no return value*.  
Use a callback function to operate on each element, iteratively.  

```javascript
let arr = [2, 5, 7, 8];
let newArr = [];
arr.forEach(
  (num) => {
    newArr.push(num + 1);
  }
);
console.log(newArr);
```

*Note*: Cannot use '++' within forEach (e.g. Immutable iterator).  

### Conceptual Talk About React

Used to build UI components.

- Buttons
- Drop downs
- Images
- Pages

Sites and Apps aren't static:

- Users could be logged in or out.
- Could be integrated with other sites or services.

Pages are a bit to broad.
Better to think about things that make up our pages.  
React simplifies displaying the UI.  

- Lots of similar portions or sections on a page.
- Data/content is different, but style and arrangement are similar or the same.

React is really good at using a simple component, passing it many values, that will be used to construct the UI.

#### Setup React

NPX: Does the work for us.  
React version just incremented.  
Node 14 or lower is recommended, though.
To up/down grade to Node v.14: `NVM use 14` or `nvm install 14`  

1. Verify node version.
2. `npx create-react-app {name-of-app}`
3. Create a new Repo in GitHub with description and public and do *not* add readme, gitignore, and license file.
4. Push an existing repo from the command line (npx initializes the git locally).
5. `npm start` runs the code.
6. Update package.json using 'older versions' from the CF Repo. Run `npm install` to update React with the package.json changes.

*Kabob Case*: Hyphenated titles and names.

NPX scaffolds-out lots of files.
React *must be compiled* it doesn't run in the browser out of the box.
Ctrl+C will *stop* the React server.

#### Deploy Early and Often

This is how we will deploy site while using React.

1. Use Netlify.  
2. Import project from GitHub.  
3. Click Deploy, wait a while.  

#### Files To Remove

Delete the following files from your project:

App.test
reportWebVital.js
setupTest.js
logo.svg

This will break stuff so cleanup index.js so it no longer references those files.

You can also remove existing App.css content and replace it. Just add `import './App.css';` to link-in the CSS.

#### Migrate from Functional to Class Based React

1. App.js: Is a functional component so delete *everything* and rewrite as a Class Component.
2. Follow the code sample below, these are minimum required code lines:

```javascript
import React from 'react';
class App extends React.Component {
  // render is required React Component method that returns JSX
  render() {
    return (
      <h1>Stuff</h1>  // as an example
      ) // wrap return statements in parens
      // wrapping multiple lines in a div is an option
      // better to send a fragment e.g. <> and </> "frags"
  }
}
export default App;
```

From here, you can start writing usual HTML code within the Frags to build things like *cards* for a web UI.

#### Tips and Tactics

When calling a Component in HTML:

- Auto-close the tag like as in previous HTML versions.
- Example `<Person />`.
- Can use Components over-and-over again in the JSX to get many UI elements using the same code.
- Can add attributes to pass data into the components from their parent, via 'props'.
- props must be referenced following the keyword 'this' e.g. `this.props`  
