# Java Facts To Remember

## What

Not everything needs to be recorded here.  
Consider this a quick-ref or study guide to help learn key facts that will help learning, and coding with, Java.  

## Gradle

You can use Gradle to "set up" a project for Java development.  

1. Create new project folder and CD into it  
2. Type: `gradle init`  
3. Respond: `application`, `Java`, `Groovy`, `JUnit4`, `single application project`  

### Gradle Settings

settings.gradle(.kts)

Assign name to build, overriding default behavior of naming build after PWD: `rootProject.name = ''`  

Define the build is a single subproject ('app' in this case) containing code and build logic. Use 'include ...' statements to add other projects: `include('app')`  

Other remarkable items in the config:

plugins: Apply plugin to support building CLI app in Java  
repositories: Define how to resolve dependencies e.g. Maven Central  
dependencies: Define testing framework  
application: Dependency used by the app  
tasks.named: Defines main class for the app  

### Generated Files

`$app_name.java` is created automatically with a `public static void Main(args[]){}` entry function.  
`AppTest.java` is generated to start-up a class file that will contain unit tests for the app.  

### Gradle Run

Run your app from within the PWD to view *app* output and other task results `> ./gradlew run`  

### Gradle Build

Build your app from within the PWD and view *task* output: `> ./gradlew build`  

## Classes

## Variables and Types

Type => is-a => memory
byte  number  1 byte
short number  2 bytes
int number  4 bytes
long  number  8 bytes
float number  4 bytes
double  number  8 bytes
char  character 2 bytes
boolean true/false  1 byte

## Defining Assigning Casting

Variables must be defined before they can be assigned to.  
Combine definition with assignment in one line as necessary.  

Cast a variable as a float type:  

- Conversion: `float myFloat = (float)4.5;`  
- Cast: `var myFloat = 3.7f;`  

## Operator Overloading

*Only* allowed in class *String*.  

## Footer

Return to [Parent Readme.md](../README.html)  
