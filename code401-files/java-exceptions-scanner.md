# Java Exceptions and Scanner

## Resources

Oracle Docs [About Exceptions](https://docs.oracle.com/javase/tutorial/essential/exceptions/index.html)  

Oracle Docs [About Scanning](https://docs.oracle.com/javase/tutorial/essential/io/scanning.html)  

Baeldung.com [Primatives and Objects](https://www.baeldung.com/java-primitives-vs-objects)  

## Primatives and Objects

Primatives include: int, bool, etc.  
Primative Types are REFs to their respective Classes, Integer, Boolean, etc.  
Primatives are immutable and Final (cannot be inherited from).  
Java converts between primitives and REF types automatically.  

```java
Integer j = 1; // 'autoboxing'
int i = new Integer(1); // unboxing
// from https://www.baeldung.com/java-primitives-vs-objects
```

Autoboxing: Converting a primitive type to a REF type.
Unboxing: Converting a REF type to a primitive type.  

### Memory Impacts

Primitives consume memory on the order of 1 to 64 bits depending on the primitive type e.g. boolean 1 bit; long & double 64 bits; all others in-between.  
*Note*: Some JVM implementations (like Oracle) map boolean type is mapped to an int of either 0 (false) or 1 (true) so it consumes *32 bits* not 1.  
Objects in the Heap (where REFs are stored) take longer to access than primitives in the Stack.  
REF Types are Objects and include additional overhead to access and manipulate.  

Arrays and Primitive Types:  

"...single-element arrays of primitive types are almost always more expensive (except for long and double) than the corresponding reference type" *[Baeldung.com, accessed 22-May-22, https://www.baeldung.com/java-primitives-vs-objects]  

### Performance

In Java, performance depends highly on the hardware the JVM is running on.  
The Java Compiler might run optimizations depending on the environment, state of VM, activity of other processes in the OS, etc.  
Object access performance still comes down to Stack vs Heap overhead though.  
Wrapper Classes (the REF wrapper around the primitive types) tend to be accessed more *slowly* than the primitive types.  

### Default Values

Usually the defaults are 0, 0.0d, etc.  
For Char type it is `\u0000`  
For Wrapper Classes the default is `null`  
When initializing (but not assigning) a variable, think about whether the default value of 0 (or its equivalent for the type) is proper, or if a `null` is a better default value given the context of the variable initialization and intended usage.  

### Usage

Primitive types tend to be faster and require less memory in the end.
Java Generics does *not allow primitive types*.  
Java Collections *do not allow primitive types*.  
Java Reflection API does *not allow primitive types*.  

## About Scanning

Java Scanner translated formatted input into tokens depending on their data type.  
White space is used to separate tokens by default (blank, tab, line terminators) => see `Character.isWhitespace`  

Oracle's recommended Scanner programming design:  

```java
import java.io.*;
import java.util.Scanner;

public class MyScannerClass {
  public static void main(String[] args) throws IOException {
    Scanner scanner = null;
    try {
      scanner = new Scanner(new BufferedReader(new FileReader(file_name.txt)));
      while (scanner.hasNext()) {
        // do stuff with scanner.next()
      }
    } finally {
      if (scanner != null) {
        scanner.close(); // allow scanner object to be garbage-collected
      }
    }
  }
}
```

*Note*: The Scanner class is not a 'stream', but needs to be closed to clear it's *underlying stream*.  

### Delimiters

Other delimiters can be selected besides default whitespace characters:

```java
...
scanner.useDelimiter(",\\s*"); // alternate delimiter specified using regex
...
```

## About Exceptions

Exceptions occur during program execution.  
Exceptions disrupt the normal flow of execution.  
Exceptions can be caught using a 'try...catch...finally' construct.  
The Exception class(es) track an exception instance through the call stack (method by method).  
The RunTime knows how to traverse the call stack, and thus where the Exception occurred, and details about the exception.  

### Catch or Specify Requirement

Code that throws certain exceptions must be enclosed by either a:  

1. 'Try' statement that catches the exception.  
2. A method that specifies that is can throw an execption using the `throws` clause.  

Code that does not honor the Catch or Specify requirement *will not compile*.  
Not all exceptions are subject to the requirements (it's ).  

#### Three Kinds of Exceptions

Checked Exceptions: Anticipated, recoverable situations e.g. bad user input handling.  
Error: External to the App and difficult to anticipate with any specificity and might not be able to recover from.  Catching these exceptions will allow the Java App to continue despite this uncontrolled situation, although exiting with a stack trace logging and perhaps a UI message is acceptable. NOT subject to Catch or Specify requirement!  
Runtime Exceptions: Internal to the application. Usually these cannot be anticipated or recovered from, and could be bugs or logic errors, or incorrect API usage. If an exception is being caught for a situation that could be a bug, it might be better to eliminate the bug. NOT subject to Catch or Specify requirement!  

Errors and Runtime Exceptions are "unchecked exceptions".  

#### Throwing Exceptions

Exceptions can be thrown by your code, package code, or by the Java Runtime itself.  
All exception "thrown" happens via the keyword 'throw'. Your code can utilize this keyword too.  
Throwable is the parent class to all Exception classes in Java, and the descendant classes allow for various exception types.  
Create your own exception Type (how?).  
Exceptions can be *chained*.  
It is recommended that you generate custom Exception Types when creating your own Package so developers know when an Exception originates form within your Package and not somewhere else.  

```java
public Object thingy() {
  Object thing;
  if (size == 0) {
    throw new EmptyStackException();
  }
  thing = objecttAt(size-1);
  setObjectAt(size-1, null);
  size--;
  return thing;
}
// the throw keyword tells the caller method that
// a an EmptyStackException condition has been hit
// within the public Ojbect thingy method.
```

Top level class is Object.  
Second level class (inherits from Object) is Throwable.  
There are two 3rd-level classes that inherit from Throwable: Error and Exception.

1. Error Class: Hard failures like Dynamic Linking will cause the JVM to throw an Error type.  
2. Exception Class: Most throw/catch happen using this class or derive from it. Indicative of a non-serious system problem.  

Exception Class has *many descendants* including NullPointerException, RunTimeException, and so-on.  

#### Try With Resources

Objects that must be closed after a program exits are called *Resources*.  
When a Resource is being used and a Try-Catch structure is necessary, Try-with-resources is utilized:  

```java
stack String readFirstLineFromFile(String path) throws IOException {
  try (FileReader fr = new FileReader(path));
    BufferedReader br = new BufferedReader(fr)) {
      return br.readLine();
    }
}
// throws IOException specifies the exception type that will be thrown
// the Resources are FileReader and BufferedReader
```

Classes that implement interface java.lang.AutoCloseable are eligible for use in a Try-with-Resources block.  

#### Finally

In situations where Try-with-Resources is not possible (Classes do not implemnet java.lang.AutoCloseable), utilize a Finally code block that executes the closing function(s) necessary regardless of whether or not an exception is thrown.  

#### Surpressing Exceptions

Supression happens when a separate exception is thrown within a Try block that is within a Try-with-Resources block.  
Suppressed exceptoins can be retreived by calling `Throwable.getSuppressed` from the exception thrown *by the try block*.  

#### Unchecked Exceptions - The DRAMA

RuntimeExceptoin, Error, and their subclasses do *not* have to be caught by Try-Catch blocks in Java.  
It is not necessarily *correct* to inherit your custom Exceptions from RuntimeException.  
It is not necessarily *correct* to throw only *unchecked exceptions*, either.  
Any Exception that can be thrown by a method is part of the method's public API, therefore callers *must know about the exceptions that the method could throw* so they can be handled.  
RunTime Exceptions are a result of programming problems (bugs) and therefore should be managed accordingly, rather than just de-facto thrown (or ignored/bypassed).  

Recommendations:

1. Do not throw a RuntimeException to create a subclass of RuntimeException simply because you don't want to be bothered with specifying the exceptions your methods *can* throw.  
2. If a client can reasonably be expected to recover from an exception, make it a *checked exception*, otherwise use an *unchecked exception* (the client couldn't do anything with the exception anyway).  

Recommendations were lifted almost verbatim from [Unchecked Exceptions - The Controversy](https://docs.oracle.com/javase/tutorial/essential/exceptions/runtime.html)  

#### Advantages of Exceptions

- Separate error-handling code from all other code => Ordinary processing and operations are easily distinguishable from error-handling code  
- Propagate Errors up the Call Stack => JRE searches *backward* through the call stack to find methods for handling Exceptions  
- Group differentiating error types => The Exception Classes hierarchy enables grouping/categorizing execptions  

#### Read Learn Write Finally

Try: Identifies code in which an exception could occur.  
Catch: Identifies code that is an "exception handling" codeblock.  
Finally: Identifies code that is *guaranteed to execute*, used for closing files, recovering resources, and performing other cleanup from anywhere in the previous code blocks.  

## Footer

Return to [Parent Readme.md](../README.html)  
