# Read Class 18

Many to Many relationships.

An interesting read on Security.

## Spring Hibernate and Many to Many Relationships

Entity Relationships are the n-to-n associations between two entities, or tables in a database.

A Team Member can be a part of multiple Projects, and a Project can have many Team Members working on it.

Each table has their own Primary Key.

To form the relationship, the local table will have a "Foreign Key" that points to the other table's Primary Key.

When setting up tables for many-to-many, SQL commands can be used, or a UI like PgAdmin4 or SQL Server Management Studio (choose your poison).

The Classes in code must be set as Entities using `@Entity` annotation at the Class definition.

Optionally, `@Table(name="table_name")` can be added at the Class definition to point to a specific table, which is useful when the could otherwise be a naming clash in the database.

Use the annotation `@ManyToMany(cascade={CascadeType.NNN})` prior to joining tables within the Class.

Use the annotation `@JoinTable(...)` to define the joining SQL commands within the parentheses.

A HashSet is defined as the pluralized Property of the Class e.g. `Set<Project> projects = new HashSet<>();`

On the other side (the foreign Entity) the `@Entity` and `@Table...` and `@ManyToMany(mappedBy="previous_table")` annotations are used, and a HashSet is definied as the pluralized Property of the foreign Class e.g. `private Set<TeamMember> teamMembers = new HashSet<>();`

### ManyToMany JoinTable and JoinColumn Annotations

[ ] Use `@ManyToMany` on both Entities to create the relationship.
[ ] The 'owning' side of the relationship is `@JoinTable` annotation Class.
[ ] The Join code defines how the tables are related following `@JoinTable` annotation.
[ ] Use the 'mappedBy' attributes indicates this Class is the foreign table.

### Testing a ManyToMany Relationship

See the unittest [example at Baeldung.com](https://www.baeldung.com/hibernate-many-to-many)  

## USENIX Article on This World of Ours

Very fun article.

Key takeaways:

- Think about chain-of-trust.
- Decide what is most important to you.
- Even the most well-trained and practiced security minds have not gotten computer security right.
- The not-so-washed masses know the previous bullet point to be true and leverage it everyday.
- The world, crazy as it is, can be fun and entertaining.

## References

Spring Hibernate Many to Many [Annotation Tutorial](https://www.baeldung.com/hibernate-many-to-many)

Harvard Scholar University - USENIX ";Login:logout" Article [This World of Ours](https://scholar.harvard.edu/files/mickens/files/thisworldofours.pdf)

## Footer

Return to root [Readme](../README.html)
