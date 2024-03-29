# Mongo and Mongoose

Database time!

## SQL and noSql

List five differences between SQL and noSql:

1. SQL: Relational databases; NoSQL: non-relational aka distributed databases.
1. SQL: Table-based databases; NoSQL: KVP or document databases.
1. SQL: Predefined _schema_; NoSQL: Dynamic schema for unstructured.
1. SQL: Scalable by increasing horsepower/resources; NoSQL: Scalable by adding database instances.
1. SQL: Uses 'Structured Query Language' aka SQL or T-SQL; NoSql: Uses 'Unstructured Query Language' aka UnQL.

### SQL-type DBs

MySql, Oracle, Sqlite, Postgres, MS-SQL.

### NoSql-type DBs

MongoDB, BigTable, Redis, RavenDb, Cassandra, Hbase, Neo4j, CouchDB.

### SqlNoSql QandA

What kind of data is a good fit for an SQL database?

> Structured, relational data.

Give a real world example.

> Storing related information for a Real Estate company is a good candidate.
> People with names live in homes with addresses, and they hire Real Estate Agents to sell their homes, and buyers must get mortgages from Banks - all of these things are related.

What kind of data is a good fit a NoSQL database?

> Unstructured, non-relational data.

Give a real world example.

> Storing random documents.
> Cloud storage is similar to NoSql is that it just stores stuff in a flat file system and keys are used to identify the data.

Which type of database is best for hierarchical data storage?

> SQL databases.

Which type of database is best for scalability?

> The answer to this is dependent on the scenario.
> In the cloud: Horizonally scalable NoSQL DB instances might be easiest, since an instance could be easily duplicated so many can be spun-up when needed without purchasing (and waiting for) handware.  
> In the DataCenter: Generally SQL type DBs are a good fit because server- and enterprise-class equipment have the ability to scale-up to very large resource numbers, which can be applied directly to a SQL type database server.

What does SQL stand for?

> Structured Query Langage.

What is a relational database?

> A database that holds data, grouped in tables, and every table has a key, and other table keys can create a reference to another table's column.

What type of structure does a relational database work with?

> Tables associated with each other through relational links between columns and/or keys.

What is a ‘schema’?

> A definition of data types to be stored and any relational information about the data.

What is a NoSQL database?

> An unstructured, non-relational document database type.  
> Mongo DB, Couch DB, and Redis.

How does it work?

> Key-Value pairs are used to store the document / data.

What is inside of a Mongo database?

> JSON formatted documents.

Which is more flexible - SQL or MongoDB? and why.

> MongoDB due to the dynamic schema.
> SQL databases require additional work and down-time to change the data schema.
> NoSql databases allow schema changes without impacting existing data already stored in the db.

What is the disadvantage of a NoSQL database?

> NoSql databases are limited to simple query types.  
> A database that might need to have complex queries called on it should use SQL, instead.

## Mongoose

Client-side app for programmatically using a MongoDB instance to store and retreive data, in an ExpressJS server application.

## MongoDB Features

MongoDB: NoSQL Database. Stores JSON formatted documents. Strong schema pattern not required, and schema is fully update-able. Full CRUD operations allowed.

MongoDB Atlas: Cloud-based Mongo database service. Free and paid tiers included.

Compass: Desktop app enables connecting, querying, and managing databases and data, locally or in Atlas.

### MongoDB Role-based Access Control

Roles:

- Grant privileges to perform specific actions on a resources.
- Do _not_ limit access.
- Multiple Roles can be applied to Users.
- Commands `rolesInfo` and `showPrivileges` and `showBuiltinRoles` provide details about a Role.

Access: Roles are applied with 'greatest access wins' paradigm. Inheritable.

Revoking Roles: Use `revokeRolesFromUser` command to remove a Role from a user.

Resources:

- Database.
- Collection.
- Set of Collections.
- A Cluster.

Authentication Restrictions:

- By IP Address.
- By resource.

Privileges:

- Consist of a Resource and the permitted action.
- Can be inherited.

Users and Roles:

- Assign Roles to users during creation.
- Update existing Users to grant/revoke Roles.
- Users are granted Privileges through Role assignment.
- Permissions applied to Roles can apply to one or more Databases.
- [Managing Users and Roles](https://www.mongodb.com/docs/manual/tutorial/manage-users-and-roles/)

Built-in Users and Roles:

- Provide commonly-needed privileges.
- [built-in Roles](https://www.mongodb.com/docs/manual/reference/built-in-roles/)

LDAP Authorization:

- MongoDB Enterprise supports LDAP integration.
- LDAP groups and users are supported.

Collection-Level Access Control:

- Allows Admins to grant privileges scoped to Collections.
- Collection-level access is provided via user-defined roles.
- Provision users with roles granted privileges on a Collection level.
- Scope: The combination of an Action and a Resource that an Action can be taken on.

## Resources

- [Mongoose API](https://mongoosejs.com/docs/api.html#Model)
- [React Router](https://reactrouter.com/web/api/BrowserRouter)
- [MongoDB Atlas Documentation](https://www.mongodb.com/docs/manual/)

## Footer

Back to [readme.md](../README.html)
