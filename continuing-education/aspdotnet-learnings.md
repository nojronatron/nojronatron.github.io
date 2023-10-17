# ASP.NET Learnings

Collection of takeaways and key infos while learning more about ASP.NET, ASP.NET Core, and .NET 6.

## Table of Contents

- [Minimal APIs](#minimal-apis)
- [Entity Framework Core](#entity-framework-core)
- [Full Stack ASP Dot Net Development](#full-stack-asp-dot-net-development)
- [GitHub CodeSpaces](#github-codespaces)
- [Resources](#resources)
- [Footer](#footer)

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

## Full Stack ASP Dot Net Development

Create a full stack webapp using:

- ASP.NET Core
- Minimal APIs
- React
- CORS

### Front-end Development Concerns

- How user interacts with features.
- Designing an effective layout.
- Designing a user flow for positive interaction.

Users manage data on the app front-end:

- Create
- Read
- Update
- Delete

### Front-end Development Design Systems

Ideas that guide:

- Design Principles: Site design.
- Brand Values: Overall design to trigger specific emotions in users.

Rules and guidelines:

- Brand Style Guide: Using the brand's visual identity correctly.
- Content Guidelines: Writing content that is in line with the organization's mission and values.
- Accessibility Guidelines: Make the site accessible to all users.

Collections of Components:

- Component Library: Reusable code for building applications.
- Pattern Library: Navigation bars, Footers, Forms, and other componentized code, for reusable, consistend App look-and-feel.
- Icon Library: Icons used within the site.

Design Tokens: Names representing hard-coded values for visual elments e.g. Spacing, Color, Typography.

#### Common Design Systems

- [Material Design](https://material.io/)
- [Fluent UI](https://developer.microsoft.com/fluentui/)
- [Bootstrap](https://getbootstrap.com/)
- [Chakra UI](https://chakra-ui.com/)

### Selecting a Design System

- Learn what features the system has, and if it has the features _you need_.
- Can the design system be customized, or are the components canned and as-is?
- Does the design system provide accessibility?
- How large in the community? Is the community active?
- How is support (does it exist)? If it does, is it free? Is their a paid option, or paid only?
- Is there an initial cost in money to use the system or is it free? One-time cost or is it a subscription?
- What framework(s) are supported? Does it support the framework you are using?
- Does the system allow using only the features you need? Can it be optimized? Is there a way to minimize unused code?
- Does it support the target browsers your app needs to run on?
- How large is the system when implemented i.e. does it slow browser load-time? Can it be tweaked to meet specific performance metrics?
- What are the dependencies of the system? Are they still available and supported? Does it include dependencies you _do not want to use_?

### Additional Design System Considerations

CSS Styles:

- CSS vs JSX syntax
- Preprocessors (SASS, LESS, Stylus) and Postprocessors (Autoprefixer, PostCSS, CSSNano)

CSS in Javascript:

- Manageability and maintainability. Good for teams in close design and FE build collaboration.
- Consistency: Easier to maintain a consistent look and feel.
- Dynamic Styling: More concise and adaptable code.
- Onboarding a migration might be difficult.
- Delivery and Performance: Slower packaging and site rendering due to larger size of packaged files and site generation.

Component Composability:

- Organization: Layout components that define DOM hierarchy and where controls are in the page.
- Presentation: Interactive and display components like Buttons, Sliders, Text boxes, etc.

Typography:

- Serif Fonts: Lines/decorations/tails could lead to more difficult rendering or contrast/vision issues.
- Sans-serif: Plain fonts are higher contrast but not as 'interesting'.
- Display Fonts: Fancier fonts usually used for Titles, Headings, or other eye-catching purposes.
- Optimized typography enables smaller download size and better rendering performance on your App.
- Rendering _order_ and performance can affect how Fonts appear to the user. Flash of Invisible Text (FOIT) and Flash of Unstyled Text (FOUT) are 2 possible problems that can occur when typography and design are not carefully planned.

Icons:

- Usually used for Navigation and Button faces.
- Select similar/same family icon designs to maintain consistency through the App/Site.

### Single Page App Frameworks

An SPA:

- Uses a single main view page.
- Navigation is moving other pages in/out of the main view page.
- URL stays the same.
- Only content is changed.
- Lots of JavaScript is used to manipulate the DOM to make this happen.

React:

- Uses EF6 and TypeScript/JavaScript.
- Engaged tooling community.
- 3rd party components are available.

Angular:

- Heavy use of TypeScript.
- Good tooling.

Vue.js:

- Popular (that's all MSFT Learn had to say about it).

Svelte:

- Powerful compiler.
- Hides framework parts.
- Looks a lot like just HTML, CSS, and JavaScript.

Next.js:

- Hybrid static + server-side rendering (SSR).

### Bundlers

Takes JS, CSS, images, etc and creates one or more 'bundled files'.

- Reduces files and file sizes for download to the client.
- Webpack: Used by many framewoks with lots of features and is configurable.
- Parcel: Easy to use, lots of features, but no configuration.
- Vite: Focused on speed and simplicity. Configured templates are used to target various frameworks.

### Front-end Development Server

Used to service HTTP requests while developing the App. SPAs are hosted applications - a server on an HTTP port and possibly behind a proxy will serve up content based on browser requests.

Configurable settings:

- Port: The TCP port the server listens on.
- Proxy: Whether one is used as a bridge between the browser and the back-end API.

### Data Binding

One-way:

- Passing parameters from Parent component to Child component.
- Child component cannot change the data.
- Child can send a message to Parent to change the data.
- Parent component is only one that can change data.
- In React this allows Parent component to control when Child component(s) are rendered (and re-rendered).
- Pass a Callback Function from Parent to Child so Child component can use it to get updated data.

React UseState:

- Allow Parent to store and update data (parameters).
- Parent can send UseState variables _as params_ to the Child component as callbacks!
- Child can then set the callback param as an `onClick` to tell the Parent to update the data.
- When Button is clicked on child component, the data sent with the 'set' callback will update the Parent and the Child will be re-rendered.

### State Management

This needs to be planned to ensure effecient component rendering:

- React has its own State Management system: `useState` hook.
- Redux is an alternative.
- `useState` 'hooks' into the Component lifecycle to add functionality.
- Carefully plan how params from useState will be sent to Child components.
- Carefully plan how Child components can use a callback to tell Parent to update State.

### Scaffold an App

Using Vite:

1. Use the Terminal.
2. `npm create vite@latest ProjectName --template react`
3. Set package name, framework, and variant (JS or TS).
4. Install dependencies using `npm install`.
5. Update `vite.config.js` to set a static server port. 3000 is suggested.
6. Run the package using `npm run dev` and open the URI in a browser to see the rendered site.

## GitHub CodeSpaces

The Full-stack learning module used a GitHub CodeSpace as a development container. This section will contain notes about CodeSpaces and my experience using them.

### Challenges

- I hadn't used CodeSpaces before (but the value seems high).
- When launching the template CodeSpace, there are six projects within the solution so learning the layout of the files and projects slowed progress.
- A Dev Certificate had expired in the Template and there was no information within the MSFT Learn Module about working with Dev certificates (this is partially on me, I should learn how to manage Dev Certificates if I want to regularly work in DotNET development).

### Cost

CodeSpaces are not free, at least after 60 hours per month:

- [ ] How to monitor usage?
- [ ] Cost after surpassing 60 hours?
- [ ] What features are included in CodeSpaces?

### Cleaning Up Codespace

Go to the [CodeSpaces Dashboard](https://github.com/codespaces) and find the CodeSpace to clean up and click the Delete button.

At the very least, 'Stop' the CodeSpace until you need it next.

## Resources

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../READMD.html)
