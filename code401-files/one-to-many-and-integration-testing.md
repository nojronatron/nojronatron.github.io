# Reading Notes for Class 13

Related Data in Spring: [One-to-Many Relationships](https://www.baeldung.com/spring-data-rest-relationships)  

Spring [Integration Testing](https://www.baeldung.com/integration-testing-in-spring)  

## One-to-Many Relationships in Spring

Spring Data REST expolses association resources for a repository.  
Entity Classes are classes that have the following attribute syntax added:  

- `@Entity`
- `@Id` and `@GeneratedValue`
- `@Column` which might include indicators in parenthesis like `@Column(nullable=false)`  
- `@OneToOne` and `@JoinColum(name-value:pair)` and might have `@RestResource(path=path, rel=address)`
- `@OneToOne(mappedBy = string_item)` to map a property to a table column?

*Note*: Carefully pick different names for each association resource or exception "JsonMappingException" with message "Detected multiple association links with same relation type!..." will be thrown.  

Expose entities as Resources:

1. Create repository interfaces for each entity by extending CrudRepository interface.  
2. Use PUT and GET calls to "create associations and verify that association between the associated resources.  

*Note*: Use DELETE to remove an association.  

### One-To-Many

Use `@OneToMany` and `@ManyToOne` annotations.  
Optional: `@RestResource` annotation to customize associated resource (see above).  
When defining a Many To One relationship:

```java
@ManyToOne
@JoinColumn(name="col_name")
// Property definition here

// then on the other side of this relationship:

@OneToMany(mappedBy="other_col_name")
// Property definition here
```

*Reminder*: How to create a Class Repository:

```java
public interface MyRepository extends CredRepository<MyClass, IdColType>{}
// IdColType e.g. 'Long' as in the Type
```

To add an Entity to a Table, a POST method is necessary, and the Controller needs to instantiate the Entity based on the input from the web-request.  
The new Entity instance can be assembled within a JSON Header (Content-Type:application/json) and the Controller can then send an appropriate response.  
Behind the scenes, Spring Framework talks to the DB interface and tries a CREATE call, adding the entity values to the correct table(s) in the database.  

-- -

Verifying an entity has been stored in the DB is done through a Controller with a GET route.  
A GET call is used to select a *single or many* entities => Single by ID or perhaps name; Many meaning ALL or a limited number through some coded restriction like a filter expression.

-- -

Many-to-many relationships are build using the `@ManyToMany` annotation, inconjunction with @RestResource.  
The association needs to be established in *both* entities where Many-to-Many is relationship is true.  

### Repositories

To manage Entities, Repositories are needed, one for each Entity that represents a Table in the DB.  

```java
public interface MyclassRepository extends CrudRepository<Myclass, Long>{};
```

### Testing Rest Endpoints

TestRestRemplate can be used for this.  

See [Baeldung.com for more](https://www.baeldung.com/spring-data-rest-relationships)  

## Integration Testing

Verifies End-to-end behavior of a system.  
Spring MVC Framework suports integration testing with mocking.  

### Dependencies

- JUnit Jupiter Engine and API
- Spring test
- hamcrest library
- json path

### Config

Use `@ExtendWith` annotation with test classes and include the extension class to load.  
Use `@ContextConfiguration(location={""})` annotation to load and boostrap the test context the test will use.  
Use `@WebAppConfiguration(value="")` loads the web app contenxt.  
Wire webapp context directly into a test using `@Autowired` followed by the property `private WebApplicationContext webAppContext;`  

### Mock MVC

Encapsulates all web application 'beans' and makes them available for testing.  
An example from Baeldung.com:

```java
private MockMvc mockMvc;
@BeforEach
public void setup() throws Exception {
  this.mockMvc = MockMvcBuilders.webAppContextSetup(this.webApplicationContext).build();
}
```

The Baeldung.com article recommends verifying the test configuration before continuing.  

### Writing Integration Tests

1. Use static imports from MovkMvcRequestBuilders or MockMvcResultMatchers classes.
1. Build the `@Test` code and call `this.mockMvc.perform(get("$.path")).andDo(print()).andExpect(view().name($.message));`
1. Add Assert* syntax if needed to test other portions of the sut.  

Use `$.varName` to place-hold variables in the test code.

Verify Response: `.andExpect(status().isOk())`  
Verify JSONPath message value: `.andExpect(jsonPath("$.message").value("expected message!"))`  
Verify Content-Type: `.andExpecte(content().contentType("application/json;charset=UTF-8"))`  

*Note*: You *can* write an empty 'return' keyword at the end of these tests.  

### Limitations of MockMvc

1. Relies on subclass 'DispatherServlet' to handle test requests, but MockMvc wraps it, using DispatcherServlet directly, so no *real* network conenctions are made, so it is impossible to test the entire network stack (or the 'conversation').  
1. Spring prepares a *faked WebApp* context to mock HTTP Reqs and Res's, not all features (of a full-blown app) are supported, e.g. no real support for "Http Redirections", which will make testing some API failures (that rely on Http Redirects) impossible.  

Use "RestTemplate", "REST-assured", or some other concrete test Context to work around these limitations.  

## Footer

Back to [Root Readme.md](../README.md)  
