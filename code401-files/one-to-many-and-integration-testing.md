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

