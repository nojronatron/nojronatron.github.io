# Reference of SQL Statements

Use this as a resource to guide writing and executing safe and valid SQL statements.  

## Queries

Select information from one or more or all columns, in one or more or all tables.  
Constraints can be put on queries to only display certain data, within certain ranges, etc.  
Queries can be 'joined' to display interrelated data.  

```sh
SELECT * FROM table_name; # returns all cols from table_name
SELECT col1,col2 FROM table_name; # return just the named column data
```

Completed Exercise 1:  

![Completed Exercise 1](./images/)  

### Constraints

Limit or specify the query results you want using Constraints.  
Constraints can be applied to other SQL commands in addition to Queries.  
Use constraints to limit results to improve performance.  
Return only what the client really, really needs, rather than everything.  

```sh
SELECT col1, col2 FROM table_name WHERE cond1 AND cond2 OR cond3;
# multiple constrains on 2 columns here
# single-col and/or single-constraint are also legal
```

Constaint Definitions

Number Operators: `=, !=, <, <=, >, >=`  
Between Operators: `BETWEEN first AND second` where first and second are values.  
Not Between: Same as between, prefixed with `NOT`  
Exists in a list: `IN(...)` e.g. `col_name IN(1, 3, 5)`  
Not Exists: Counter of IN e.g. `col_name NOT IN(2, 4, 6)`  

## Insert Update Delete

## Makin Tables

A schema must be defined when a new Table is added to a database.  
If a database already exists the system will throw an exception.  
To avoid 'already exists' exception use `if not exists` in the create table statement.  

```sh
CREATE TABE IF NOT EXISTS table_name (
  column DataType TableConstraint DEFAULT default_value,
  nother_col DataType TableConstraint DEFAULT default_value,
  ...
);
```

### Data Types

Many data types exist (MySql, Postgres, SQLite, MS SQL Server are just a few that have intersecting types):

Integer and Boolean - Recall that 0 is false and 1 is true.  
Float, Double, Real - These are all FP or decimal type primatives and are therefore 'precision values'.  
Character/Char, VARCHAR, TEXT - String values with limited memory allocations w/ overflow truncation.  
Date, DateTime - Depending on the system these might have somewhat different schemas.  
Blob - Data stored directly in the database. Not always the best option if performance (memory and query processing) are of any concern.  

### Table Constraints

Primary Key
AutoIncrement
Unique
Not Null
Check (expression)
Foreign Key

### Example Schema

```sh
CREATE TABLE my_table (
  id INTEGER PRIMARY KEY,
  title TEXT,
  owner TEXT,
  birthday INTEGER,
  active BOOLEAN,
  created DATETIME,
  Updated DATETIME
);
```

## Alter Tables

Add, remove, or modify columns and table constraints.  

### Add Columns

```sh
ALTER TABLE table_name
ADD col_name DataType OptionalTableConstraint
DEFAULT def_value;
```

### Remove Columns

```sh
ALTER TABLE table_name 
DROP col_to_delete;
```

### Rename Table

```sh
ALTER TABLE table_name 
RENAME TO new_table_name;
```

### Other Alter Capabilities

Consult the documentation for the DB platform to get details on other ALTER operations.  

## Drop Table

Use with caution:  

- An FK relationthip will break if a table partner is missing and could have detrimental results to your application.  
- Data in the table can only be restored from a backup *prior* to the table drop command execution.  
- Always use `IF EXIST` clause to avoid an exception being thrown if the table does not exist.  

```sh
DROP TABLE IF EXISTS table_name;
```

## Resources

A great deal of the information on this page was gleened from exercises provided by [SQLBolt lessons](https://www.sqlbolt.com)  

## Footer

Return to [Parent Readme.md](../README.html)  
