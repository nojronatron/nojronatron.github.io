# Week 7 Class Notes

## Monday 27 June Notes

### Upcoming

Technical interviewing in 2 weeks, which will over prep us for most real interviews.

Continuation of Android dev using the Task Master app.

Using Rooms: Is an ORM (Object Relational Manager) + SQL Queries.

AWS Amplify on Tuesday and DynamoDB => AWS is a high-value skill set.

Advice:

- Use UML
- Draw wireframes
- Anything that can help you understand the connection points when developing a solution

TCP/IP and REST are common networking / WRRC techniques, regardless of the framework or language used.

Graphs: Not on final technical whiteboard. Abstract datastructure that things data together with 'paths'.

### Rooms

Room Database: Similar to the 3-liner JPA Code in Spring, but we will need to build our own Queries.

The App talks to the Room DB, and in parallel communities with the DAO (Data Access Object).

The DAO does "get entities", and persists data back to the DB.

Entities is the same as before, Classes with annotations and GET/SETters.

See [Android Developer Docs](https://developer.android.com/training/data-storage/room#java)

Database Inspector:

- Requires API 26 or Higher
- ...

SQL Lite:

- Very capable, widely deployed
- NOT a good choice for large numbers of concurrent WRITE operations
- Supports structured data and SQL Queries

Data Access Object:

- Similar to Repositories
- Requires we write so SQL Queries

Rooms Setup:

- In your MODULE build.grade add room_version, implementation, annotationProcessor
- Same place, optionally add testImplementation
- Gradle re-sync is *required*

Create Entities to model the data:

- New java class
- Remember to add getters and setters

Create an ENUM if one is necessary:

- New file, name + '.java' extension.
- Include package pointing to the package that the Entities will be stored in.
- See java snippet example below.

```java
// package reference here
public enum EnumName { 
  CATEGORY1("category1"), 
  CATEGORY2("category2"); 
  private final String someString; 
  // CTOR
  // getters, setters
  // @Override toString() or other overrides and custom methods as necessary
  }
```

Implement the Enum in the entity:

- As a Field: `EnumName enumName;`
- Add a getter and setter for all Fields including the Enum.

Adding Entity Decorators:

- '@Entity' at the class level.
- Add an ID Field except "Primary Key": `@PrimaryKey(autoGenerate=true)`



## TODOs

[ ] Android Studio: Create a macro to do common things like: Font resize/zoom.

## Footer

Return to [Root README.md](../README.md)
