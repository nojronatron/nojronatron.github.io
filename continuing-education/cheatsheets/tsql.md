# TSQL Language Cheatsheet

Scripting language for talking with SQL data.

## Table of Contents

- [Essentials](#essentials)
- [Why T-SQL?](#why-t-sql)
- [SSMS](#ssms)
- [Join](#join)
- [Terminology](#terminology)
- [SQL and Docker](#sql-and-docker)
- [References](#references)

## Essentials

1. Query for the least amount of necessary data. Tell T-SQL what you want.
2. Only change data that needs to be changed.
3. Avoid processing data within TSQL (use programming languages for this).
4. Consider how Join result data will be represented when designing the query.

Use single quotes `'` to surround strings.

Keywords no longer need to be all caps, it is case-insensitive.

Comments: Prefix with `--`

Primary Key must be unique and should not change:

- Avoid keys like `FIrstName + LastName` because these can change over time.
- Select an ID along with the data you want.
- GUIDs are not as performant as Integer IDs.
- Can be incrementing or decrementing or random.
- Gaps are ok.

Top-of-mind data write transaction note:

1. Logfile gets changed first.
2. Data changes _next_ based on logfile changes.

Aliases:

- Rename a field name to simplify script writing.
- Must be at least 1 character long.
- Programming best practices don't really apply, so use `p` for `dbo.People` if you want.
- Alias by adding the new name to the end of a statement: `from dbo.People p`

Delimit Reserved Words (best practice):

- Add square brackets `[`, `]`
- State is reserved: `select p.[State] from dbo.People p`

Update:

- Write the `set` statement _last_ to over-updating table(s) in the database.

Delete:

- Write as a `select` statement first to refine to ensure correct records are returned.
- Change to a `delete` statement once debugged.

T-SQL can also:

- Create/drop Tables.
- Create Stored Procedures.

Limit Your Application:

- Never supply Apps with direct access to SQL DB.
- Wrap TSQL Queries and Scalers in SQL Stored Procedures, instead of adding TSQL directly in code.

Effecient Query Execution:

- Querying against ID fields is the most effecient.

## Why T-SQL?

Executing T-SQL scripts at the DB server has several benefits:

- Simplify code by encapsulating query complexity in Stored Procedures.
- Efficiently execute queries and scaler operations close to the data.
- Finely control parameters and return data.
- Perform complex queries exactly the same way every single time.
- Gain insight into query/scaler effeciency with execution plans
- Portable language. There is a lot of overlap between relational query languages.

In most cases, an ORM will be necessary to enable interfacing your database:

- ORMs are fine-tuned to varying goals.
- Some abstract away database interaction details almost completely.
- Some allow fine-grain control over SQL queries, including the ability to write raw queries in code.
- Others also allow interaction with Stored Procedures, ensuring a safe, testable DB interaction interface.
- An ORM can make code more complex through the sematics and interaction requirements of the ORM itself, such as boilerplate setup code.

### Stored Procedures and Lightweight ORMs

Lightweight: Low-overhead for performance, and limited coding requirements.

Ready To Code: Translate SQL Query results into language-native objects, and vice-versa.

SQL Integration: Call Stored Procedures with arguments, pushing complexity away from code while enabling fine-grained control over Query and Scaler performance.

Less-opinionated: Allows developer to implement change tracking and schema migration that matches their business requirements.

## SSMS

Refresh SSMS Table Cache:

- Key combo: Ctrl + Shft + R
- Do this after creating a new Table.
- When writing a new Query and `dbo.NewTable` has red underline:
  - Ensure correct Database is selected (Using, or DB drop-down).
  - With the `using` statement.

Execution Plan:

- Estimated: Programmative guestimate of relative cost.
- Actual: The actual Query execution analysis.

## Join

Joining data means to match-up data from multiple tables based on varying criteria:

1. Start with a standard query (select ... from dbo....).
2. Add join type statement (left join db.... ON field = field).
3. Nulls are returned when matching field's record doesn't have data in the linked table record's field. This might be what you want.

Inner Join:

- Where do these records match-up?
- Include only records where data in joined _fields_ is the same.
- inner join `table [alias]` on `field` = `otherField`
- `inner join dbo.Addresses a on p.Id = a.PersonId`
- Finds "overlapping" records based on queried record fields.

Left Join:

- left join `leftTable [alias]` on `field` = `otherField`
- Return _all_ records of the left table, and include only _matching_ records from the right table.

Foreign Key:

- A table Key that points to the Primary Key on another table.
- Consider it a lookup link.

Sub-query clause:

- Use `from` keyword followed by parentheses.
- Write the sub-query just like a usual query but within parentheses.
- Optionally provide an alias after closing parenthesis.
- Write the outer query.
- Useful for debugging complex queries using text highlight and `Execute` button in SSMS.
- Usually sub-queries can be replaced with a `where` statement (which might even change performance).

## Terminology

Query: Ask for data.

Select: What you want.

From: Where the data should come from. Optional parenthesis used for sub-querying.

Where: Filter clause.

Order by: Param `field` `[asc|desc]`. Ascending is default.

On: Used with `inner join`, `left join`, and `right join` operations, and `constraint` clause.

Insert: Insert data into specified table using named columns, and collection of values. Values can be comma-separated grouped lists for multiple record insertions.

Update: Adjust data on specified table, with supplied value, using where statement(s) to identify _which records are updated with the value(s)_.

Delete: From a table. Use Where clause to scope to specific record(s) to delete.

## SQL and Docker

Goals:

- Setup and run SQL Server in 5 minutes.
- Connect and Configure DBs and Tables.
- Simplify querying a dockerized SQL Server.

Major Steps:

1. Launch Docker Desktop.
2. Generate restore-backup.sql file that executes RESTORE DATABASE, WITH FILE=1.
3. Declare a docker-compose.yml file that sets sql services (build, container name, ports) and passes environment variables (as necessary) to Dockerfile.
4. Declare a Dockerfile with ARGS to capture environment variables, target the correct DockerHub image, provide other installation required variables, executes commands to prep the Docker Container environment, copies in required files, change file permissions (i.e. for SH or executable files), expose necessary part(s), and provide the CMD["{command_path}", "{entrypoint-script.sh}"].
5. Use `docker-compose` commands to up, down, and logs the Container.

See an example in my [deploy-mssql-docker](https://github.com/nojronatron/deploy-mssql-docker) repo.

### Setup and Run an Image

Cmdline: `docker run -e "{env_var}" -e "{env_var}" -p 11433:433 -d mcr.microsoft.com/mssql/server:2022-latest`

- Runs a docker image.
- Environment variables and their values e.g. "ACCEPT_EULA=Y" and "MSSQL_SA_PASSWORD=myP4ssw0rd!".
- Port `localPort:containerPort`
- Run the following image name in disconnected mode: `-d {docker_tag_name}`

Optional Exploratory Database:

- AdventureWorksLT: Lightweight version.

Edition: Without indicating the PID, Developer Edition is selected.

Output: A GUID representing the newly downloaded, configured, and running Container.

### Connect and Configure

1. Launch SSMS.
2. Server Name: `localhost,{internal_port}`
3. Login: SQL Server Authentication + creds.
4. Click Connect.

### Dockerfile

Specify the steps to build a new image:

- FROM: Build image
- AS: Name the image
- ENV: Environment variable K=V format, newline separated
- WORKDIR: Define a temporary working directory e.g. `/tmp`
- COPY: Copies first to next.
  - Next can be `.` to mean "WORKDIR" aka "here"
  - Backup DB file
  - TSQL Scripts
- RUN: Set of commands to launch SQL instance and execute commands
  - For SQL Server this would likely be a set of backup DB files

Execute the Dockerfile: `docker build -t {name} .`

#### Configure for a Release

1. Follow the basic steps above.
2. Add new steps to select the image again with a new `AS` name (e.g. 'Release').
3. Use COPY command to move completed files so setup files won't be available.

### Other Docker Operations

Stop: `docker stop {guid}`

Remove: `docker remove {guid}`

View all Containers: `docker ps -a`

## References

- Tim Corey [SQL Development Made Easy with Docker](https://www.youtube.com/watch?v=Yj69cWEG_Yo)
- MSFT SQL 2022 [Quickstart install connect docker SQL Server](https://learn.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker?view=sql-server-linux-ver16&preserve-view=true&tabs=cli&pivots=cs1-bash#pullandrun2022)
