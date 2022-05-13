# Reference of SQL Statements

Use this as a resource to guide writing and executing safe and valid SQL statements.  

## Queries

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

Many data types exist (MySql, Postgres, SQLite, MS SQL Server are just a few that have intersecting types):

Integer and Boolean - Recall that 0 is false and 1 is true.  
Float, Double, Real - These are all FP or decimal type primatives and are therefore 'precision values'.  
Character/Char, VARCHAR, TEXT - String values with limited memory allocations w/ overflow truncation.  
Date, DateTime - Depending on the system these might have somewhat different schemas.  
Blob - Data stored directly in the database. Not always the best option if performance (memory and query processing) are of any concern.  

## Resources

A great deal of the information on this page was gleened from exercises provided by [SQLBolt lessons](https://www.sqlbolt.com)  

## Footer

Return to [Parent Readme.md](../README.html)  
