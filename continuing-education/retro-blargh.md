# Occasional Retrospective Notes

Semi-regular notes taken during my software developer journey.

## Monday 12-Sept-2022

Now that I'm back from my volunteer event, I have some work to do. It's time to revisit K-ary Trees and Binary Search Trees. Coding these up and writing unit tests for these might take a minute, but I'm looking forward to reviewing these data structures and finding key takaway points for future use.

### Java Generics

I've battled with these before and I did so again today. For future reference, I need to remember the following to help guide me to a solution, faster:

1. Utilize an interface if you have to. This will set up a constraining rule that limits (or enforces) the types are actually supported within the class or class member.
1. Remember to separate type template placeholders for reference types, versus reference type's value(s) they might be holding.
1. Start with a completely non-generic class so it is easy to tell where the template placeholder types should go.
1. When certain methods do not easily support being generisized, consider moving the functionality closer to the expected/intended type(s), perhaps up the inheritance chain or via a new class that supports inheritance and/or inherits from another, similar class.

### Data Structures

Often times I struggle with taking instructions a little too literally. This causes me to try again and again to get code to work where it really shouldn't (see [Java Generics, above]{#java-generics}) or is above my skill level to complete in an efficient way. It will help me to remember that when writing code becomes difficult or I keep re-writing code and coming to a dead end, there are better ways to approach and resolve the problem:

1. Stop. Take a break and think about the problem that needs to be solved, logically.
1. Write out the problem domain and ask some questions about it to better describe the problem to solve, and perhaps uncover some ways to solve it.
1. Break out a diagramming or drawing app (or an actual dry-erase board) and try solving it through diagrams and simplified steps.

My experiences at Code Fellows taught me the importance of breaking down a problem into the smallest possible bits, and working through each individual component carefully. This should help keep me from "coding in circles" and instead, finding a solution that I can then write tests for and start coding, and move forward.

## Friday 9-Sept-2022

Today I have a volunteer event scheduled that will keep me busy through Sunday. Before that, I coded the Code Challenge and wrote a test for it and it passes! There are probably a few other tests to write to ensure the code is functional in all the expected ways including failure cases, while will be developed over time. For now, I'm calling the code challenge exercise a success, and can safely say that I passed the challenge per the rubric scoring system.

## Thursday 8-Sep-2022

Met with Ryan to go over our project, update the Trello cards, and plan next steps. Made good progress completing several MVP cards, created a few new ones, and updated existing ones. There are a few cards that seemed a little lacking in detail so we added to them when we could, otherwise left a comment reminding us that more definition would be necessary to do work.

Following the meeting I completed the tasks at hand and then got back to work building my Java Code Challenge Libraries, starting with Trees and Queues. They needed to be built from the ground up following the curriculum, which I found to be much easier to do this time around (versus when learning them in classes, earlier). I guess the pressure of everything including homework and new material every day, multiplied by lack of sleep and limited time, fried my brain a bit!

Once I built-out a Binary Tree with Pre-Order, In-Order, and Post-Order traversal methods, I then had to build-out a Queue class so that I could implement a breadth-first traversal method. This required implementing generics as well. All the while I was writing and running unit tests to ensure the code I wrote was working and when it wasn't, I would know quickly and could pin-point the problem and fix it.

I am to the point where I am ready to write the Code Challenge code that I planned-out on the whiteboard, but it is too late to get involved with that right now. When I get a little time I'll get back to it and find out just how well (or not!) I did in the mock interview!

## Wednesday 7-Sep-2022

I don't know where the time goes! Actually, plenty of it is spent doing research, learning about aspects of coding, taking care of things around my home and neighborhood, and volunteering in my community. Most recent community volunteer event was Tuesday where the ham radio emcomm team worked on a local repeater system to try and improved its coverage of the service area. No towers were climbed, and progress was made.

Things I've been working on include:

- Added planning and design work for EnigmaBay's React project, including a code review and PR approval and subsequent merge to main.
- Preparing for a volunteer event the weekend of Sept 12th.
- Cleaning up the yard, as there is a lot of loose grass clippings and other trimmings laying around. What fun.

