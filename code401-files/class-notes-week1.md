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

### Debugging

Did I set the type properly?  
Is the method accessible?  
Is my method expecting the correct type or the caller sending the correct type as args?  
Do the number of params match?  
Does the method return anything or is it void and is the caller expecting that?  
Where am I in the code body? Am I within another method or at the class root?  

### Compiling at the Terminal

Gradle (tomorrow).  
Today: JavaC.  

```sh
> javac filename.java
```

## Whiteboarding Overview

Note: There are many different ways a whiteboarding interview and layout will work/go.  
Problem Domain: The problem the interviewer supplies.  
Test Cases: Given a good input, a good output is expected (with examples?). Includes Edge Cases where errors or other returns could happen.  
Algorithm / Logic description: Use arrows and verbose english to discuss how the logic should work.  
Pseudocode: Required during week 1, later is optional. If it helps you, use it.  
Actual Code:  
Big O: Effeciency of the algorithm. No actual code writing is required to get this right.  
Step Through / After-code: Talk through the code, visualizing the step-through following current and next values based on operations.  

### Invision

Whiteboarding software.  
Recommended by Code Fellows.  

### Miro

Whiteboarding software.  
Alex says Miro is better than Invision.  

### Stay Engaged

You may have to ask questions of the interviewer to better understand the problem.  
What are the inputs and outputs? What are the types? Consider drawing example in/outputs.  
Edge Cases: Update these throughout the interview. Consider questions about nulls, empty/undefined, various datatypes, and whether in-place or output new result.  

#### Whiteboarding Advice

Ask as many questions about the problem as you can early in the process: inputs, desired outputs, are objects required or okay to just build a new method, etc.  
Keep whiteboard neat, but use enough style to differentiate sections of the whiteboard.  
Use the software to create images/drawing shapes with labels to depict input(s), output, and then put the steps in between.  
Chat about the algorithm next. Still not code, rather describe the algorithm operation(s).  
Pseudo-code: With a visual and an algorithm, write pseudo-code to represent how the actual code would work.  
Big-O Notation: Creating a variable is O(1); Not creating any new structures so Space O(1); Time O(n).  
More Big-O: Mention the worst-case scenario O(n) in time for the algorithm and make an assertion about use of space.  
Testing Discussion: Describe which testing suites you would use, if/when purposely-failing tests, null/empty tests, and known-good (must pass) test methods.  
Remember to cover *start* and *stop* conditions if they are used.  
Talk-though the whiteboarding every step of the way.  
At any time throughout the process, tell the interviewer when you are going to stop and think through something briefly -- avoid uncomfortable and/or unexpected silence.  
Revisit the algorithm to ensure it matches your code.  
You can talk as you type and what you type.  
Ask the interviewer if they have any questions about what you've done so far and whether anything could be reviewed.  
If you want to use a built-in method *you'd better know how it works*!  
Testing: Mention JUnit Jupiter as the testing tools and the basic pass/fail requirement.  

## Tuesday Discussion Topics and Streams of Thoughts

### Review Pluralize Lab

Do not have to use '.Equals()' when comparing non-objects.  
Do not overload a single method => DRY and single-responsibility.  
Public: Accessible everywhere within the current Project.  
Private: Limited access within a subset of the current Project (more on this later).  

### Practice Whiteboard Interview

Experience and Exposure are going to help you getting through these problems.  
This problem was "Given an array, return an array with the middle index removed."  
Good question to ask: "Should the array be edited in-place or can I return a new array?"  
Another good question: "Do you have sample input I can use?"  
Another question regarding arrays: "If working with an odd-length array, should there be any special handling?"  
What do I know about arrays? They have a length; They are of a set size.  
Visual: Should reflect the algorith including input and result or output of the algorithm.  
Recursion: A separate iterating process than Looping.  
When thinking through the Algorithm:  

- Do NOT think about code specifically.  
- Consider more about the step-by-steps required to meet the Problem Domain statement and visual.  

When Pseudo-coding:  

- High-level, code-looking statements, but worry less about specific code and instead consider how the statements solve the problem.  
- Use declarations perhaps in CAPS with terms like DECLARE, DEFINE, ITERATE, RETURN, etc.  

Solve the problem first *then* write the code.  

### Gradle

