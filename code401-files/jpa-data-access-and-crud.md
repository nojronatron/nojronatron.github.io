# JPA Data Access and Spring CRUD

## References

Spring [Accessing Data with JPA](https://spring.io/guides/gs/accessing-data-jpa/)  

Baeldung [Spring Data Repositories and CRUD](https://www.baeldung.com/spring-data-repositories)  

## Accessing Data with JPA

Build an example app with JPA.  

### Requirements

- Favorite IDE
- JDK 1.8 or later
- Gradle 4+ (or Maven 3.2+)

### Spring Initializr

- pulls in dependencies needed for this example project
- select Gradle (for this class)
- In dependencies select "Spring Data JPA" and "H2 Database"
- Generate and download the Zip

### Entities

Objects that are annotated with specific syntax:

- Entity: '@Entity' defines a public class as a JPA Entity
- ID and GeneratedValue: '@ID' and '@GeneratedValue' define the property that follows to be a unique DB-ready ID, as defined at the database  
- Table: '@Table' would be added if the Entity Name did NOT match the Class name  

### Annotations and Beans

`import org.springframework.context.annotation.Bean;`

### Queries

Spring Data JPA stores data in relational databases.  
A Repository interface is used to implement a means to work with a database.  
Methods that allow saving, finding, and deleting your Class 'entities' are inherited.  
Simply declaring method signatures enables using the inherited member e.g. `List<Customer> findByLastName(String lastName);` is all you need!?!  

### Creating an Application Class

Initializer creates a simple class for an App.  
Annotations overview:  

`@SpringBootApplication` - Convenience annoation adds the following annotations  
`@EnableAutoConfiguration` - Adds 'beans' based on classpath settings (and other beans, and other property settings).  
`@ComponentScan` - Spring will look for other components, configs, services in 'com/example' package so it can find Controllers.  

### Main

'SpringApplication.run()` is Springs under-the-covers execution member for the usual 'main()' entrypoint of this App.  
No Web.xml file needed any longer!  

### Logger Factory

There is a *logger factory*!!!  

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
// etc
```

### Build A JAR

Use Gradle or Maven - same as noted in other readmes:

```sh
./gradlew bootRun

# or ./gradlew build then run
java -jar build/libs/app-file-name-v-n-n.jar
```

## Baeldung CrudRepo with JPA and PASR in Spring Data

### CRUD Repository

Provides CRUD functions.  
Simplest of the three, and can be used without the other 2 at all.  
Create an Entitiy:

```java
@Entity
public class MyClass {
  @Id
  private long id;
  private String thingy;
  // other members
}
```

Define an Operation:

```java
@Repository
public interface ProdRepo extends JpaRepository<T, U> {
  MyClass findByName(T thing);
}
// Spring Data Repo will auto-gen the implementation based on the name provided!
```

CrudRepository Interface:

In generic.  
Implements inheritance (uses 'extends') and down-casting.  
Defines: findOne, findAll, count, delete, exists, and save(S entity).  

### Paging And Sorting Repository

Provides methods to paginate and sort records.  
Concentrates on Generic findAll(Sort sort) and findAll(Pageable pageable) methods.  
Pageable object has members: Page size, Current page number, and Sorting.  
*Note*: First parameter of PageRequest is zero-based.  

### JpaRepository

Provides methods like 'flushing' and 'persistence context' and 'delete records in a batch'.  
Interface dnables the following functionality:

```java
findAll with overload findAll(Sort sort)
save(Iterable<? extends T> entities)
flush()
saveAndFlush(T entity)
deleteInBatch(Iterate<T> entities)
```

Each method is directed toward operations upon single or collections of Entities *in a database*.  

## Downsides of Spring Data Repos

- Your code gets tightly coupled to the abstractions used.  
- Must take care to not expose the implementation details of the interfaces.  
- Extending CrudRepository exposes all methods, when only some of them are actually necessary or wanted.  

## Footer

Return to [Root Readme.md](../README.html)  
