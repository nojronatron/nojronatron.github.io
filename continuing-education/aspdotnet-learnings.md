# ASP.NET Learnings

Collection of takeaways and key infos while learning more about ASP.NET, ASP.NET Core, and .NET 6.

## Minimal APIs

Get started developing an API with just a few lines of code, as opposed to the many files and code blocks necessary using previous templates and frameworks of DotNET.

- Targets .NET 6 and newer with all the new features they bring along.
- Simpler to startup a new project.
- Add features when needed to a small, compact, easy to read codebase.
- Web API utilize Controllers to handle HTTP verbs, process inputs, and return results. Minimal APIs does not.
- Streamlined Program.cs: No wiring of Controller routes (`AddControllers()`).
- Swagger is still available.
- Routing is a series of method calls representing HTTP verbs: `MapGet()`, `MapPost()`, `MapPut()`, and `MapDelete()`.
- Database, CORS, and Authentication setup are no different in Minimal APIs.
- `app.Run()` starts the API so it is 'listening' for requests.

### Minimal APIs Project Template

Run `dotnet new web -o $projectName -f net6.0` to get started.

Use `dotnet run` just like any other project to launch it.

The default TCP port is a value between 5000 and 5300. SSL ports should be in the 7000 to 7300 range.

### Add Swagger

Swagger is a documentation tool.

Whenever changes happen to an API, documentation should change too!

Self-documenting can be helpful, reducing costs of maintaining code during the development process.

How to install Swagger: `dotnet add package Swashbuckle.AspNetCore --version 6.1.4`.

Configure Swagger:

1. Add a using statement for the namespace: `Microsoft.OpenApi.Models;`.
2. Set SwaggerGen method (see example below).
3. Add `UseSwagger()` and `UseSwaggerUI()` (see example below):

```c#
// Set SwaggerGen method
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen(
  sg => {
    sg.SwaggerDoc(
      "v1", new OpenApiInfo {
        Title="title",
        Description="description",
        Version="v1"
    });
});
```

```c#
// Add UseSwagger and UseSwaggerUI
app.UseSwagger();
app.UseSwaggerUI(
  usui => {
    usui.SwaggerEndpoint("/swagger/v1/swagger.json", "version");
});
```

### Why Minimal APIs

- Reduced overall code through simplifying route definition in service definition, and in route implementation through lambdas.
- Fast, low-code way to develop a prototype or proof-of-concept.
- Self-documenting when OpenAPI Swagger is used.
- Routes are defined using HTTP Verbs and are simplified.
- Full support for Middleware such as CORS, etc.

### Routing with GET Requests

Major use cases:

1. Just implement the response as a lambda in the route using `app.MapGet()` function.
2. Access a specific record using a unique identifier as a wildcard match. See example below.

```c#
// client sends an HTTP GET verb with the URI "/products/1"
// id param will capture the route parameter '1' in the Minimal API route
app.MapGet("/products/{id}", (int id) => data.SingleOrDefault(product => product.Id == id));
```

### Routing with POST Requests

POST will create a resoruces.

- Used to capture and process data in the request Body.
- Request body 'body' is sent to the lambda for processing.
- Content of 'body' can be serialize and processed.

```c#
// assume a Product Class like
public record Product(int Id, string Name, string Description);
// JSON BODY with POST request:
// {
//   "Name": "New product",
//   "Description": "product description"
// }
app.MapPost("/products", (Product product) => { /* process BODY here */ });
```

### Routing with PUT Requests

PUT means "update an existing record".

- `MapPut()`.
- Similar to `MapPost()`.
- Expects a posted BODY with the request.
- Client wants the existing item to be _updated_ with changes in the request body.

```c#
app.MapPut("/products", (Product product) => { /* update the data store using this product instance */ });
```

### Routing with DELETE Requests

Use `MapDelete()`.

- Unique ID expected in the request.
- Lambda should check the data store for that ID and then delete it.
- Alternatively can search for ID in data store and just change a property such as `IsDeleted` from `false` to `true`.

### Returning a Response

Minimal API framework recognizes Types and serializes them as JSON.

## Entity Framework Core

ASP.NET Core and .NET 6 support local DB storage ORMs like Entity Framework Core.

- Persist data in an ORM using CRUD operations.
- Lightweight, extensible solution.
- Open source and cross-platform.
- Work with a DB using .NET objects.
- Simplifies data-access coding tasks that other frameworks (or accessing SQL directly) would impart.
- Supports SQLite, MySQL, PostgreSQL, Oracle, and MS SQL.
- Decouples application from database providers (there is still work to do to switch, but coupling is loose).

### MoEntities and Context

EF uses entity classes and a context object to represent a session with a database.

