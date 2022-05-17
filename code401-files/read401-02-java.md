# Read Class 01

## Reference Sources

[Programiz tutorial on Java Packages](https://www.programiz.com/java-programming/packages-import)  
[Baeldung guide to Java Loops](https://www.baeldung.com/java-loops)  

## About Java Packages

Java Packages are containers with types (classes and interfaces and so-on) that are easily maintainable and can be utilized by other code.  
Java *Projects* allow only one Class Name type per project.  
Packages are named using qualified naming schemes to help separate similarly (or same) named classes, for example:  

```java
import java.util.Date;
import java.sql.Date;
```

The above are 2 different classes.  

### Two Categories of Packages

Built-in: Packaged with a JDK.  
User-defined: Packages users create following a set of rules and principals.  

### User Defined Packages

Keyword: Package. Follows strongly-named scheme: `com.test`  
Directory structure follows strongly-named scheme: `./com/test/CustomApp.java`  
Create the Class within the package: `class test { public static ... }`  
The package hierarchy is of unlimited size.  
IntelliJ IDEA can create packages (rClick source folder, select New => Package, enter package name). File system is created automagically.  

### Import Statement

Use the import statement to "bring in" code from Java Packages.  
Packages can import other packages.  
To import package(s) from a user-defined package:  

```java
package package.name;
import package.ClassName;
class MyClass {...}
```

## Loops in Java

Use loops to repeatedly run code statements repeatedly.  
Control structures that use a boolean test to determine when to stop executing the following code block.  

### Types of Loops

For: Repeat operations through inc/decrementing a counter.  
For-Each: Selects each item in an iterable, one at a time, until all iterable items have been selected once.  
While: Depends explicitly on a boolean test as the exit criterial.  
Do-While: Same as 'while' but one iteration of execution occurs *prior to* the boolean test is evaluated.  

## Footer

Return to [Parent Readme.md](../README.html)  
