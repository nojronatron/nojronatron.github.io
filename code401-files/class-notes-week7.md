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

[ ] Write at least 3 Espresso Tests.

[ ] Merge-sort: Whiteboard completely. Coding is your choice.

## References

Wikipedia article [Amazon Web Services](https://en.wikipedia.org/wiki/Amazon_Web_Services)  

## TODOs

[ ] TaskMaster: How to alter the background colors on Activities.

[ ] Android Studio: Create a macro to do common things like: Font resize/zoom.

## Footer

Return to [Root README.md](../README.html)
