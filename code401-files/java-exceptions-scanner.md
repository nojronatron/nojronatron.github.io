# Java Exceptions and Scanner

## Resources

Oracle Docs [About Exceptions](https://docs.oracle.com/javase/tutorial/essential/exceptions/index.html)

Oracle Docs [About Scanning](https://docs.oracle.com/javase/tutorial/essential/io/scanning.html)

Baeldung.com [Primatives and Objects](https://www.baeldung.com/java-primitives-vs-objects)

## Primatives and Objects

Primatives:

- int, bool, etc.
- Are REFs to their respective Classes, Integer, Boolean, etc.
- Are immutable.
- Are Final (cannot be inherited from).

The Java compiler converts between primitives and REF types automatically.

### Autoboxing and Unboxing

Initializing a variable that _could be a primitive_ as a REF type is called 'autoboxing'.

```java
Integer j = 1; // 'autoboxing'
int i = new Integer(1); // unboxing
// from https://www.baeldung.com/java-primitives-vs-objects
```

Autoboxing: Converting a primitive type to a REF type.

Unboxing: Converting a REF type to a primitive type.

### Memory Impacts

Primitives consume memory on the order of 1 to 64 bits depending on the primitive type e.g. boolean 1 bit; long & double 64 bits; all others in-between.

_Note_: Some JVM implementations (like Oracle) map boolean type is mapped to an int of either 0 (false) or 1 (true) so it consumes _32 bits_ not 1.

Objects in the Heap (where REFs are stored) take longer to access than primitives in the Stack.

REF Types are Objects and include additional overhead to access and manipulate.

Arrays and Primitive Types:

"...single-element arrays of primitive types are almost always more expensive (except for long and double) than the corresponding reference type" \*[Baeldung.com, accessed 22-May-22, https://www.baeldung.com/java-primitives-vs-objects]

### Performance

In Java, performance depends highly on the hardware the JVM is running on.

The Java Compiler might run optimizations depending on the environment, state of VM, activity of other processes in the OS, etc.

Object access performance still comes down to Stack vs Heap overhead though.

Wrapper Classes (the REF wrapper around the primitive types) tend to be accessed more _slowly_ than the primitive types.

### Default Values

Usually the defaults are 0, 0.0d, etc.
For Char type it is `\u0000`
For Wrapper Classes the default is `null`
When initializing (but not assigning) a variable, think about whether the default value of 0 (or its equivalent for the type) is proper, or if a `null` is a better default value given the context of the variable initialization and intended usage.

### Usage

Primitive types tend to be faster and require less memory in the end.
Java Generics does _not allow primitive types_.
Java Collections _do not allow primitive types_.
Java Reflection API does _not allow primitive types_.

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

_Note_: The Scanner class is not a 'stream', but needs to be closed to clear it's _underlying stream_.

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

- 'Try' statement that catches the exception.
- A method that specifies that is can throw an execption using the `throws` clause.

Code that does not honor the Catch or Specify requirement _will not compile_.

Not all exceptions are subject to the requirements (it's ).

#### Three Kinds of Exceptions

Checked Exceptions: Anticipated, recoverable situations e.g. bad user input handling.

Error: External to the App and difficult to anticipate with any specificity and might not be able to recover from. Catching these exceptions will allow the Java App to continue despite this uncontrolled situation, although exiting with a stack trace logging and perhaps a UI message is acceptable. NOT subject to Catch or Specify requirement!

Runtime Exceptions: Internal to the application. Usually these cannot be anticipated or recovered from, and could be bugs or logic errors, or incorrect API usage. If an exception is being caught for a situation that could be a bug, it might be better to eliminate the bug. NOT subject to Catch or Specify requirement!

Key takeaway: Errors and Runtime Exceptions are "unchecked exceptions".

#### Throwing Exceptions

Exceptions can be thrown by your code, package code, or by the Java Runtime itself.

All exception "thrown" happens via the keyword 'throw'. Your code can utilize this keyword too.

Throwable is the parent class to all Exception classes in Java, and the descendant classes allow for various exception types.

Exceptions can be _chained_.

Devs can create a custom exception Type by inheriting from the base Exception Class, defining a String message, and then 'throwing' or 'catching' the Exception as usual.

It is recommended that you generate custom Exception Types when creating your own Package so developers know when an Exception originates form within your Package and not somewhere else.

An example that creates a custom Exception Type within a 'throw' statement:

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

Exception Class has _many descendants_ including NullPointerException, RunTimeException, and so-on.

#### Try With Resources

Objects that must be closed after a program exits are called _Resources_.

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

In situations where Try-with-Resources is not possible:

- Example: Classes that do not implemnet java.lang.AutoCloseable.
- Utilize a Finally code block that executes the closing function(s) necessary.
- Closing Function should be called regardless of whether or not an exception is thrown.

#### Supressing Exceptions

Supression happens when a separate exception is thrown within a Try block that is within a Try-with-Resources block.

Suppressed exceptoins can be retreived by calling `Throwable.getSuppressed` from the exception thrown _by the try block_.

#### Checked Exceptions - Detail

Represent errors outside of coding errors e.g. File IO cannot find a file because it does not exist.

Checked Exceptions are verified at _compile-time_.

Declare Checked Exceptions with the 'throws' keyword at the definition of a method.

```java
private static void checkedExceptionWithThrows() throws FileNotFoundException {
    File file = new File("not_existing_file.txt");
    FileInputStream stream = new FileInputStream(file);
}
```

Example above lifted from [Baeldung.com](https://www.baeldung.com/java-checked-unchecked-exceptions)

Common checked expections:

- IOException
- SQLException
- ParseException

Checked Exceptions inherit from parent class Exception.

Creating a new Exception can be done through inheritance e.g. `public class MySillyCustomException extends Exception {...}`.

#### Unchecked Exceptions - Detail

These are program-logic errors.

Unchecked Exceptions are _not_ verified at compile-time.

Do _not_ declare unchecked exceptions using the 'throws' keyword in a method.

Common Unchecked Exceptions include:

- NullPointerException
- ArrayIndexOutOfBoundsException
- IllegalArgumentException

RuntimeException Class is the superclass of all _unchecked exception_.

Extend RuntimeException to create a custom UncheckedException:

```java
public class MySillyUncheckedException extends RuntimeException {...}
```

#### When To Use Checked and Unchecked

Use to separate error-handling code from regular code.

Per Oracle documentation:

- Unchecked Exceptions should occur when the caller cannot be expected to (or is not able to) do anything to recover.
- Checked Exceptions should occur when the caller can _reasonably_ be expected to recover from the condition.

For Example:

- If the user inputted filepath is invalid, throw a (possibly custom) _Checked Exception_.
- If input filepath is _null_ or an _empty string_ throw and _Unchecked Exception_ because there is a bug in the code.

##### Unchecked Exceptions - DRAMA

RuntimeExceptoin, Error, and their subclasses do _not_ have to be caught by Try-Catch blocks in Java.

It is not necessarily _correct_ to inherit your custom Exceptions from RuntimeException.

It is not necessarily _correct_ to throw _only_ unchecked exceptions either.

Any Exception that can be thrown by a method is part of the method's public API, therefore callers _must know about the exceptions that the method could throw_ so they can be handled.

RunTime Exceptions are a result of programming problems (bugs) and therefore should be managed accordingly, rather than just de-facto thrown (or ignored/bypassed).

Recommendations:

1. Do not throw a RuntimeException to create a subclass of RuntimeException simply because you don't want to be bothered with specifying the exceptions your methods _can_ throw.
2. If a client can reasonably be expected to recover from an exception, make it a _checked exception_, otherwise use an _unchecked exception_ (the client couldn't do anything with the exception anyway).

Recommendations were lifted almost verbatim from [Unchecked Exceptions - The Controversy](https://docs.oracle.com/javase/tutorial/essential/exceptions/runtime.html)

Oracle wrote some code that basically washes away an unchecked exception situation during a type casting operation, here is the example:

```java
@SuppressWarnings("unchecked")
static <T> WatchEvent<T> cast(WatchEvent<?> event) {
    return (WatchEvent<Path>)event;
}
```

- `@SuppressWarnings` decorator tells the compiler to not show the 'unchecked' warning message at compile time.
- The generic static function performs the casting operation, forcing the Type to be `Path` instead of the _unbounded wildcard_ that is allowed in the input parameter.
- This is not recommended, but it demonstrates a way to work around the unchecked warning.

#### Advantages of Exceptions

- Separate error-handling code from all other code => Ordinary processing and operations are easily distinguishable from error-handling code
- Propagate Errors up the Call Stack => JRE searches _backward_ through the call stack to find methods for handling Exceptions
- Group differentiating error types => The Exception Classes hierarchy enables grouping/categorizing execptions

#### Read Learn Write Finally

Try: Identifies code in which an exception could occur.  
Catch: Identifies code that is an "exception handling" codeblock.  
Finally: Identifies code that is _guaranteed to execute_, used for closing files, recovering resources, and performing other cleanup from anywhere in the previous code blocks.

### How To Handle InterruptedException

Notes while interpreting this [Baeldung](https://www.baeldung.com/java-interrupted-exception) article.

Multi-threaded Exception handling class.

Multiple theads are executed simultaneously.

Main Thread: The usual, default starting Java thread - main().

Threads run in the same memory space (lightweight) and can communicate amongst themselves.

Thread Lifecycle:

1. Start => is Runnable AKA New thread
1. Runnable => scheduling via `.start()` results in Running
1. Running state branches: Wait for Lock, Sleep/Wait, and Stop/Exit.
1. If Wait For Lock => Blocked until Lock Acquired, meaning cannot access code currently used by another thread, when released then return this thead to Runnable.
1. If Sleep/Wait => Enters this state from `.wait()` method call or signal from another thread. Waiting until Notify/Resume called then return to Runnable.
1. If Stop/Exit => Transition to Terminated state. Terminated could be an abnormal exit state.

InterruptedException is thrown when a thread is interrupted from SLEEP or BLOCKED (possibly others).

InterruptedException is a _checked exception_, so blocking operations will throw it.

Interrupts: A _request_ framework that allows thread to ask other threads if it can execute now. Also indicats to the Thread to 'stop current activity and do other work'.

InterruptedException can be thrown via methods:

- sleep()
- join()
- wait()
- put() - of a BlockingQueue
- take() - of a BlockingQueue

Thread class methods dealing with Interrupts:

```java
public void interrup() { ... } // allows asking to interrupt this thread
public boolean isInterrupted() { ... } // ask if thread has been interrupted
public static boolean interrupted() { ... }
```

Credits for Java code _[Baeldung Interruption Methods in Threads (see References)]_. Comments are mine.

InterruptStatus Flag: A boolean Field in each thread representing the status. Set by Thread.interrupt().

Scheduling: This is JVM-dependent. JVM versions and OS type will alter exactly how interrupts are implemented.

Deadlock: A situation where code does not handle Thread Interrupts properly.

Strategies to avoid deadlock:

- Propagate InterruptException up the call stack. Use 'throws' keywords to each method, indicating to the calling method that it needs to handle the thrown exception. Causing method could not-catch or could re-throw to the caller.
- If Thread is in state "runnable" the Exception cannot be propagated, instead the interruption must be preserved. See Baeldung code for example code.
- Utilize custom Exception handling: An example of this is to close resources before terminating the thread.

#### Capturing Exceptions Especially in Tests

Utilize a lambda to call the throwable and store the return value of 'assertThrows' in an Exception type variable.

```java
Exception actualException = assertThrows(MyCustomExceptionClass.class, () -> sut.throwMyException());
assertTrue(expectedException, actualException);
```

It is also possible to test that the exception handling is passing on the interrupted status, but using a custom method that throws the exceptoin type and testing for boolean True or False.

## Additional References

Baeldung [code repo](https://www.baeldung.com/java-checked-unchecked-exceptions) on Checked and Unchecked Exceptions.

Baeldung on [Threads and InterruptedException](https://www.baeldung.com/java-interrupted-exception)

Java Docs on [ExecutionException](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ExecutionException.html)

A way to supress Unchecked Error during compile time in subsection "Retrieving the File Name" in Oracle Java Docs on [Essential IO Notification](https://docs.oracle.com/javase/tutorial/essential/io/notification.html)

## Footer

Return to [Parent Readme.md](../README.html)
