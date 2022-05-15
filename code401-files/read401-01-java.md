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

### Summary

Operators are used to build *expressions*.  
Expressions are the core components of *statements*.  
Statements can be grouped into *blocks*.  

### Expressions

Comprised of variables, operators, and possibly invoking other members.  
Evaluate to a single value.  
Data Types between expressions must match in order to process without error.  
Use parentheses to force order-of-operation precedence within expressions to ensure they evaluate to a predictable value every time.  

### Statements

End is semi-colon `;`  
Includes:

- Assignment expressions
- Usage of `++` or `--` e.g. `counter++;`  
- Method invokations  
- Object creation expressions  

### Blocks

Zero or more statements contained between braces `{` and `}`  
Some expressions utilize braces to surround *multi-line* code blocks  

### Control Flow Statements

Without control flow statements, code is executed from top-to-bottom.  
Control Flow Statements allow altering the flow of execution based on the state in memory (i.e. variable values) aka 'conditions' at that point in the code.  
Results of control flow might include:

- Skipping-over code blocks or statements i.e. break, if, or switch statements.  
- Running the same code block multiple times i.e. looping structures like for, do/while.  
- Executing code that was skipped before but now needs to be run i.e. if/then/else or switch statements.  

#### The Switch Construct

Because I have a hard time remembering how Switch statements are constructed in every language I've come across it, I've copied-pasted the example from *[Oracle Documentation, accessed 14May22]*:

```java
public class SwitchDemo {
    public static void main(String[] args) {

        int month = 8;
        String monthString;
        switch (month) {
            case 1:  monthString = "January";
                     break;
            case 2:  monthString = "February";
                     break;
            case 3:  monthString = "March";
                     break;
            case 4:  monthString = "April";
                     break;
            case 5:  monthString = "May";
                     break;
            case 6:  monthString = "June";
                     break;
            case 7:  monthString = "July";
                     break;
            case 8:  monthString = "August";
                     break;
            case 9:  monthString = "September";
                     break;
            case 10: monthString = "October";
                     break;
            case 11: monthString = "November";
                     break;
            case 12: monthString = "December";
                     break;
            default: monthString = "Invalid month";
                     break;
        }
        System.out.println(monthString);
    }
}
```

[Switch Demo by Oracle Docs](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/switch.html)  

## Compiling Code

To 'compile code' is to make human-readable code statements into machine-readable bits and bytes that become 'machine instructuctions' telling the computer what to do and when to do it.  
Compilers are converters that take C#, Java, and other compiled language code, and turn it into machine code for execution (Run Time).  
Compilers use strict rules to determine whether code *can* be compiled or not - some of them tell you while you are writing the code if there are errors in the code statements that would prevent compiling.  
Compilers, however, do *not* check code statements to determine if they do the right thing or not, they will compile "bad code" and either an exception is thrown at runtime, or incorrect (or unexpected) output occurs.  

### But That Is Not All Really

There is more to compiling that the simple statements listed above.  
For example, C# is not compiled to "machine language" literally, it is compiled to an intermediary code that a *runtime environment* (or virtual machine) can understand and execute.  
C++ compiles to machine language.  

### Another Definition of Compiling

Slacking.  
Playing when you should be coding.  

## Java Coding References

There are 51 keywords in Java, from 'abstract' to 'new' to 'while'.  
Arguably, the underscore '_' might or might not be a keyword, you decide.  
Java Literal Words that can only be used in a specific way, they are: 'false', 'null', and 'true'.  
Java Restricted Keywords are used in specific ways but can also be used as ordinary variable names, e.g. 'requires' when used as a statement tells Java to not execute the code without the external code required in the statement `requires some.other.module;` but `int requires = 0;` simply instantiates and initialized an integer called 'requires'.  
Identifiers are keywords that denote Java API commands that can be used elsewhere, but it could cause problems in the code e.g. `int System = 7; System.out.println(System); // does not work`  
User-created Identifiers: Words the developer uses to identify variables, objects, methods, and etc.  

Examples gleaned from *[Java For Dummites 8th Edition, page 20767, https://www.dummies.com/article/technology/programming-web-design/java/java-for-dummies-cheat-sheet-207676/]*  

All In One Java for Dummies [All In One Cheat Sheet](https://www.dummies.com/article/technology/programming-web-design/java/java-all-in-one-for-dummies-cheat-sheet-207712/)  

### Four Tools Needed To Dev Java

Java Compiler, Java Virtual Machine, Java API, and Java API Documentation are needed for developing apps using Java.  
Java SE is the standard edition.  
Java ME is special-purposed for small devices.  
Java EE is (was) the enterprise data-oriented development, but has since been handed over to the Eclipse Foundation and renamed to Jakarta EE.  

Information source for Java SE, ME, and Jakarta EE: *[Java for Dummies website, https://www.dummies.com/article/technology/programming-web-design/java/getting-started-with-java-programming-200023/]*  

Information source for portions of this subsection: *[Java For Dummies website, https://www.dummies.com/article/technology/programming-web-design/java/getting-started-with-java-programming-200023/]*  

### Error Messages and Meanings

There are multiple error messages that might be "thrown" in Java code at runtime.  
Here is a reference to [some errors and what they mean](https://www.dummies.com/article/technology/programming-web-design/java/tackling-error-messages-in-java-programming-199123/)  

## Footer

Return to [Parent Readme.md](../README.html)  