The Entity Class:

- Like a plain-old c# object.
- An ID field allows the API to identify instances.
- Each represents a business object in the app and maps to a single DB table.

The Context Class:

- Does the actual querying and data moving between code and DB.
- Saves data to the DB.
- Create and manage DB connections.
- Retreive data.
- Buffers the data.

### EF Core CRUD Operations

Delegate DB operations to the Context class.

Queries are _always_ executed against the DB.

Queries are:

- Asynchronous.
- Are implemented through the context in the name of the custom Entity (class).
- Find: Use `FindAsync(param)` to get data by Id or other Entity field(s).
- Remove: Include the ID of the item to remove, or send the entire instance to the `Remove(param)` method.
- Update: Retreive the existing item first (usually by ID) then use `Item` ([see in-memory db](#add-ef-core-in-memory-db)) and `IsComplete` fields to make changes to the instance, then use `db.SaveChangesAsync()` to commit the changed entity back to the DB.

### EF Core In-Memory DB

- Useful for testing an application.
- Avoid using in a production environment.
- Simple, easy to implement and use.

#### Add EF Core In-Memory DB

Terminal: `dotnet add package Microsoft.EntityFrameworkCore.InMemory --version 6.0`

Once installed:

- Add using statement to `Program.cs` and any entity models e.g. `Pizza.cs`: `using Microsoft.EntityFrameworkCore`.
- Set up in-memory by adding a builder sevice: `builder.Services.AddDbContext<YourEntity>(options => options.UseInMemoryDatabase("items"));`.
- Set up EFCore Context like the example below.

```c#
class YourEntityDB : DbContext
{
  public YourEntityDb(DbContentOptions options) : base(options) { }
  public DbSet<YourEntity> YourEntity { get; set; } = null!;
}
```

### EF Core Database Provider

Connect to a relational database that will persist data between application stop-starts:

- Reuse code vs. in-memory store!
- Supports more than 20 DB providers including SQLite, MS SQL, and more.

#### Add EF Core DB Provider

1. Add NuGet packages.
2. Configure DB Connection.
3. Configure DB provider in teh ASP.NET services.
4. Perform DB migrations.

#### Install EF Core SQLite

1. Add EFCore SQLite provider: `dotnet add package Microsoft.EntityFrameworkCore.Sqlite --version 6.0`.
2. Add EFCore Tools: `dotnet tool install --global donet-ef`.
3. Add EFCore Design-time logic: `dotnet add package Microsoft.EntityFrameworkCore.Design --version 6.0`.

#### Enable EFCore SQLite DB Creation

First, add a builder to Program.cs:

```c#
// check config for connection string 'pizzas' and if missing use the datasource instead
var connectionString = builder.Configuration.GetConnectionString("Pizzas") ?? "Data Source=Pizzas.db";
```

Next define SQLite as the database type:

```c#
// YourEntityDb is the Class that inherits from 'DbContext' in a separeate Class file
builder.Services.AddSqlite<YourEntityDb>(connectionString);
```

Update migration using the EFC Migration Tool: `dotnet ef migrations add InitialCreate`.

Create DB and Schema: `dotnet ef database update`.

Verify:

- No errors in the Terminal.
- A new file named `YourEntities.db` appears in the filesystem.

#### Add Routes that Utilize SQLite DB

GET: `app.MapGet("/things", async (ThingDb db) => await db.Things.ToListAsync());`

POST:

```C#
app.MapPost("/thing", async (ThingDb db, Thing thing) =>
{
  await db.Things.AddAsync(thing);
  await db.SaveChangesAsync();
  return Results.Created($"/thing/{thing.Id}", thing);
});
```

GET (by ID):

```C#
app.MapGet("/thing/{id}", async (ThingDb db, int id) =>
{
  var thing = await db.Things.FindAsync(id);
  if (thing is null)
  {
    return Results.NotFound();
  }
  else
  {
    return Results.Json(thing);
  }
});
```

PUT (Update):

```C#
app.MapPut("/thing", async (ThingDb db, Thing updateThing, int id) =>
{
  var thing = await db.Things.FindAsync(id);
  if (thing is null)
  {
    return Results.NotFound();
  }
  thing.Name = updateThing.Name;
  thing.Description = updateThing.Description;
  await db.SaveChangesAsync();
  return Results.NoContent();
});
```

DELETE:

```C#
app.MapDelete("/thing/{id}", async (ThingDb db, int id) =>
{
  var thing = await db.Things.FindAsync(id);
  if (thing is null)
  {
    return Results.NotFound();
  }
  db.Things.Remove(thing);
  await db.SaveChangesAsync();
  return Results.Ok();
});
```

## Resources

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../READMD.html)