Today and on Monday I spent a few hours doing interview preparation activities, mostly working with behavioral questions, but also looking at some software developer openings around the area. There was a post on a bulletin board I frequent about a remote job opening that could be interesting. The OP works for the company and stated the entry requirements might look very high, but the hiring managers are likely to accept more junior developers for the role. Some of the entry requirements include C#, Azure, SQL, Git, and Selenium -- all of which are things I have experience with. I have some research to do.

Today I completed a technical interview challenge. The expectation was to build a function that accepts to binary trees, counts tree nodes that have no children, compares the two counts, and return true if both counts are the same, false if not. In 40 minutes I was able to build a plausible algorithm, write the code (Java this time!), define my testing approach and tools, and analyze the solution using Big-O notation. The only part I was missing was a step-through of my solution using the identified inputs and outputs, which cost a few points in total. Even without verifying my Java code for syntactical and idiomatically correct, my self-analysis shows I would likely pass a Code Fellows technical interview. I'll write the Java code anyway to get the practice and confirm my assumption though.

Completing that code challenge in Java prompted me to review how Tree data structures are arranged, how to traverse them, and how to and analyze them. Doing this work begged for a new repository so I created one from scratch, and intend to build-out the repo with various code challenges including basic data structures (for reuse) such as Trees, Stacks, Graphs, and so on.

All of this aught to keep me quite busy for the forseeable future! :zany_face:

## Sunday 3-Sep-2022

Friday was busy with lots of tasks in lots of areas, including software. Most of the software-side of things was researching React-js design and techniques including planning, routing, and nav bars. Plenty of time was spent fiddling with CSS and react-bootstrap. The Enigma Bay team is making progress on the site layout based on wireframes and selected color palette, and I have a little work to do fixing up an alignment problem in a Component. Some things I should keep in mind when buiding a responsive site using CSS and Bootstrap:

- Try to avoid setting custom in-line CSS properties when they could be done in Boostrap. Not a hard-and-fast rule, but keeps the front-end code a little cleaner and easier to troubleshoot.
- Use 'm' for margin and 'p' for padding, along with 'x', 'y', 't', 'r', 'b', and 'l' to managing margin and padding the Boostrap way.
- Remember to use 'mx-auto' when necessary to help with centering items.
- Modify images and icons to be the right size for where they belong in the site, especially when using a responsive design that could either expand (causing the image to pixelate) or contract.
- Leverage 'text-center' in Bootstrap to simplify centering text within a box.
- Using 'd-flex' in Bootstrap is similar to declaring a flex-box. Applying this to a Grid Column can help with responsive design. Adding on to this, additional properties like 'justify-content-evenly' match-up well with CSS flex-box.
- Bootstrap also has width 'w' and height 'h' elements, and these can be applied to boxes as well as an `<img >` tag by setting its class e.g. `class="mw-100"`.
- Leverage `<div>` tags rather than `<p>` and other block or inline tags to improve control over customization. Otherwise, override each tag style, or better yet import a CSS reset file and define your own tag style defaults.
- Centering content both horizontally AND vertically is easily accomplished with flexbox. See the css and html code example below:

```css
.parent {
  height: 100%;
  display: flex;
  align-items: center; // horizontal centering
  justify-content: center; // vertical centering
  padding: .25rem; // your choice
}
```

```html
<div class="parent">{text}</div>
```

For responsive design, and allowing viewability on varying sized browser windows, try using 'vw', 'em', and 'rem' (relative em) units. Be aware that font styles and browser-zoom levels might cause unexpected results. There is a lot to this, and many resources exist that dive deeper into how to get responsive design working well.

After battling with Bootstrap for a little longer, I was reminded how difficult styling websites can be when mixing it with CSS, because Bootstrap implements margin, padding, and box-sizing automatically, which makes some CSS styling ineffective. I keep going back and forth between "stick with pure CSS!" and "stick with just using Bootstrap" and there is never a winning decision, it is always a draw. At least for the purposes of the current project, the time spent fiddling with style is just practice time anyway, and much of the styling wil be revamped completely as the project moves forward.

## Thursday 1-Sep-2022

