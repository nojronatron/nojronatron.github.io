# Read Class 01

Notes and comments taken while completing assignment Read: Class 01.

Oracle Docs on [Java Language Basics](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/index.html)  
Reddit Thread on [Compiling](https://www.reddit.com/r/explainlikeimfive/comments/233dq5/eli5_what_does_it_mean_to_compile_code/)  
XKCD Comic on [Compiling](https://xkcd.com/303/)  
Java Articles for [Dummies](https://www.dummies.com/category/articles/java-33602/)  

## Java Language Basics

### Variables

Instance Variables: Objects store their data in 'non-static fields' aka 'instance variables', which are unique to that instance of a class.  
Class Variable: Only one instance of the variable exists among class instances aka 'static fields'. Precede the variable initialization with the keyword 'static'.  
Local Variable: Temporary variables that store data local to a *method*. The variable is local to the method's enclosing braces.  
Parameters: A list of one or more local variables that are scoped to a method that are passed-in from a calling method.  

### Naming

Any legal word that is not a special or reserved keyword.  
*Should* start with a letter (by convention).  
Should *NOT* start with a '$' or "_".  
Whitespace is not permitted as the first character.  
Letters, digits, dollar signs, and underscore characters are legal only as middle-characters (after leading character).  
Use all-lowercase for single-word names.  
Use camelCase for multi-word names.  
Constants should be named in ALL_CAPS_WITH_UNDERSCORES.  

## Operators

Operators perform functions on the state (data stored in) variables.  
Precedence: Operators perform their actions in a specified order of evaluation.  
Evaluation: Operators are evaluated from left-to-right.  

### Operators By Precedence

(Descending order of precedence)  

Postfix:  `expr++`, `expr--`  
Unary: `++expr`, `--expr`, `+expr`, `-expr`, `~`, `!`  
Mutiplicative:  `*`, `/`, `%`  
Additive: `+`, `-`  
Shift: `<<`, `>>`, `>>>`  
Relational: `<`, `>`, `<=` `>=` `instanceOf`  
Equality: `==`, `!=`  
bitwise AND: `&`  
Bitwise Exclusive OR: `^`  
Bitwise Inclusive OR: `|`  
Logical AND: `&&`  
Logical OR: `||`  
Ternary: `?` and `:`  
Assignment: `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `&=`, `^=`, `|=`, `<<=`, `>>=`, `>>>=`  

## Expressions Statements and Blocks


## Footer

Return to [Parent Readme.md](../README.html)  
