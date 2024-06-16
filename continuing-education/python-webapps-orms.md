# MSFT Reactor Webinar: Python WebApps and ORMs

Host: Pamela Fox, Cloud Advocate in Python, MSFT

- 20+ years experience with Python.
- Pamela used to work for Kahn Academy.

## Connecting Python WebApps to DBs using ORM

Tools Used Today:

- VSCode
- Python3
- PostgreSQL
- Flask
- DevContainers
- Docker

## About DBs

Persist data across multiple users or computers.

- A browser can store data for a single user on a single system.
- Database can store data across many devices.
- Databases store data for many users.

DB's are also useful and performant for generating statistical reporting.

No-SQL (Document Databases):

- MongoDB, Redis, Cosmons DB for NoSQL.
- Typically a JSON document.
- Sometimes a Key-Value-pair document (which is of course similar to JSON).

Relational:

- PostgreSQL, MySQL, SQLite, MS SQL Server.
- Contain tables with columns and rows.
- Tables relate the data by referencing columns between tables.

SQL Structured Query Language:

- Select, Insert, Update, Delete.
- Various JOINs.
- SQLite has all of the above SQL commands, but with performance implications.

## PostgreSQL

Features:

- Open-source.
- Relational DB.
- Supports JSON, XML, and more.
- Many extensions like PostGIS for geospatial.
- Python libraries for PG: psycopg (driver), SQLAlchemy (ORM)
- Default db name is 'postgres'.

Playgrounds to try it out:

- PostgreSQL playground
- pgvector playground

Use .env File:

- DBHOST, DBUSER, DBPASS, DBNAME... the usual connection suspects can be set here.

YAML Files:

- Used to setup the Docker Image
- Will contain information set in your `.env` files
- Also contains SQL driver packages, etc

VSCode SQL Tools:

- Use to connect to local or cloud-hosted Databases within VSCode
- Explore Tables, Schema, Views, Functions, ... the usual suspects!
- Use SQL commands to create tables, insert data, and then select from tables to validate creation succeeded

## Demo Accessing DBs from Pythong

Call SQL via a DB Driver!

- Connect directly with a SQL DB.
- Use packages such as psycopg or asyncpg (for synchronous and async commands, respectively).
- Execute SQL statements directly.
- Called "Raw SQL".
- Is vulnerable to SQL-injection attacks.
- Remember "Users will input anything and everything" whether malicious or not.
- Inputs need to be sanitized, set for locale and internationalization, etc.

Utilize an ORM to interact safely:

- Object Relational Mapper.
- Represents table rows as objects.
- Provides methods for querying and modifying data.
- No more writing raw SQL.
- Removes most vulnerabilities compared to raw SQL statements.
- SQLAlchemy.
- Essentially overlays a query languange on top of actual SQL commands.

Tip: Use any ORM options that allow viewing the actual SQL Statements that are called so it simplifies dev, test, and debugging.

Mapped As Data Class:

- Built-in to Sql Alchemy 2.0
- Treats all Table classes as "data classes".
- Validation is available for Data Classes.
- This is similar to adding `ToString()` to a C# class, where class member names and values are easily stringified.

## Flask and Databases

Flask:

- Like Django.
- Very lightweight framework.
- Does NOT come with any DB functionality so either use Flask SqlAlchemy or Flask-Migrate extensions.
- Models are defined in Python.
- DB Migrations are run.
- SqlAlchemy can then be used in all "class routes".

Tip: Playwright can be used to test Flask and Django-based webapps!

Flask Migrations:

- Tracks changes to schema.
- Migration files record the changes between DB schema states.
- Code-generates changes to DB schema.
- Run the code to apply the changes using the generated code.

## Vector Search

What type of querying are you using? Vector Search, or Retreival Augmented?

Vector Search:

- Compare objects to other objecst.
- Creates a graph.
- Used to determine similarity.

RAG - Retreival-Augmented Generation:

- When Vector Search is not enough
- PGVector can be used to support Vector Search _and_ RAG

## Hosting DB Backed WebApps on Azure

Considerations:

- How big will database be?
- How about reads vs write operations?
- Latency concerns?
- What is required backup/restore/recovery policy?
- Data sovereignty regulations.
- Multiple replicas necessary for HA?

Azure databases:

- PostgresQL on Azure
- Flexible PG SQL server for inexpensive dev/test usage

Bicep:

- Infrastructure as code.
- Use to declare resources necessary for an environment.
- Deploy environments with consistent settings.

## Resources

- Tutorials and exercises using Flask on [Pamela Fox's GitHub](https://github.com/pamelafox)
- MS Reactor previous webinar: [Pyton WebApps 101](https://aka.ms/python-web-apps-101)
- Check out Khan Academy's SQL Lessons.

There will be a Docker-related MSFT Reactor session on Tuesday June 18th "Python Web Apps: Containerization with Docker".

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
