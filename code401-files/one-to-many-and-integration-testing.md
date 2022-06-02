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

