# Read Class 33

One-to-Many and Many-to-Many Relationships in GraphQL in AWS Amplify.

CompletableFuture in Java.

## References

GraphQL API on [Docs.Amplify.aws](https://docs.amplify.aws/cli/graphql/data-modeling/#has-many-relationship)

Baeldung [Guide To Completable Future](https://www.baeldung.com/java-completablefuture)

## GraphQL API

DynamoDB tables for GraphQL types are created automatically using '@model` directive in the Schema.

## One To Many

Releationships between '@Model's are formed using directives:

- '@hasone'
- '@hasMany'

Use '@hasMany' to devine one-to-many relationships.

Retrieve related content from a source record using '@hasMany'.

Add '@hasMany' to the parent model's field that needs to have many items referenced within it.

An FK relationship is created (under the hood) from the '@hasMany' directive.

A secondary index can be specified using '@index' directive at the child model's related field.

This generates the appropriate Mutation code!

### Bi-directional Has One Relationship

Unavailable in iOS due to Swift language limitations.

Use '@belongsTo' on the child model's field to the parent's model's '@hasOne' field.

This generates Mutation and Query code to implements the relationship on the data.

### Bi-directional Has Many Relationship

Similar to Bi-directional Has One Relationship, implement '@hasMany' (instead of '@hasOne') on parent model field, and '@belongsTo' on child model field.

This generates Qureies and Mutations code that implements the relationship on the data.

Alternate Way: Implement a custom field that stores reference to parent object.

### Many-To-Many Relationship

The parent '@model' model's Field needs the '@manyToMany' directive on it.

The child '@model' model's Field needs the '@manyToMany' directive on *it*.

This generates a *join table* codefile named after 'relationName' argument in both directives.

Queries and Mutations are also generated that enable retreival on FK records from either parent model/table.

### Other Notes

Default values can be assigned to fields.

Generated Queries, Mutations, and Subscriptions can be *renamed*.

Generated Queries, Mutations, and Subscriptions can be *disabled* by setting their value to 'null'.

Custom Queries can be implemented.

Customized creation and update timestamps can be implemented. '@model' causes default 'createdAt' and 'updatedAt' field generation under the hood. Pass-in the timestamps attribute to the directive to customize them.

A *Subscription* is a 'real-time update' schema.

Access level to Subscriptions can be edited.

Multiple relationships can be configured between models.

Tables are called on your behalf using the IAM User configured when AWS Amplify was set up.

There is a default limit of 100 records returned per Query, but it is adjustable.

## Baeldung Completable Future


## Footer

Return to [Root README](../README.md)
