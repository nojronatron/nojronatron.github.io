# Spring, Spring App, Spring MVC, and Thymeleaf

Notes taken while reading the reference materials.

## References

https://spring.io/guides/gs/serving-web-content/

https://www.thymeleaf.org/doc/articles/springmvcaccessdata.html

## Springboot

Requirements to build a simple website:

1. An IDE
1. JDK 1.8 or later
1. Gradle 4.0+ or Maven 3.2+

Helpful Utilities:

- Spring Tools Suite [STS](https://spring.io/guides/gs/sts/)  
- Also [Spring Initializer](https://github.com/spring-io/initializr/) for generating JVM Projects online  
- [Getting Started Guide](https://spring.io/guides/gs/intellij-idea/) for IntelliJ  

### Architecture Comments

Drop all static resource files into subfolder `/static` or `/public`  
The default index page is used (by default) as the root or home page of the webapp.  
Spring uses Controllers to render pages (like MVC). Annotation: `@Controller`.  
Each Controller defines a 'Route'.  
HTTP Web Requests are trapped and directed to "method_name" using annotation `@GetMapping`.  
Annotation `@RequestParam` binds QueryString value to a named parameter e.g. `@RequestParam(name="username", required=false, defaultView=String:default_value)`.  
*ThymeLeaf* performs server-side rendering of the HTML.  
String attributes are passed to the HTML file via elements with attribute `th:text` (expression).  

#### Spring Boot Devtools

Enables:

- Live Reload: Dev can edit the live project and rendered page will keep up without restarting.  
- Hot Swapping: Java JVM swapping (limited to certain bytecode variants, tbd).  
- Template Engine Switching (clears cache): (TBD)  
- Restarts via changes in ClassPath. Building in IDEA or using `maven compile` or `gradle build` forces a ClassPath change. Some IDEs may change ClassPath on *Save*. Additional paths can be configured to trigger restarts.  

Devtools is not enabled in a JAR, but can be enabled by setting properties in Maven or Gradle files e.g. 'excludeDevtools=false'  

### Setup

Utilize Spring Initializr: Select Project, Language, and Boot version, JAR/WAR file generation, and JDK version. Can also add "Dependencies". Generates a downloadable Zip file.  

### Dev Overview

Controllers
Templates

### Gradlew

### Creating and Running a Jar File

`./gradlew bootrun` and `./gradlew build` => Return an executable JAR file.  
JAR files are stored in the Project path 'build/libs/application-name-version.jar'  

## Thymeleaf

The following is a very high-level overview of Thymeleaf, based on the paged linked in References, above.  

### Controllers

Website paths, model data, and template views are considered a 'model map'.  
Thymeleaf takes a model map and transforms it into a Thymeleaf context object.  

### Attributes

Model Attributes are data that can be accessed during view execution.  
Context Variables are the Thymeleaf equivalent of Model Attributes.  

### Parameters

Request parameters can be viewed with `params` dot notation.  
Multi-valued Request Params can be accessed using bracket notation.  

### Session Attributes

Session atributes are accessed using `session.`  
Get direct access to 'java.servlet.http.HttpSession' object by using `#session`  

### Servlet Context Attributes

Shared between Requests and Sessions.  
Access them using `#servletContext.method`  

### Spring Beans

Beans registered with the Spring Application Context carry methods defined in `@Configuration`.  
Use Beans in the HTML via the 'th:text=` attribute.  

## Footer

Return to [Parent Readme.md](../README.html)  