This morning I worked on a [LeetCode](https://www.leetcode.com) challenge, medium level, in javascript. The goal was to implement a function that takes two non-empty linked lists with data type Integer (Number), and sum the values across lists. Remember elementary school math, summing large numbers like 714 and 237? Like that but with singly-linked nodes, and (of course) the numbers are in reverse-order, which makes carrying-over values a little more difficult. I'm about 75% done and will get back to it in a bit.

Meanwhile, EnigmaBay had a meeting to discuss moving the project forward. We chatted about color schemes, icons, CSS, Bootstrap, and SASS, React Router, and the React Component hierarchy we want to implement. Very productive! We start developing the layout and basic design of the website today.

ESLint with React was reporting some errors and warnings that were unexpected. After reinstalling eslinter and learning there is a plug-in specifically for React, I installed that too. Two elements needed to be udpated in the eslintrc.json file:

1. "extends" element needed to be updated to a collection that included both "eslint:recommended" and "plugin:react/recommended"
1. "parserOptions" element needed "sourceType": "module" added

Now linting seems to be working as expected.

## Wednesday 31-Aug-2022

It has been a busy start to the week. Not all of my activities have been code-related, unfortunately. Several tasks related to volunteer activities came up and I decided to concentrate efforts there to try and meet some deadlines in the coming weeks.

At any rate, I took time this morning to respond to a few interview questions and practiced speaking them aloud in an effort to gain my confidence and organize my thoughts, preparing for when the interviewing starts.

This morning I completed a technical interview challenge: Sum Odd Values in a Binary Tree. Ending (self) score was 34/40 (32 is passing). I was able to depict the problem domain, inputs and expected output, testing approach and basic test cases, write an algorithm and analyze it in Big O notation, as well as write pretty-close-to-working javascript code (minus a few syntactical errors).

To check my work (because testing ones self is dubious) opened a [replit](https://replit.com/@JonRumsey/SumOddNumsInBinaryTree#index.js) to validate my code. Note that I had to create classes to meet the requirements of the challenge:

- MyBinaryNode: For the Binary Tree class
- MyBinaryTree: For creating and storing the initial input
- MyNode: For the MyQueue class
- MyQueue: For breadth-first traversal

It was time consuming to write all of this out, but exercising my mind to get to the correct solution is important. I find myself questioning the code I write before, during, and after I write it (before testing it). Perhaps its the test engineer in me.

The next challenge was from [CodeWars](codewars.com) using javascript. In 40 minutes I completed whiteboarding Kata "Testing 1-2-3" and got very close to a solution. Below are some retrospective commments:

1. Array.prototype.length is a property, not a function/method.
1. Indexing into an array is zero-based so do not change the beginning iterator in a for loop unless you really really need to.
1. Next time consider using `Array.prototype.map( (element, idx)=> { return ... });` and increment idx value within the string concatenation (or template literal).
1. Concatenating strings in javascript using template literal requires `${}` placeholders and *back ticks* (e.g. code fencing characters).

```javascript
// template literals
let var1 = 1;
let var2 = 2;
let var3 = var1 + var2;
let myString = `${var1} plus ${var2} equals ${var3}`;
```

Considering my internal anxiety coding with javascript, not all that bad really.

## Saturday 27-Aug-2022

Reactjs oh-my!

I'm glad I started fiddling with React, javascript, and CSS these last few days. Today's adventure was trying to get a React site looking okay and passing props around. Looking back at issues and resolutions:

When importing a collection of data using a json file:

1. Be sure it is directly in the 'src' folder. A sub-folder or some other part of the React project folder hierarchy will not work.
1. Ensure the json collection is a collection starting with '[' and ending with ']', and also be sure to make all collection items objects using braces, separated by commas.
1. File contents do not need to be loaded into state in order to use them. They can be passed as props e.g. `<GameBoard wordlist={words} />`

When using React-Bootstrap, be sure to:

1. Install it: `npm install react-bootstrap bootstrap`
1. Import it in the root file: `import 'bootstrap/dist/css/bootstrap.min.css';`
1. Import the specific Bootstrap Component(s) you want to use on the Component you want to use it in `import { Container, Row, Col } from 'react-bootstrap';`

Track Keys and Values when passing a collection as props:

1. Review [React Keys](https://reactjs.org/docs/lists-and-keys.html#keys)
1. The Parent Component should specify the key attribute inside the array (inside a Map function).
1. The Child Component that uses the passed-in props does *not* need to reference props.key, only props.value (whatever value is).

Lastly, whenever it is not clear whether data is being passed around or what it looks like in-flight, use console.log and check it out at run time.

## Friday 26-Aug-2022

After finishing some tasks around the house, I jumped right in to a 40 minute technical interview challenge. This one was summing odd numbers in a binary tree. It tests the interviewee's understanding on binary trees, including traversal and Node data structures. Whiteboarding these challenges in Miro (and similar apps) is quite difficult because there is an additional interface layer between me and the depiction I'm attempting to draw and layout. When working on a real, in-person, dry-erase board, it is much easier to erase, correct, and draw-out the brainstorming and ideation. Granted, one benefit of Miro (and similar) is duplication of complex drawings is super fast!

It took the full 40 minutes but I earned a passing score because I pretty much nailed every section in the rubrik except for code and Big-O. The failures there were not writing any Big-O evaluation *at all*, and my javascript code was only 85% complete before the time expired.

To solve this challenge I used Breadth-first Traversal using a Queue, rather than Depth-first using a recursive function because it is more difficult to store Recursive function values/outputs than it is to collect and store data within a while structure.

Code Fellows hosted a Big-O algorithm analysis webinar with guest speaker and alumn Isaiah Burkes. He reviewed why we do code analysis, how it is done using Big-O notiation, and gave a few rules of thumb to help remember algorithm analysis:

- "code slows as data grows"
- "How does the run time of my code grow as the size of the input grows?:
- Analyze time (or space needed) for code to execute all steps for any and all inputs.

The last bulletpoint is referencing algorithms that take multiple input parameters. Each parameter has an impact of the algorithm run time and could significantly add to the run time.

After this I started in on the LingoBingo-js project, working in a dev branch to initialize a React singe-page webapp. The goal is to sort out how to build-out Components so they fit into the existing wireframe design intentions. I plan to do more work through the weekend, and the plan is to pick-up collaborative work early next week.

## Thursday 25-Aug-2022

As happens on most days when I leave my Linux box powered-on overnight, a Printer Added popup appears in the notification area on the desktop. This hasn't been a problem, but my curiosity about it got me researching. It's pretty simple: The CUPS service is restarted at about midnight daily in order to 'roll the log file'. There is a [bug](https://bugs.launchpad.net/ubuntu/+source/cups-filters/+bug/1869981) filled with Cannonical with discussion, and the basic result is there is not a problem per se, and it can be worked around.

I realized, after reviewing yesterday's technical interview problem js solution, that I failed to nullify a node within the `pop()` method. While this is not a problem per se, it is best practice to nullify objects so the memory is freed. For managed code the object will get garbage collected when all references to it are removed. The larger the code base, the more important this design practice becomes in terms of memory efficiency, so is a good habit to get into now.

```javascript
// updated pop() method code
  pop() {
    // returns the TOP node or item (LIFO) from the stack
    if (this.isEmpty) {
      return "Stack is empty";
    }
    let tempNode = this.top;
    this.top = tempNode.next;
    this.nodeCount = this.nodeCount - 1;
    this.isEmpty = this.nodeCount < 1;
    tempNode.next = null; // orphan tempNode from the Stack for cleanliness' sake
    return tempNode.data;
  }
```

My Stack's `isEmpty()` method is relying on a hidden nodeCount property to compute a boolean return when called. Looking at a best practice pseudo code example, I could instead just check to see if 'head' is null, and so long as I manage the 'head' node reference properly, `isEmpty()` should always return correctly and without throwing.

```javascript
// updated isEmpty() method code
class Stack {
  constructor() {
    this.top = null;
    // this.nodeCount = 0; // this is no longer necessary
    // this.isEmpty = true;
  }
  isEmpty() {
    return this.top === null;
  }
  // this.nodeCount operations removed from any methods that have it
  // this.isEmpty interrogations are replaced with this.isEmpty()
  // any code where this.isEmpty is calculated should instead point to this.isEmpty()
```

Earlier this morning I read an update from SalesForce about Heroku free products pricing changes. Yep, that's right, those free Dynos and Postgres instances you've been using for all these year might become charged services. Check out Heroku's Blog Article [Heroku's Next Chapter](https://blog.heroku.com/next-chapter) for information from Bob Wise, GM and EVP at SalesForce. Thankfully, no immediate action is needed, but sometime in October I'll need to revisit my Heroku instances and figure out what will be going away and what will stay.

Back to code! I failed another technical interview challenge (couldn't complete in 40 minutes, and was doing it wrong anyway) so I attempted to solve it without a time limit on my physical dry-erase board, and then punished myself :wink: by writing out the code in javascript.

I started with a Node class, similar to a linked list Node, but this will be used in a Queue class.

```javascript
class Node {
  constructor(data) {
    this.value = data;
    this.next = null;
  }
}
```

Then built the Queue class with count, front, and back properties, and functions isEmpty, getCount, peek, enqueue, and dequeue.

```javascript
class Queue {
  constructor() {
    this.count = 0;
    this.front = null;
    this.back = null;
  }
  isEmpty() {
    return this.front === null;
  }
  getCount() {
    return this.count;
  }
  peek() {
    if (this.front === null) {
      return null;
    } else {
      return this.front.value;
    }
  }
  enqueue(data) {
    let newNode = new Node(data);
    // case 1: no nodes in queue
    if (this.front === null &&
        this.front === this.back) {
      this.front = newNode;
      this.back = this.front;
      this.count = 1;
      return;
      }
    // case 2: 1 node in queue
    if (this.front !== null &&
       this.front === this.back) {
      this.back = newNode;
      this.front.next = this.back;
      this.count++;
      return;
     }
    // case 3: more than 1 node in queue
    this.back.next = newNode;
    this.back = newNode;
    this.count++;
  }
  dequeue() {
    if (this.isEmpty()) {
      return null;
    }
    let temp = this.front;
    this.front = this.front.next;
    temp.next = null;
    this.count--;
    return temp.value;
  }
}
```

Next up is the duck-duck-goose function code. Code Fellows utilized arrow functions for their datastructures and algorithms training assignments, so I followed suit.

The important part of the code starts with the Queue instantiation and loading from the input array. From there the main processing code is pretty short and sweet, but entails two iterating structures, which is not always the most efficient algorithm in BigO.

The worst-case BigO of Time for duckDuckGoose() is probably O(n * k). Thankfully, the Queue datastructure has a O(1) in time and O(1) in space for all of its operations so total time through each iteration is fairly fast and lean.

BigO in space for duckDuckGoose() is more like O(n) because the entire input array is stuffed into the Queue O(1) storage at a time for every item in the array.

```javascript
const duckDuckGoose = (arr, k) => {
  // test for null and empty cases here
  if (!Array.isArray(arr) || !Number.isInteger(k)) {
    return null;
  }
  if (arr.length < 1 || k === 0) {
    return null;
  }
  if (arr.length === 1) {
    return arr[0];
  }
  if (k === 1) {
    return arr.at(-1);
  }
  // end null empty test returns
  if (k < 0) {
    k = Math.abs(k);
  }
  
  let myQueue = new Queue();
  // enqueue the array!
  for (let idx=0; idx < arr.length; idx++) {
    myQueue.enqueue(arr[idx]);
  }

  // main processing
  while (myQueue.getCount() > 1) {
    for (let jdx=1; jdx < k; jdx++) {
      myQueue.enqueue(myQueue.dequeue());
    }
    myQueue.dequeue(); // this should be the kth item
  }

  // return result
  return myQueue.dequeue();
}
```

It's not always necessary to code all of the edge case tests (depends on your interviewer I guess), but I decided to do it to exercise my software test engineer skills.

Next I wrote some exercises starting with the example case, and added a bunch of edge case inputs and a few larger input cases. Below is the base example case:

```javascript
let result = duckDuckGoose(['a', 'b', 'c', 'd', 'e'], 3);
console.log('result a-e, 3: ', result);
```

In the end the challenge isn't really that hard, in fact it was easier to write it using a Queue (including coding the queue in full) than it was to try and solve it will various types of for and while loops.

## Wednesday 24-Aug-2022

While updating my notes organization yesterday, I also added some emojis that did not work at first. Some investigating revealed that I didn't have the correct plug-ins selected. Some references that lead me to the correct solution:

GitHub Docs on [Publishing GH Pages using Actions](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)

GitHub Docs on [Using Jekyll with GH Pages](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll)

Jeykyll's GH [README](https://github.com/jekyll/jemoji) defining the jemoji plugin.

Jekyll Docs on [Plugins](https://jekyllrb.com/docs/plugins/)

Sounds like Jekyll-themed GH Pages can be locally tested, which might require some Ruby knowledge - I didn't look too deeply into this as there are more important things for me to research and practice right now.

Technical Interviewing exercise: I attempted to complete a Stack-related technical interview question but could not complete the discussion and solution design within 40 minutes. This is not uncommon for me. So I took an additional 40 mins or so to try and create a Stack using Node just to see if I could do it using [replit.com](replit.com), and I could! Following is the code I wrote:

```javascript
'use strict';

// node class constructor
class Node {
  constructor(value) {
    this.data = value;
    this.next = null;
  }
}

// stack class constructor
class Stack {
  constructor() {
    this.top = null;
    this.nodeCount = 0;
    this.isEmpty = true;
  }
  push(value) {
    // node or item is added FILO to this stack and returns nothing
    let newNode = new Node(value);
    if (!this.isEmpty) {
      newNode.next = this.top;
    } 
    this.top = newNode;
    this.nodeCount = this.nodeCount + 1;
    this.isEmpty = this.nodeCount < 1;
  }
  pop() {
    // returns the TOP node or item (LIFO) from the stack
    if (this.isEmpty) {
      return "Stack is empty";
    }
    let tempNode = this.top;
    this.top = tempNode.next;
    this.nodeCount = this.nodeCount - 1;
    this.isEmpty = this.nodeCount < 1;
    return tempNode.data;
  }
  peek() {
    // returns a copy of the value at TOP node without removing it
    if (this.isEmpty) {
      return "Stack is empty";
    }
    return this.top.data;
  }
}
```

While this is not fully vetted (unit tests etc), the properties are updated correctly, and the pop(), peek(), and push() functions operate as expected.

The technical interview question was to track the maximum value within a Stack, so I worked on some code to implement that feature. Below is the additional code:

```javascript
// the code above...
  maxVal() {
    let arr = [];
    let result = this.peek();
    while (!this.isEmpty) {
      let temp = this.pop();
      result = temp > result ? temp : result;
      arr.push(temp);
    }
    for (let idx=arr.length - 1; idx >= 0; idx--){
      this.push(arr[idx]);
    }
    return result;
  }
// end of class definition
```

The code was all developed using a real dry-erase board and replit. Testing the code required `console.log()` and replit breakpoints and their built-in debugger. Here is the rest of the code:

```javascript
let myStack = new Stack();
let emptyStack = myStack.isEmpty;
console.log("Created stack. emptyStack? ", emptyStack);
myStack.push(100);
emptyStack = myStack.isEmpty;
console.log("Pushed a value. emptyStack? ", emptyStack);
let stackPeek = myStack.peek();
console.log("Peeking the stack, value is: ", stackPeek);
let popResult = myStack.pop();
console.log("popResult: ", popResult);
emptyStack = myStack.isEmpty;
console.log("emptyStack? ", emptyStack);
myStack.push(3);
myStack.push(2);
myStack.push(5);
myStack.push(1);
myStack.push(4);
console.log("stack empty should be false: ", myStack.isEmpty);
console.log("peek should be 4: ", myStack.peek());
console.log("maxVal should be 5: ", myStack.maxVal());
console.log("stack empty should be false: ", myStack.isEmpty);
console.log("peek should be 4: ", myStack.peek());
```

Just now I noticed that replit has a 'unit tests' tool! Something else to check out for sure.

That will be it for today. There is plenty more to do (of course), and never enough time.

## Tuesday 23-Aug-2022

After some meetings with Ryan about our MERN-stack project, I decided it would be a good idea to brush-up on various topics so I am primed for planning and development, especially React and CSS/Bootstrap. While I was browsing around my Code Fellows notes, I realized I did a terrible job of organizing my reading notes and in-class notes, so I reorganized them a bit. Several topics were missing altogether, others were incomplete, incoherent, or just not-quite-done. For some of these items I simply went in to the documentation, referenced authoritative materials, and made necessary edits, updates, and additions. For those topics that are missing, I'll have to create new documentation notes - one example is ReactRouter - which will be added to my [cont-ed index of topics](./conted-index.html).

## Saturday 20-Aug-2022

Despite telling myself I wouldn't do much "techie" stuff today, here I am working through CSSBattles.

Battle #2, Eye Of The Tiger #16 is pretty great. I couldn't finish it in 10 minutes like [these guys](https://www.youtube.com/watch?v=4ya4wpDgy_o) but that's not really important. The key take-aways are:

1. When using `display: flex;` always try `margin: auto;` in the child box to center it easily
1. Creating circular-ish items (think eyelid, teardrop, etc) use `border-radius: {top-left} {top-right} {bottom-right} {bottom-left}` in that order to control each corner
1. Margin properties can be short-handed into a single line similar to border and border-radius: `margin: {top} {right} {bottom} {left}`
1. Rotating a box with `transform: rotate(ndeg);` will make your margin-adjusting efforts confusing - just remember the previous take-away (tilt your head)

A decent overview of [flex box](https://www.youtube.com/watch?v=fYq5PXgSsbE).

Details about CSS [margin property](https://developer.mozilla.org/en-US/docs/Web/CSS/margin).

## Friday 19-Aug-2022

Over the past 2 weeks I have been busy with preparing for, and participating in, volunteer activities. The Multiple Sclorosis NW Division holds fund-raising bike rides throughout the US, and I helped by providing amateur radio and transportation services to promote a successful, incident-free, and enjoyable event for all participants and the MS Society itself. Less than a week later, I travelled into the woods to support Destination Trail's "Bigfoot 200" ultra-trail-marathon through the Gifford-Pinchot National Forest. Again, I provided ham radio communications to support the success of this event in terms of tracking runner's bib numbers as they enter and leave aid stations, as well as ones that "drop out" of the race due to time cutoff or exhaustion. Logistics is another big part of my volunteer efforts in person as well as "on the air" using ham radio, to help arrange supply deliveries, transportation of runners and crew from an Aid Station to another location, etc.

CodeWars challenges are a great way to prepare for technical interviews, especially wnen using a whiteboard to rationally work through the problem and design a possible solution. Practicing javascript challenges will help prepare me for anticipated work in the EnigmaBay team, on the Lingo Bingo WebApp.

Fridays at Code Fellows tend to be busy with streams of final presentations, mid-term presentations, guest speakers, and collective social events for CF students and alumni. Today's JavaScript 401 Finals presentations included a team with Andrew S, whom I hadn't talk to in a while. He was a peer in previous CF classes with me, and it was great to see him present his team's project. All teams presented very well and it was great to see their progress toward graduation!

There was also a Python Midterm presentation. The first team included previous team-mate Liesl, and the team obviously had a *lot* of fun presenting their app. The next team included previous team-mate Dana H and Gina N, as well as co-Code Fellows team mate Vinny S! Their app searches Wikipedia and finds related articles that link together a "start" and "end" article. The other teams also had amazing projects including a Chess game built from the ground up that included a console version as well as a GUI, and an app that scaped Canvas data and provided graphs, calendaring items, and quick links to common tools and areas of Canvas.

Back into coding practice, I work on CSSBattle.dev again. I need to remember how to make trangles, so here is an example of an upright isocolese triangle in red:

1. Set the left border as 100px solid and *transparent*
1. Set the right border as 100px solid and *tranparent*
1. Set the top border as 100px solid and red (or your preferred color for the entire triangle)

It is important to remember that the vertex angle is determined by border-left and border-right unit settings.

## Friday 29-July-2022

At some point in the future, I'll want to change-up this format to something like a more formal blog article. I haven't decided yet what it will be, other than not a massively long MD file with a FILO stack of entries.

I finished up the Zip Linked Lists code challenge review by performing a mock whiteboard interview within a 45 minute period and then adding the whiteboard to the solution. This is not really sustainable in that it will cause a tremendous number of repositories to appear in my GH profile with little benefit (to anyone), so I plan to set up separate code challenge repositories for various languages.

Related, I worked my way through a CodeWars challenge in javascript (which I haven't written much of lately). I followed the general rubrik outlined by Code Fellows for a technical interview and produced reasonable code that passed the default CodeWars unit tests. Not that that is everything! So this prompted me to create a new js-specific code challenge repository, so this a future efforts will have a place to live.

Somehow I decided today was a good day to look up how to add emojis to markdown files. There are at least two ways:

- If supported, just use colon-surrounding syntax i.e. `:smile:`
- Point to the appropriate API using image placeholder syntax i.e. `![smiley](url-to-smiley-emoji)`

For example:

`:smile:` in supported markdown interpreters results in a :smile:

`!["smiley"](https://github.githubassets.com/images/icons/emoji/unicode/1f603.png?v8)` results in a vvv large smiley vvv

!["smiley"](https://github.githubassets.com/images/icons/emoji/unicode/1f603.png?v8)

Here are a couple of references with more info:

[Emoji Cheat Sheet](https://github.com/ikatyang/emoji-cheat-sheet#smileys--emotion)

Markdownguide.org's [Extended Syntax guide](https://www.markdownguide.org/extended-syntax/#overview)

## Thursday 28-July-2022

Building Java Projects in GitHub using GH Actions. There is a template in github repo 'actions/starter-workflows' that is a good starter. Originally I copied an existing yml file from a CodeFellows example, but that was designed for a slightly different environment and project, so I had to modify it. There were a couple issues:

1. gradlew could not be found. This was probably because I was forcing a CHDIR in the yml file and I didn't need to.
1. gradlew could not be executed. In Linux, file permissions are managed using bits for Read, Write, eXecute, etc. Windows does as well but it is a little different. In my yml I defined an Ubuntu environment for building and testing, so permissions could be a problem. Git has the ability to set permissions via `git update-index --chmod=` and to add eXecute permissions append `+x` to the end.
1. The last change that was required was to set the JDK compatibility level to 11, instead of 17 (not supported in GH Actions?).

Earlier today was a Code 401 instructor's panel where they discussed current content in those classes. There was a good amount of discussion around C#/DotNet, and TypeScript (which is starting to make inroads to the JS class due to increased use in the industry). There was also good discussion around strategies to deal with learning to code, especially JS, such as breaking down the problem in words, and writing solutions as comments rather than code, and then worry about coding the problem once an algorithm appears to solve the problem at hand.

## Wednesday 27-July-2022

Today I passed the final technical interview at Code Fellows and am officially an alum! Certificate is due in a week or so!

Passing the technical interview was extremely difficult, and I followed the advice I'd received from Code Fellows instructors and staff: Stick with it, pay attention to the details, break down a problem into the smallest parts, and take care of myself along the way. I will continue to do more technical interview practicing while I job hunt, so that I am well practiced and can more easily get over nervousness during a real interview.

Today I picked-up where I left off with one of my older projects, the [Bigfoot Bib Report WL Form](https://nojronatron.github.io/Bigfoot-Bib-Report-WL-Form/). The BigFoot 200 event is coming up and during a recent preparatory meeting the form was re-introduced (much to my surprise and delight) and there was new (and renewed) interest in it. I'm going to try and get this as ready as possible, with help from other interested volunteers to test it and provide feedback on possible improvements.

There are a ton of projects on my pet-project kanban board that I stil need to get to. There is definitely more work than there is time. At least these projects and tasks are centered around the goals of improving my software developer skills in every regard, and prepare me for my next big thing.

## Footer

Back to [root README](../README.md)
