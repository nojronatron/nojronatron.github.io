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

*Emulator Requirement*: Must set the phone Emulator API to (32?).

See [Android Developer Docs](https://developer.android.com/training/data-storage/room#java)

Database Inspector:

- Requires API 26 or Higher

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
- Add an ID Field and set as "Primary Key": `@PrimaryKey(autoGenerate=true)`

Create a DAO for the Entities:

1. Create a DAO *interface* to represent Entity/Entities.
1. import packages: androidx.room.?: Dao, Insert, Query
1. Decorate the class with @Dao
1. Decorate a create method with @Insert: `@Insert public void insertEntity(Entity entity);`
1. Decorate a FindAll method with @Query: `@Query("SELECT * FROM Entity ORDER BY field ASC") public List<Product> findAll();`
1. Decorate a FindByAnId method with @Query: `@Query("SELECT * FROM Entity WHERE id = :id") public Entity findById(Long id);`

An DAO can use GENERICS!

- "One Purpose DAO" will force a single Entity by Type.
- Utilizing a Generic could enable DRY, single-use interface methods.

Create a Database Representation:

1. Create a Database Package.
1. Create a public Abstract Class named appropriately because it should not be instantiated.
1. Extend RoomDatabase object (see docs).
1. Add '@Database(entities={class1},{class2},{...etc}, version=1') annotation to the abstract class declaration. This will tell the DB what Tables it needs.
1. INSIDE THIS CLASS add the DAO by creating an abstract method: `public abstract EntityDao entityDao();`

Create DB Converters Class:

1. Add this new class to the database Package.
1. This will be a public class.
1. Use '@TypeConverter' annotation above the methods (see code snippet example below).
1. Create a method to go back-and-forth between the conversion types.

```java
// this converts timestamp to date
@TypeConverter
public static Date fromTimeStamp(Long value) {
  return value == null ? null : new Date(value);
}

// this converts date to timestamp
@TypeConverter
public static Long dateToTimestamp(Date date) {
  return date == null ? nul : date.getTime();
}
```

Create a Database now that the boilerplate DB interface layer code is done!

1. Set variables to represent the Database DAO as a Field.
1. Work within the OnCreate() lifecycle method.

Set variables for what will be needed/injected:

- Database Package classes
- Public static final String DATABASE_NAME = custom-name

Within OnCreate() method on the MainActivity:

