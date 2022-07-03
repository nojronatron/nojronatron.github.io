# Saving, Defining, Relationships, and Accessing Data in Room

## References

[Saving Data in Room](https://developer.android.com/training/data-storage/room)

[Define Data Entities in Room](https://developer.android.com/training/data-storage/room/defining-data)

[Define Data Relationships in Room](https://developer.android.com/training/data-storage/room/relationships)

[Accessing Data Using Room DAOs](https://developer.android.com/training/data-storage/room/accessing-data)

## Save Data In Local DB Using Room

Use Room to locally store non-trivial data for e.g. caching when device is offline.

Room overlays a SQLlite Instance and interfaces.

SQL Queries are verified at compile-time.

Annotations minimize boilerplate code.

DBs can be [easily migrated](https://medium.com/androiddevelopers/incrementally-migrate-from-sqlite-to-room-66c2f655b377).

## Implement Room

Update build.grade to support RXJava, Guava, Test Helpers, and Paging3:

```sh
dependencies {
    def room_version = "2.4.2"

    implementation "androidx.room:room-runtime:$room_version"
    annotationProcessor "androidx.room:room-compiler:$room_version"

    // optional - RxJava2 support for Room
    implementation "androidx.room:room-rxjava2:$room_version"

    // optional - RxJava3 support for Room
    implementation "androidx.room:room-rxjava3:$room_version"

    // optional - Guava support for Room, including Optional and ListenableFuture
    implementation "androidx.room:room-guava:$room_version"

    // optional - Test helpers
    testImplementation "androidx.room:room-testing:$room_version"

    // optional - Paging 3 Integration
    implementation "androidx.room:room-paging:2.5.0-alpha02"
}
```

Above code sample smipped from *[Saving Data in Room]*.

## Primary Room Components

Room Database. Can talk to rest of app and will call getDAO.

Data Access Objects (DAO): Get Entities from db and persist changes to DB.

Entities: Models stored in the DB as Tablular data records. Must support GET/SETters.

Android App: Common communication point between Room DB, DAO, and Entities.

## Entities

Annotations: `@Entity`, `@PrimaryKey`, `@ColumnInfo` etc.

Entity parameters: e.g. `(tableName = "users")`

Key parameters:

- No-params Key is an int type usually named 'id'.
- `(primaryKeys = {"firstName", "lastName"})` uses combo of columns for a 'composite primary key'.
- Ignore a field in an entity: `@Ignore`. Use to *not* store the field data in the DB e.g. images etc.
- Ignore inherited fields from a parent Entity: `@Entity(ignoredColumns="col_name")`

### Other Annotations

Full-text search `@Fts3` (small disk volumes) and `@Fts4`. Args `(launguageId='lang_id')`.

Specific Columns can be indexed if SDK Versions don't support FTS3 or FTS4, using an 'indices' property or the `@Entity()` annotation, then define the `@Index` annotations to specify the columns.

`@AutoValue`: Support Java Immutable Value Classes between DBs where a column contains identical data.

## Relationships in Room

Room *does not allow entities to directly reference each other* for technical reasons.

Use an Intermediate Data Class:

- Model the relationship between the related Room Entities.
- Pairings are held as embedded objects.
- Query methods return isntances of the data class for use by the App.
- Leverage SQL statements in the `@Query()` annotation e.g. `("select user.name AS userName, book.name AS bookname from user, book where user.id = book.user_id)`.

*[Example lifted from Define Data Relationships In Room]*

Use the MultiMap approach:

- Define a 'multimap' return type for a method that maps the relationship between entities.
- Put "directly in your SQL query".
- Return type of method is `Map<T, List<U>>`.

*[Example lifted from Define Data Relationships In Room]*

## DAO

Annotations: `@Dao`, `@Query("select * from tbl_name")` etc, `@Insert`, and `@Delete`.

Define Data Access Objects as an Interface *or* an Abstract Class, using `@Dao` annotations.

### DAO Annotations

Annotations are used to define the operation the abstract DAO Method represents:

- `@Insert`: Define a non-implemented method with return type void called 'insertAll' or similar that takes a Collection as method parameter.
- `@Delete`: Define a non-implemented method with return type void called 'delete' or similar that take a single Instance as a method parameter.
- `@Query(SQL_statement)`: Define a non-implemented method with a Collection return type called "getAll" or similar.

### DAO Abstract Methods

Scaler abstract methods do NOT allow writing custom SQL statements.

Query abstract methods allow parameters defining custom SQL code.

Scalar abstract methods utilize a param 'onConflict' to resolve how to deal with a conflict on Write/Update.

Update Method: Attempts to update records in the database using an Entity instance.

Delete Method: Attempts to delete specific records in the DB using an Entity instance.

Query Method: Supports Simple SQL, JOIN methods, specific 'where' requirement queries, and MAP statements.

Paginated queries are allowed.

There are more details that should be examined before attempting to implement [here](https://developer.android.com/training/data-storage/room/accessing-data)

## Database

A Database Class must be defined to represent the Room DB using annotation `@Database`.

Database Class must inclue an `entities` array listing data entities associated with the DB.

Database Class must be abstract and must extend RoomDatabase.

Database Class must define abstract methods w/ zero args returning instance of DAO class for each DAO Class that is associated with the DB.

## Using the Database

Set up an instance of the database like so:

```java
AppDatabase db = Room.databaseBuilder(getApplicationContext(),
  AppDatabse.class, 'db_name').build();
```

Above code sample smipped from *[Saving Data in Room]*.

AppDatabase abstract methods can be used to get an instance of the DAO, e.g.:

```java
UserDao userDao = db.userDao();
List<User> users = userDao.getAll();
```

Above code sample smipped from *[Saving Data in Room]*.

### Resources

[Sample app "Sunflower" using Room](https://github.com/android/sunflower)

[TV Tracking App using Room](https://github.com/chrisbanes/tivi)

[CodeLab](https://developer.android.com/codelabs/android-room-with-a-view)

[7 Pro-tips for Room](https://medium.com/androiddevelopers/7-pro-tips-for-room-fbadea4bfbd1)

## Footer

Return to [Root Readme](../README.html)
