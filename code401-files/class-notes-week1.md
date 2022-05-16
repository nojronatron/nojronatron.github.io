# Java401d12 Class Notes

Week 1: 16-May to 20-May 2022

A collection of draft, WIP, and straggler notes taken during class discussion, presentations, etc.  

## Dr.Robin

You Are A Software Developer! Get used to calling yourself this.  
We are all developers here, and the more often you say it the more of a reality it becomes.  
"Tech skills for a better life, community, and world." -Code Fellows Vision  
Mission: Guide people from all backgrounds to change lives through fast-paced, career-focused education. Shaping passionate learners with immersive training to meet industry needs and improve diversity." -Code Fellows Mission  

Campus Director

### Advice

- Use "___ helped with ___" to ensure assistants are recognized.  
- Attribute with URLs to copied code.  
- Include collaborative efforts in Readme.md or Collab.md  
- The more you put in, the more you will get out.  
- Set up a schedule and *stick to it*, including breaks, food, and drink.  
- Ask for help, do NOT 'muscle through' issues.  
- Dig-in to networking during Code 401 (it is expected)  
- Polish materials to get ready for interviews including "do my GitHub Projects showcase my talent?"  
- Personal Brand: 'Here I am, someone who is invested in *some thing*' and preparing to *promote your brand*... things that set you apart from the rest of the field. Culminates in Brand Presentation day.  

### Career Accelerator Program

Direct support to you while planning for your next career.  
Must graduate 401, submit a (stellar) resume, pass a qualifying *moch behavioral* interview (45 mins max) with post-interview feedback for improvement. DO NOT LEAVE THIS ON THE TABLE.  
Not a one-shot deal.  

### Talent Portal

Connects alumni with 'partners' with Code Fellows, where CF manages resume passing and keeping alumni notified as to which partner(s) are viewing the CAP resume.  

## Class Discussion

Prepare for reading a ton of documentation.  
Start getting good at extrapolating a solution from reading documentation and other resources.  
Put effort into *exposure* and *practice* throughout this class, and within tech.  
Slack DM Alex for short discussions or anything that is critically important.  
For longer discussions (30 mins+) schedule ahead of time w/ Alex.  
Lunch will *always* be from 1230 to 1330.  
Get code challenges out of the way 1st and DO NOT TAKE LONGER else you are doing yourself a dis-service.  
You have *one job* as a developer: SOLVE PROBLEMS, which can be an *endless time suck*.  
Do *not* refactor until you are done *solving the problem*.  
Goto Canvas and the Class Repo to keep up to date and help solving code problems, including class recordings (1-3 hrs after class to encode).  
FYI: React can work with other languages besides javascript.  
Spring MVC:  
Thymeleaf: Template engine.  
Assignments will re-open before mid-terms, then close for the remainder of the class.  
Final opportunity to submit assignments during 2nd half will be before final project week.  
Late work: Turn-in substantially completed work *before* deadlines, to avoid penalty when completed later.  
Do NOT worry about implementing tests in Code Challenge Day 1.  
While Alex is in Remo, he is available to get assistance/conversations.  

## Objects and Arrays

Arrays should store like-data values.  
Objects can store different data types.  
Create objects multiple ways including `let myObj = {};` and object instantiation of a class `let myThingy = new Thingy([args],...)`  
DRY: Don't Repeat Yourself. Classes allow following this principal.  
Strongly Typed Languages: Require declaring a Type (or Class).  
Functional and Procedural languages include javascript: Run code top-to-bottom as a runtime language.  
Compiled languages like Java are translated to run in a specific way, not just top-to-bottom.  
Libraries: Do *not* utilize a 'main' function.  

## Long Stream of Consciousness

