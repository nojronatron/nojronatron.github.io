# Power Hour Talk: All About Loops
Presenter: Kassie Bradshaw, Python Alum  

## "repl" 
KB used replit.com as the presentation

## Trivia  
JavaScript has 7 types of loops.  

## Looping Code in General
Just says "execute code within brackets".  
Usually includes some sort of condition under which the loop exits.  

## For Loop
`for (Where is the loop going to start?, Loop runs while this condition is true, How much will variable be incremented while loop is running? ) { code }`

## Foreach Loop
Is an Array prototype method.  
`let myArray = ["one", "two", "three"];`  
`arrayName.forEach(function(item, index){ do... });`  
Why use this instead of a for loop?  
- If you have the option of using a prototype method, use it!  
- PMs are better optimized for working with iterables.  
- Will only get back items that are actually defined; a benefit of a prototype method.  
  
Can use the "arrow function" to operate on each iterable.  
`myArray.forEach( item => console.log(item));`  


## While Loop  



## Map  
Loops over an array, creating a new array and modify it with results from operations against the source array.  
Usage: let newArray = `myArray.map(item => { let newItem = 'Value: ${item}'; console.log(newItem); return newItem;});`  
  
## For...In and For...Of Loops  
Is meant to iterate over the properties of an object.  
Can operate on arrays as well as objects, however:  
- forin when operated on arrays will return the indices of the array items (think for keys in array).  
  -- It _can_ get the values when using the key as the argument to the object indexer.  
- forof is used similarly to a For() loop.  
  
ForOf loop is the newest loop released.  
ForOf loop can iterate over any iterable object.  
ForOf loop is a simplified version of the For() loop, in that code is shorter but just as effective.  
  
`let myObject = { school: "codefellows", activity: "pph", time: "noonish"};`  
`let myArray = ["hi", "howedy", "how are ya?"];`  

Code expaining how to use For...In to return values by using the keys:  
`myArray.forIn(i => Console.Log( myArray[i] ));`  (this needs to be verified).  

## Breaking Out Of A Loop
There are a few ways?  
1. Use conditional with a `break` statement e.g. `if(j=2){break;}`.  
2. Use an additional conditional that increments the tracking variable for ex: `if ( condition ) { indexer = top indexer value};`.  