1. Assign new Room methods to the abstract Database Class.
1. Room.databaseBuilder(// many methods and props and vars here) build-out the database safely.

#### Threading

In production environment, you *must set up multi-threading* so that DB queries do not lock the UI.

For this class, we are going to set "AllowMainThreadQueries()" to avoid DB setup and use errors using Rooms.

For AWS *Multi-threading will be utilized* and will not require AllowMainThreadQueries() at all.

### Save and View DB Items

Once you reach a point where you can build and run the app without errors:

1. Open App Inspection in IntelliJ IDEA.
1. Open DB Inspector to view Tables.
1. Open Table by dbl-click to view the data.

Set Up a Spinner Element:

1. In the AddItemActivity define a set up spinner method (see example snippet below).
1. Grab a reference to the Spinner element.
1. Set an Adapter to handle logic of the Spinner element.
1. Create a new ArrayAdapter<> with context 'this' comma R.layout.simple-spinner-dropdown-item
1. An array of items *must be provided*: See the posted class repo code.

*Optional*: Add the selectable items into you XML Resources, but this is not a scalable solution like Enums can be.

*Optional*: Use explicit casting "(Spinner)" to ensure ref is captured.

1. Define a private void method to handle storing a new data item.
1. Instantiate a Button instance e.g. Save button.
1. Create a new setUpSaveButton() method to set up Spinner, Button, and set a new onclick Listener.
1. Create a ~~lambda~~ onClick(View view) Event Listener to:
1. Find by ID to get name input of the Task (or thing).
1. Create a new product name and product description based on what was selected.
1. Apply any new data to local variables.
1. Call the Product CTOR and fill it in!
1. Remember to inject the database Field into this method so DB operations can be done within it.

*Note*: When casting to ensure types are correct, use parenthesis to enforce order-of-operations - likely you are trying to write multi-line statements onto a single line.

*Enum Notes*: Define it as a child to the class that needs it, and include toString() and fromString() methods to ensure it can be called.

*Tracking Element IDs*: Use the XML to more rapidly find and copy/past IDs, rather than the rendered UI.

*Required*: You must get a reference to the Spinner UI element in order to do anything with it.

#### Snackbar

Belayed until another time.

#### OnResume

Remember anything you put into OnCreate()? Those are stuck in the Lifecycle.

Use `super.onResume();` and add use clearn() and getAllItem() etc to load the Fields on *subsequent* times the Activity is loaded.

Tell RecyclerView that data has changed behind it without the Adapter being scoped to the Class level e.g. `ProductListRecyclerViewAdpater plrvAdapter;` and then use that Field within Class.methods().

### Expectations for Today

Code Challenge: Time box to no more than 2 hours! (me):

- Create a new Package for Sorting.
- ONLY work with Integers don't worry about everything else.
- Pseudocode => How an insertion sort works.
- Sample arrays.
- Provide whiteboard of the pseudocode activities (required!).
- Develop code based on pseudocode.

Lab 29: Room => Task Model and Room, Add Task Form, updates to Home and Details pages. Stretch goals (2, optional).

## Tuesday Morning

All AWS, today and tomorrow.

Host mobile apps using AWS Amplify.

### Insertion Sort Whiteboard Review

When you write "Edge Case" on your technical whiteboard, think of it like this: "What are the 'edges' of the data/inputs and outputs that my function has to deal with?"

Always good to include a step-through.

Use colors to identify areas of a step-through such as iterations the step-through step is in.

Remember to add test-case handling in your pseudocode.

### Merge-Sort Code Challenge

Make sure you whiteboard this! Even if coding doesn't happen, have a whiteboard ready for Weds morning discussion.

### AWS Amplify Part 1

There are dozens of AWS Cloud Services, many devs know 1, we will have experience with 4 by the time we graduate.

AWS is a collection of APIs and platforms to provide services.

SNS: Automate (or manual) message-sending service.

Elastic Beanstalk: Like Heroku but charges money.

Can create a budged in the Billing Console > Budgets window, and make sure it applies to *all AWS Services*.

*Note*: A budget and alerts in AWS Billing Console has been set up!

#### Remove ROOM

1. build.gradle: Remove ROOM references.
1. Remove TaskManager Database class: Say yes to removing the references.
1. Delete the DAO Class implementation (TasksDao.java).
1. Model: Remove '@entity' and primary key annotations from the model class(es).
1. Enter each Activity and remove references to Database Variables.
1. It might be necessary to refactor some custom methods in order to remove the database references completely, so comment-out code and leave TODOs for what needs to be revisited.
1. The TypeConverter might have a problem because it was annotated along with the DB and Room stuff.
1. Consider doing an Emulator "Wipe" command by closing the Emulator and selecing the 'Wipe Data' menu item in the emulated phone's entry in the Device Manager.

#### AWS Amplify Management CLI

Read the docs on how to [download and install](https://docs.amplify.aws/cli/)

Commands:

- status:
- add: Add category item, like API or other AWS Service.
- push: Push to cloud.
- console:
- publish: Publish bits in cloud to service.

##### Create an IAM User

1. Logon as Root user.
1. Open the Identity and Access Management view > Users
1. Download the AWS Amplify CLI

*Note*: AdministrativeAccess-Amplify is selected by default, DE-SELECT IT and just select AdministrativeAccess.

*Note*: DOWNLOAD the CSV of the newly created users. This will be necessary in the AWS CLI console when logging in.

#### Setup AWS Amplify on TaskManager

Update build.gradle scripts at the Project level and the App level to support AWS Amplify.

The AWS Amplify getting started document has a list of items that must be added to the Project's build.gradle.

#### GraphQL

Checkout the graphql.org [Learn Files](https://graphql.org/learn/queries/)

GraphQL notes:

- Depth Level can be adjusted beyond 2.

#### Lambdas

Detects specific ACTIONS, and perform processing when the Action occurs.

### Tuesday Assignments

- [X] Write at least 3 Espresso Tests.

- [X] Merge-sort: Whiteboard completely. Coding is your choice.

## Wednesday 29-June

Is Data CIA? Stored Confidentiality, with Integrity, and Available?

Cloud Pros:

- Accessibility
- Security
- Automation
- Scalability
- Save space on local
- No hardware in my house/managing own servers

CLoud Cons:

- Malicious code
- Latency
- Needs INTERNET

### Integrating AWS With Android App

After installing Amplify, additional folders are put in your Project.

GraphQL will also add folder and files including a Schema json, queries, etc.

step to convert from Room to Amplify w/ GraphQL:

1. deleted db and daos
1. delete your model
1. remove all annotations and imports from your files
1. add amplify dependinces into gradle
1. add atskmasteramplifyapplication to extend app
1. put amplify config into above app file
1. update graphql schema (then api update on cli, after success then push w/o conflict resolution)
1. run amplify codefen models to generate them locally
1. delete old model and convert every usage in your app
1. every dao usage needs to be converted to aplify api usage
1. change recyclerviewadapter to have better string output

From Instructor Alex:

```java
  // Steps for adding Amplify to your app
  // 1. Remove Room from your app
  //   1A. Delete the Gradle Room dependencies in app's (lower-level) build.gradle
  //   1B. Delete database class
  //   1C. Delete DAO class
  //   1D. Remove `@Entity` and `@PrimaryKey` annotations from the Product model class
  //   1E: Delete the database variables and instantiation from each Activity that uses them
  //   1F: Comment out DAO usages in each Activity that uses them
  // 2. Make an IAM user
  // 3. Run `amplify configure`
  // 4. Add Amplify Gradle dependencies in build.gradle files
  // 5. Run `amplify init`
  // 6. Run `amplify add api` (or `amplify update api`)
  // 7. Run `amplify push`
  // 8. Change model in "amplify/backend/api/amplifyDatasource/schema.graphql" to match your app's model
  // 9. Run `amplify api update` -> Disable conflict resolution
  // 10. Run `amplify push --allow-destructive-graphql-schema-updates`
  // 11. Run `amplify codegen models`
  // 12A. Add an application class that extends Application and configures Amplify
  // 12B. Put the application class name in your AndroidManifest.xml
  // 12C. Uninstall the app on your emulator
  // 13. Convert every usage of model classes to use Amplify generated models in app/src/main/java/com/amplifyframework/datastore/generated/model
  //   13A. Instantiate classes using builder
  //   13B. Get data elements via getters (if you aren't already)
  // 14. Convert all DAO usages to Amplify.API calls
  // 15. Update RecyclerView adapter's collection via runOnUiThread()
  // 16. Fix date output in RecyclerView items
```

### Wednesday Lab

Add Task Form, refactor your homepage recyclerview, and get Amplify up and running.

Remove Enum from the project, add a hard-coded list of Strings that represent all the categories.

Spinner code might have to be altered to utilize the list instead.

Remember to utilize onResume property to ensure re-vising views are updated with Amplify + Dynamo latest data.

### Code Challenge Quick Sort

No deductions for late submissions.

Most complex of all sort algorithms.

JS Array.sort() uses Quicksort.

Quicksort is a common interview question.

## Thursday June-30

AWS and Billing:

- Check this regularly.
- Set notifications/alerts so billing activity isn't missed.
- Free Tier lasts for 1yr or reaching max threshold, whichever comes first.
- Relational DB is one place that is likely to accumulate charges.

### Quicksort Whiteboard Review and Comments

Final Technical Whiteboard and Interviews will require camera on.

Put your working screen under the camera so your face is head-on with the camera feed.

Pivot:

- There are a few ways to approach this, some will pick a worst-case starting point, others will do better.
- Consider the pivot point (partition method?) as a statistically likely good spot to start.
- Middle or a randomly selected integer might keep the algorithm from picking the worst case scenario.

Managing Quicksort Temporary Placeholders:

- Use a Stack.
- Quicksort in-place.
- Tightly-scoped local variables e.g. Temp.

Variable LOW is used to track how many values are less than the PIVOT point.

### Relational Data in GraphQL

One => Many and Many => One

*Note*: Many to Many is a Left-Join SQL in the end.

Use the schema.graphql file to build new table(s).

Create a new 'type', name it, and utilize directives '@model', '@auth' etc.

```java
type Contact @model @auth(rules: [{allow:public}]) {
  id: ID!
  email: String!
  fullName: String
  products: [Product] @hasMany(indexName: "byContact", fields: ["id"])
}
```

Update Product to enable the FK relationship:

```java
type Product @model @auth(rules: [{allow:public}]) {
  id: ID!
  name: String!
  description: String
  dataCreate: AWSDateTime
  productCategory: String
  contactId: ID! @index(name: "byContact", sortKeyFields: ["name"])
  contactPerson: Contact @belongsTo(fields: ["contactId"])
}
```

*Note*: Relationship descriptions API has been updated a little, is similar, but a lot cleaner.

When done editing Schema:

1. Update CodeGenModels 'amplify codegen models' in Amplify CLI.
1. Run 'amplify status' in the CLI.
1. Run 'amplify push' and answer the quesions according to your app requirements.
1. View the results in Amplify Admin UI after the PUSH operation completes.

When creating a new entity (Amplify Class) after setting up the schema:

1. Assign a variable of type that is the name of the Schema model.
1. The value will be a ModelName.buildeer() with chained commands that set the Fields, rather than using a CTOR.
1. Call Amplify.API.mutate() with args and callback handlers to call ModelMutation.create(variable_created_in_first_step).

```java
// sample code from Taskmaster project
Task task = Task.builder()
  .title(newTaskTitle)
  .body(newTaskDescription)
  .state(newTaskStatus)
  .build();
```

Amplify uses 'success' as a callback function.

Inside an Amplify success callback add:

- Create nice logging output `Log.i(string title, string message);`
- Process data such as creating a collection of model data from the DB.
- This works for filling a Spinner with data! Use code inside the onCreate() method to fill the spinner.

```java
// sample code from Taskmaster project
Log.i("", "Entered incrementTaskCounter lambda.");
TextView successText = AddTask.this.findViewById(R.id.submittedText);

// aws amplify graphql insert method
Amplify.API.mutate(
  ModelMutation.create(teamAlpha),
  response -> Log.i("HomeActivity", "Added Team with id: " + response.getData().getId()),
  error -> Log.e("HomeActivity", "Failed to create new Team", error)
);

finish(); // necessary to exit the lambda
```

*Note*: Review ApiModelname.java to see what the params are needed for Queries and Scaler methods!!

Grabbing a stream of a collection and filter it for a selected item (comparisonObj) and return it as an instance, else throw a specific exception:

`myModel.stream().filter(c -> c.getter().equals(comparisonObj)).findAny().orElseThrow(RuntimeException::new);`

### Completable Future

Similar to JS Promises, which are asynchronous methods.

Asynchronous is *not* procedural programming.

Asynchronous will take whatever time the longest call takes.

Synchronous will take the SUM OF ALL CALLS in order.

CompletableFuture is an asynchronous package.

`CompletableFuture<List<MyModel>> thingFuture = null;`

Closing methods are necesary: To resolve the CompletableFuture (e.g. tell it to complete) you must include '.complete(arg)'.

You *must* complete a CompletableFuture otherwise your app will hang, so Exceptions *must be handled*.

CompletableFuture Exceptions receive 2 params, the output (if processing completed) and the exception that was thrown.

To capture the exception write the 3rd parameter like:

```java
failure -> {
  mymodelFuture.complete(null);
  Log.e(String logTitle, String customMessage);
}
```

Another CompletableFuture exception type: InterruptedException.

*Note*: You might run into a 'null reference exception' when using CompletableFuture calls. How to deal with this? TBD

### Thursday Lab

Advice:

- Consider the logic you will need in order to view items from the DB filtered by specific Fields and Values (conditional rendering).
- You will be adding Teams so be sure to build-out the schema accordingly, with Queries and Mutations methods.

### Thursday Partnered Code Challenge

MUST BE PAIRED.

Treat as if this is the final technical interview.

### Other AWS Services

Cognito

DynamoDB

S3

## Friday Class Notes

### Career Coaching Workshop

1. Graduate!
2. Targeted Job Search.
3. Stellar Resume.
4. Informational/Recruitment Call. You might be asked for your target salary range.
5. On-site Interview. Tell me about yourself? Elevator pitch! Remain calm so knowledge access is possible.
6. Receive an offer! Prepare to decide whether to walk-away or how to accept.
7. Negotiation => Job Offer!

### Technical Spruce-up

GitHub:

- Keep doing what I'm doing.
- Employing a bot to make my commit history more green is not my gig.
- Enable Private Contributions.
- After 401, make non-showcase repositories private, but pin your *best projects*.
- Update your README at the root of your dashboard! (See HexxKing's repo on this topic).

### Tools and Online Editors for Collaborating and Proving

- [X] [replit.com](https://replit.com/)

- [ ] [CodePen](https://codepen.io/)

- [X] Google on [Sandboxing Code](https://developers.google.com/code-sandboxing)

- [ ] [code sandbox](https://codesandbox.io/)

- [X] [HackerRank](https://www.hackerrank.com/)

- [ ] [CoderPad](https://coderpad.io/)

- [X] Code Fellows advice to set up [GoogleDocs for Technical Interview](https://www.codefellows.org/blog/setting-up-google-docs-for-technical-interview-happiness/)

- [X] [Leetcode](https://leetcode.com/)

- [X] [CodeWars](https://www.codewars.com/)

### Graphs

These notes supplement [reading notes on graphs](graphs.html) in this repo.

Lots of examples of Graphs, generally, in the world.

Graph are interconnected data structures.

Nodes in Graphs are called Vertices.

*Note*: Try to stick with the accepted terminology so everyone is on the same page especially Vertices vs Nodes.

Root: The starting vertex when analysing and traversing a graph.

Potential Connections: Edges are connections, and Graphs have neighbors via edges. But not all Vertices are connected directly to all others.

Neighbor: Currently-adjacent Vertex.

Degree: Number of edges connected to a Vertex.

Traversals:

- Trees: Unidirectional traveling across edges between vertices.
- Graphs: Could be undirected, or directed unidirectional or potentially multi-directional.

Cyclic vs Acyclic:

- Cyclic means traversals can visit the same vertices multiple times.
- Acyclic means traversals are one-way and usually neighbor vertices are not visited more than ones.

Edges can have Weight:

- Relates the cost or importance, depending on the problem domain.
- Enables evaluating "best path" or paths between vertices.

### Code Challenge for Friday

Graph Implementation!

- add a node.
- add edge => Create a custom method addBidirectionalEdge() to help out.
- get nodes.
- get neighbors.
- traverse graph.
- size: return total vertices in the graph.

Remember left and right? These are edges!

Reference all edges like done in the kAry Tree!

Find vertices via Breadth First Traversal and return the collection.

Consider using a hashset or set to track visited vertices.

lucy-gelderloos

## References

Wikipedia article [Amazon Web Services](https://en.wikipedia.org/wiki/Amazon_Web_Services)  

Pseudocode Reference from [CSC Calpoly Institute](https://users.csc.calpoly.edu/~jdalbey/SWE/pdl_std.html)

## TODOs

[ ] TaskMaster: How to alter the background colors on Activities.

[ ] Android Studio: Create a macro to do common things like: Font resize/zoom.

## Footer

Return to [Root README.md](../README.html)