Automation building tool for Java.  
Maven is a compettitor but we are not going to use it in this class.  
Groovy and Kotlin can be used but will not be used in this class either.  
To create a new Gradle project: `$> gradle init` which generates project files etc.  
Gradle uses its own Daemon (process) to manage its work.  
Gradle will ask a bunch of questions: Apps vs Libraries, etc.  
*Important*: Use JUnit Jupiter.  
Gradle sets up the JUnit Jupiter with a default "proof of life" test.  
It is up to you to build-out other tests necessary for your project.  

### IntelliJ

Important: *Where* you open your IDEA folder. If you don't see 'settings.gradle' you are in the *wrong folder* and tests will not run, etc.  
Everything under the '/test' folder should be colored 'green' otherwise you opened the project in the wrong folder.  
For a package, concentrate in the 'lib' folder to build your package namespace => lib/src/main/java/project_name/Library  
Packages cannot be Run in IDEA like an App can.  
Use LibraryTest (and other tests you create) to test your ...library.  
*Note*: Ensure to include '.idea' in the `.gitignore` file with your submitted work.  
Resources allow building modular code e.g. APIs to incorporate into your custom App.  
Performance and IDEA Cache: Invalidate the cache every once in a while to maintain IDEA performance.  

#### Packages

Import using `package.class.member` or `package.class.*`  

#### Testing

Arrange => Act => Assert

Arrange: Configure variables to prep for testing including test-inputs and expected outputs.  
Act: Call the function under test.  
Assert: Pass/Fail output based on expected return the function under test.  
Use the term "System Under Test" or 'sut'
Create your test names to describe what the test is doing and expected output.  
*Note*: Empty Tests will PASS by default!  

#### Check Your SDK

Make sure the language and SDK selection in Project Structure are correct.  
Do *not* use the Oracle SDK for this class.  
Run the tests after setting SDK and continue only if the tests pass.  

## ArrayList T

ArrayList has built-in methods like `.add` and several others:  

- Get: `.get(n)` accesses an element via the index number 'n'.  
- Set: `.set(n)` modifies an element in place via index number 'n'.  
- Remove: `.remove(n)` removes an element via the index number 'n'.  
- Clear: `.clear();` removes all elements from the array.  

```java
String[] studentArray = new String[9]; // create new array of strings with capacity of 9
ArrayList<Integer> classSizes = new ArrayList<>(); // this is an object Type
```

### AsList

This comes from a parent package to the ArrayList class.  
Use like `my_arrayList.addAll(Arrays.asList(my_other_array));`  

### Collections

Has built-in methods like SORT that take an existing Array as an argument and sort it (in-place?).  

## Wednesday Whiteboard Review

CONDITIONAL instead of IF
DEFINE functions instead of DECLARING them
DECLARE variables

Question: Is this a sorted array? If so, should it stay that way?  

## Creating Packages

Name your Package and Class *the same thing*.  
Exporting a package: First line of package should be `package package_name;` to make it available to the rest of your code in your App.  
Importing: Grab a single class `import package_name.ClassName;` or all members in a package `import package_name.*;`  
Create a package to easily reuse code, including your own!  
IntelliJ: rClick => New => Package. Create a new Class within the package_name folder.  
Package Names are camelCase.  
Class Names are PascalCase.  

## Map and Set

HashMaps aka Dictionaries aka Hash Tables aka Key-Value Stores.  
HashMaps are good at storing retreivable, organized data.  
Set extends HashMaps?  
HashSet inclues member `.addAll(ArrayList<>)` to bulk-add an existing ArrayList.  
Linked- versions of HashMaps and HashSets maintain order.  
Good at handling: Counts, Lookups, and Uniqueness.  
Measure Uniqueness!!  
Quick Lookups!!  
Count Instances!!  

### Maps

Maps accept a Key Value pairs as args.  
Values *belong* to a specific Key.  
KV Pairs need to be typed e.g. Key of type Integer, Value of type String.  
Create a HashMap Example: `HashMap<String, ArrayList<Boolean>> variableName = new HashMap<>();`  
Create a HashSet Example: `HashSet<String> variableName = new HashSet<>();`  

### Input and Output

Path: `import java.nio.file.Path;`  
Paths: `import java.nio.file.Paths;`  
Access, Read, track (counting instances): `HashMap<String, Integer> myMap = new HashMap<>(); String[] items = {string, string, ...}; System.out.println(scannerInstance.nextLine());`  

Access: `Path path_var = Paths.get(file_path_var);`  
Get Absolute Path: `path_var.toAbsolutePath();` outputs the path in full of the path_var value.  

### Scanner

