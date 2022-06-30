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

ASYNCHRONOUS PROGRAMMING IN JAVA!

Better than callbacks that are scattered throughout code or deeply nested - difficult to trace in either case, and error handling is poor.

CompletableFuture class and Future interface and CompletionStage interface.

- Defines contracts for asynchronous compuations steps.
- Compatible with synchronous (the default).
- Building block and framework.
- 50+ methods for composing, combining, executing asynchronous steps.
- Error-handling capability is included.

### Simple Future

Class CompletableFuture implements Future.

A future result can be represented by an empty CTOR instantiation.

```java
Future<Integer> asyncResult = myFunkyMethod(3, 5);
```

Get() method blocks current thread until result is provided.

```java
int result = asyncResult.get(); // this is a blocking call
```

To spin-off an async operation: Use Executor API.

Return an instance of 'Future' when peforming an async call.

Receiving method can call Future.get() to acquire the result from the async thread/execution.

Future.get throws *checked exceptions*:

- ExecutionException: Encapsulates an exception during async operation.
- InterruptedException: Thread execution of a method was interrupted.

### Encapsulated Computational Logic

How to execute code asynchronously? Use static methods:

- 'runAsync()': Create CompletableFuture instance out of Runnable functional type.
- 'supplyAsync()': Create CompletableFuture instance out of Supplier functional type.

Runnable and Supplier are functional *interfaces*.

Instances of Runnable and Supplier can be passed as lambda expressions (Java 8 and newer).

Runnable does *not* allow returning a value.

Supplier is *generic* that returnes a *parameterized* type.

```Java
CompletableFuture<Integer> futureResult = CompletableFuture.supplyAsync( () -> 12345);
```

### Processing Results in Async

Feed results from computations to a function.

Method 'thenApply()' performs this function-feed for you!

Returns a Future that holds a value returned by the function.

Use the functional interface 'Consumer' for return void operations that take a single parameter.

Method 'thenAccept()' receives a Consumer and passes it the result of another process.

Use 'Runnable' lambda to execute a non-returning function and use the 'thenRun()' method.

### Combining Futures

CompletableFuture instances can be chained.

Further chaining and combining is also possible.

Refered to as "monadic design pattern".

Chain to Futures sequentially using 'thenCompose()' method.

Differences:

thenApply: Work with a result of the previous call. Return type will be combination of *all calls* (nested).

thenCompose: Uses previous stage as the argument, and returns a *Future* with result directly (rather than nested like thenApply does).

### Paralelling Executiong

Use 'CompletableFuture.allOf()' static method to do so.

Will return *void* however.

Manually get the results of the Futures using 'CompletableFuture.join()' method (Java 8+) to get them.

### Handling Errors

Implement the throw-catch patterns using a special handle ethod.

Handle method receives 2 params: Result of computation (if finished) and exception thrown (if throw exists in chain).

Check out the sample code in the Baeldung article for specifics.

### Asnc Methods

Used to run a process in a separate thread.

Fork/Join is used under the hood, and additional terminalogy and understanding is necessary to get the gist of how async methods work.

About [Fork/Join](https://www.baeldung.com/java-fork-join)

### JDS 9 CompletableFuture API

Supports:

- delays
- timeouts
- subclassing
- many new instance APIs
- several static utility methods
- new function 'orTimeout()'
- new function 'completedOnTimeout()'

Baeldung's [GitHub](https://github.com/eugenp/tutorials/tree/master/core-java-modules/core-java-concurrency-basic) has source for the article.

## Todos

- [ ] Review 'Checked Exceptions' to learn more.

## Footer

Return to [Root README](../README.md)