Protected, Public, and Private: Control access to classes and members.  
Parameters: Abstract idea that the variables will eventually have values.  
Arguments: Whatever you want to call the local variables you will use within the function.  
Dot notation/object notation: Use '.' between objects and their members, child-objects, etc.  
Escape character `\`: Use to enable use of a reserved character in a string.  
Applications need an entry-point e.g. a 'main' function.  
Libraries do *not* have an entry-point and are referenced by another App or other Libraries.  
To execute java apps from command line: `java appName.java` But this performs the java runtime execution but it probably doesn't do a full compilation.  
Compiler: javac.exe is an example. It just creates a 'build file' but does not execute it.  
Always *compile* before pushing to your repo.  
Probably the most commonly used types will be String and Int.  
Hexadecimal values default to Int type, so be sure to cast to the correct type for the size of the Hex value.  
CONSTANT_VALUES can be accessed outside of the defining class with: `className.CONST_VAL;`  
Work within objects, using methods within those objects to get work done.  
String Interpolation? *NO* Instead do: `System.out.println("Maximum integer is: " + maxInt)`;  
Terminology: Method (rather than Function) because we are working in a OOP language.  
Short-cut declartion for float and double: 'f' and 'd'.  
Expressions: Happen within parens `( expr... )`  
Need precision? Float (32-bit) over Decimal.  
String type is a Class *not a primitive type*.  
Characters 'char' are a special type that represent ASCII codes to display a specific single character.  
char char1 + char char2 returns a 'string'.  
Integer.parseInt(string): Converts a string into an integer.  
Do not use '==' to compare/equality of objects, *this includes String*!  
When comparing Types '==' will fail you so use `{}.equals(other)` instead.  
Overflow: Wraps-around from MAX_VAL to MIN_VAL and vice-versa.  
Two ways to create arrays:  

```java
int[] myArray = new int[10];
int[] myArray2 = {1,2,3};
```

Println(array) will return the reference address to the item in memory.  
Common java utilities example: `import java.util.____`  
Use StackOverflow and Google searches to find the import libraries you want/need rather than trying to wade through docs.oracle.com (don't get lost in the sauce).  

Loops: FOR and WHILE  

```java
for(int i=0; i,myArr.length; i++) {
  ...
}
```

```java
//  use a boolean conditional because it will be easy to read
while(condition) {
  incrementor/decrementor/condition-setter
  ...
}
```

For...Of

```java
//  for every value in :array do codeblock statements
for(type variable : array) {
  codeblock;
}
//  : is essentialy the "of" in the statement
//  Inc/decrementor is not necessary here
```

Break: Break *out* of the parent looping structure.  
Continue: Move on with next iteration.  
Be aware: Procedural Debugging is a little different than Compiler debugging.  
Static: Can be applied to Methods and Variables.  


### Aliasing For Automation

Aliasing: `alias ls='ls -la'` causes `ls` to always run `ls -la`.  
[ ] Mess with this to streamline my processes.  

## Prep Notes TODOs and Reminders

[ ] DS&A Syllabus  
[ ] Career Coaching Syllabus  
[ ] Roger wants a connection to Ninendo.  
[ ] Take a look at Full Stack Labs.  
[ ] Prep for technical moch interviews through reviewing Code Challenges and previous projects.  
[ ] Prep for behavioral moch interviews through completion of STAR Questions.  
[ ] Study Whiteboard Challenge Workflow to get your future whiteboards to look a certain way.  
[ ] Not sure how to do something like build a project? Run it? Do it over and over until it makes sense and becomes easier and commits to memory.  
[ ] Include blockers and challenging areas in Learning Journals for your own good *and* so Alex is aware of what is going on.  
[ ] Ask yourself DS&A questions: How do I traverse this structure? Sort that out *first*.  
[ ] Thursday Code Challenges are *Moch Interview* assignments, timeboxed to 30 minutes.  
[ ] Build a shortcut to assist with string concatenation in Java.  

Assignments Due Monday:

[X] Read  
[ ] Code Challenge (just get the whiteboard layout good and properly whiteboard the solution)  
[ ] Lab  
[ ] Learning Journal

Assignments Due Tuesday Morning:  

[ ] Read: Java Imorts (but not NetBeans) and Loops in Java  

Get-Ahead Work Items As Time Permits:

[ ] Pick Accountability Partners  
[ ] Workshop #1 Prep: Networking Gameplan  
[ ] Workshop #1 Prep: Resume & Completed Resume

## Class Time Notes

## Footer

Back to [root Readme](../README.md)  