Java's Scanner class has built-in methods that will be helpful.  
Boolean `.hasNextLine()` returns true only if look-ahead to next line succeeds.  
Remember to use RegEx101.com to help when regex is the right solution for finding strings in lines.  

```java
Scanner scanner = new Scanner(path);
scanner.hasNext();
scanner.nextLine();
```

Relative vs. Absolute file pathing:

- Absolute can be a good for accessing a file that is in an expected location, i.e. a `/bin` directory.  
- Relative will be relative to the root of the executable's PWD.  

### Exception Handling

Types include: Runtime Exceptions, IO Exceptions i.e. File System based.  

```java
try {
  // run your might-throw-an-exception code here
  myScanner = new Scanner(myPath);

}
catch (IDException ioe) {
  // oopsie something bad happened in the try block
  System.out.println("That file cnnot be scanned or was not found. File path is: " + myPath.toAbsolutePath());
  ioe.printStackTrace();
  System.exit(status_code);  // status_code can be any integer but 0 is usually 'success' 
                             // any other integer is 'failure of some type'
}
```

Multiple Catch blocks can be defined.  

## Static and Non-Static Members

Static members are shared among all instances of a Class.  
Static members can be called via the ClassName of the containing Class.  
Non-Static members are Instance Members.  
Instance Members are unique to the Instance of the Class.  
Instance Members are *not shared* among instances.  
You will want to consider the following when creating a member:

- Member needs to share data with other instances: Make it STATIC.  
- Member should only be utilized by the instance of the Class: Do *not* use Static.  

## Setting Up A New Java Project

1. Go to the directory and mkdir the project directory you want to do.  
1. Git Pull.
1. gradle init
1. Difference between an App and a Library? Apps have Main (an 'entry point').  
1. Check that correct SDK is selected (apply it) and then do a BUILD.  
1. Check if settings.gradle is in the root

*Note*: Sometimes the project directory must be removed and gradle init run again.

## Object Oriented Programming

There are 8 primitive data types in Java.  
Everything else *is a class*.  
Classes are blueprints for instantiated object(s).  
Methods define *behaviors*.  
State is defined by the data contained within the object e.g. Fields and Properties.  
Methods often alter the state (or Properties) of an object, like change a boolean value via a method.  
Constructors allow instantiating Objects from Classes.  

### OOP Principals

Encapsulation: Hide state (data) from other objects and processes.  
Inheritance: Avoids having to re-write Classes by enabling building-upon an existing 'parent' class.  

#### Encapsulation

Encapsulation: Do not display the data state of an object to everything.  
Encapsulation: Use GETter and SETter functions to change state (data).  
Use 'static' keyword to *share Methods and Properties* between object instances.  

### Access Modifiers

Public: The class you are working in can see all other access-modified members.  
Protected: Classes, Packages, Subclasses, and other Project-level items have access.  
Private: Only the defining Class can access these members.  
Default: Only the defining class or Package.  

*Note*: Default is an optional modifier keyword.  

### Constructors

Build your own constructor!  
Use 'public' to allow calling the Constructor from other modules.  
The term 'this' relates to the current *scope*.  
Multiple Constructors can be created with differing parameter lists.  

### Properties

Keep Properties private.  
Constants can be created that cannot be edited using 'final' keyword.  

```java
public static final int MY_CONST = 1;
// use UPPER_SNAKE_CASE for constant properties
```

### Domain Modeling

## Acquire Input From Terminal

`./gradlew run --args strings...`  

To have your App accept other types (besides String[]), just define the args parameter list in Main method.  

```sh
./gradlew run --args %arg_types_defined_by_main_method%
```

## Aliasing TerminalFor Automation

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
[ ] GitIgnore: Use this for the *entire class*  

Assignments Due Thursday:

[ ] Read: Java Primitives vs Objects, Exceptions, Scanner  
[ ] Pick Accountability Partners  
[ ] Read04: OOP, Objects, Binary, Decimal, and Hexidecimal  
[ ] Code Challenge - Paired Whiteboard Interviewing  
[ ] Complete Lab03  
[ ] Lab04 (make as much progress as possible within timebox TBD) (interact with a BMP file)  
[ ] Learning Journal  

Get-Ahead Work Items As Time Permits:

[ ] Workshop #1 Prep: Networking Gameplan  
[ ] Workshop #1 Prep: Resume & Completed Resume

## Class Time Notes

## Footer

Back to [root Readme](../README.md)  
