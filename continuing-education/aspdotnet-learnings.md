# ASP.NET Learnings

Collection of takeaways and key infos while learning more about ASP.NET, ASP.NET Core, and .NET 6.

## Table of Contents

- [Blazor](#blazor)
- [Blazor Forms and Validation](#blazor-forms-and-validation)
- [Minimal APIs](#minimal-apis)
- [Entity Framework Core](#entity-framework-core)
- [Full Stack ASP Dot Net Development](#full-stack-asp-dot-net-development)
- [GitHub CodeSpaces](#github-codespaces)
- [Resources](#resources)
- [Footer](#footer)

## Blazor

There are 3 "flavors" (my words) of Blazor:

- Blazor Web
- Blazor Server
- Blazor Hybrid

Deploy a new Blazor Server using dotnet: `dotnet new blazorserver -o MyBlazorServerProject -f net6.0`. This creates a new Blazor Server Project named "MyBlazorServerProject" using the DotNET 6 SDK.

### Blazor Web

Provides a WebAssembly capabilities where components are executed in the client browser, rather than on the server. Provides cross-platform compatibility and enhanced performance by eliminating round-trip WRRCs.

The number of available .NET APIs is limited, however speed and responsiveness are very high.

### Blazor Server

Serves-up static or dynamic pages to clients, based on ASP.NET Core technologies, and utilizes SignalR for back-end communications with each Web Client connection (WebSockets). Back-end data interop is built-in, and web page interactions are handled locally and by the server depending on the type of action.

Useful for for embedded applications and apps running on the local network.

Some limitation on performance due to WRRC round-trip time requirements.

### Blazor Hybrid

Define UI layout and functionality, similar to React and Vue, and integrates with .NET MAUI for managing multi-platform support such as Android, iOS, and Linux. Designed for native apps, desktop, and mobile.

## Blazor vs Razor

Blazor utilizes Razor Components, which are specially crafed Razor pages, using Razor syntax to integrate C# with HTML.

### Razor Components

Razor Components are Pascal-case files with an extension of `.razor`:

- Contain C# and HTML.
- Razor Syntax provide additional markup, usually beginning with the `@` character.
- Razor Markup allows defining the `@page` (URL Path) of the component, and where C# `@code` is allowed within the HTML markup.
- Razor Markup allows Expressions within HTML code through use of the `@` as well, i.e. `<h3>My @webSiteName</h3>`.

Deploy a new Razor Component using 'dotnet' like so `dotnet new razorcomponent -n ComponentName -o Pages`. This will create a new Razor Component named `ComponentName.razor` in the folder `Pages` of an existing Blazor Server Project.

## Build and Run Blazor

To build Blazor Server use the same methods as with other projects (`dotnet build` or 'F6' using Visual Studio).

To build and run Blazor Server and force it up restart when code is changed (ala `nodemon`) use `dotnet watch` in the Terminal or PowerShell console in the Blazor Server Project path.

### MVC Controllers

- Use `Microsoft.AspNetCore.Mvc` namespace at the top of a Class definition.
- Add `[Route(string)]` and `[ApiController]` attributes to designate the class as an MVC Controller.
- CTOR-Inject any required services just like any other class.
- Use `[HttpGet]`, `[HttpPost]`, `[HttpPatch]`, `[HttpDelete]` (etc) REST call definitions to identify each Controller Method as an HTTP/API endpoint.

## Blazor Share Data Between Components

There are 3 ways to do this:

- Use Component Parameters: Parent component provides parameter values to the child component.
- Use Cascading Parameters: Parent component provides parameter values via child component(s) to grand-children component(s).
- Share Data using AppState.

### Component Parameters

- Useful for passing data from Parent Components to Child Component Fragments.
- Component Fragments are designed to only render a single Control or small subset for the Parent Component.
- Child Components do _not_ automatically have access to the same data the Parent Component might have.
- Define Component Parameters _in the child component_ and then set their value(s) _from the parent component_.
- Use `[Parameter]` attribute to identify the Component Parameter in the Child Component.
- Use `<ChildComponent Param=Value />` syntax to assign a value to the Component Parameter in the Parent Component.

```c#
// child Component
<h1>Hello @Name</h1>

@code {
  [Parameter]
  public string Name {get; set;}
  ...
}
```

```c#
// parent Component
<h1>The computer says <ChildComponent Name=@UserName /></h1>

@code {
  public string UserName = "Anony Mouse";
  ...
}
```

See [Razor Lifecycle Events](https://learn.microsoft.com/en-us/aspnet/core/blazor/components/lifecycle?view=aspnetcore-8.0#when-parameters-are-set-setparametersasync) for details about when parameters are set and how to manage that event.

### Cascading Parameters

- Used for passing data farther down the Component hierarchy requires using `CascadingParameters`.
- Use `[CascadingParameter(Key=string)]` to define the Cascading Parameter in the Component Fragment.
- Use `<CascadingValue Key=string Value=string>` and `</CascadingValue>` to _wrap_ descendent Component elements so they have access to the Cascading Parameter(s).

_Note_: Objects can be passed using Cascading Parameters - it is not limited to value-type variables.

### AppState

Define the properties to store in a new Class and register it as a scoped service:

1. Create a new class with the parameters necessary to represent "state".
2. Register the Class in `Program.cs` as a scoped service: `builder.Services.AddScoped<StateObject>();`.
3. Inject the registered class into any Component that needs to use it using Razor Syntax: `@inject StateObject stateObj`.

## Blazor Data Binding in Blazor

When an HTML element value is changed, the web page must be refreshed to show it.

- In HTML + JS, this requires additional code.
- Blazor Server enables data _binding_ to avoid having to write data-refresh code.
- Razor syntax `@bind` does the hard work for you.
- `@bind` understands whether `value`, `checked`, `content` or some other attribute is necessary to bind with, based on the element type it is attached to.

Bindings work on events, too:

- `onchange` DOM event: This is default trigger.
- `oninput` fires whenever any character is entered into a TextBox, for example.
- Bind to events using `@bind-value` and `@bind-value:event` directives.

### Bound Value Formatting

Use the `@bind:format` directive to update formatting.

See [Format Strings in Blazor Documentation](https://learn.microsoft.com/en-us/aspnet/core/blazor/components/data-binding#format-strings-1) for details on when `@bind:format` can be used.

_Note_: It is still possible to use pure C# string formatting techniques to apply:

- Specialized formatting rules.
- Culture-based formatting styles.

## Blazor Pages, Routing, Layouts, and Navigation

- Router Component: Improves Blazor App navigation using the NavLink component.
- Route Parameters: Increase Routing functionality.
- Layouts: Reduce duplicate code.

### Blazor Routing

Use `@page` directive and `<NavLink>` component both impact routing.

- `@page` helps configure Routes.
- The query string in the URL contains information for the Router to process.
- Goal is to direct the user request (query) to the correct page component with all information the component needs to render what the user wants.

Router is configured in `App.razor`:

- `<Found Context="routeData">` and `<NotFound>` components tell the Router what to do.
- Route data and Layout information are included in the wrapped `<routeData>` details.
- `<RouteView props...>` defines the RouteData and the DefaultLayout to use.
- If wanted, an entire page can be defined using HTML elements (or another Razor Fragment) to display a page with links (back home etc) in the `<NotFound>` element content.

The `@page` directive:

- Syntax: `@page "/RouteName"`
- Specifies the component should _handle requests directly_.
- More than one `@page` directive can be used to define multiple routes that lead to the same page.

NavigationManager manages handling portions of a URI:

- Full URI: `https://domain.ext/parentRoute/relPath?key=value`
- Base URI: `https://domain.ext`
- Base Relative Path: `parentRoute/relPath`
- Query String: `?key=value`

NavigationManager Usage:

- Must be `@inject`ed into component where values will be used.
- In the example NavigationManager is used to get BaseUri, and that value is assigned to a variable that is called in the Razor syntax within an Anchor Link, providing a link to the Home Page.
- NavigationManager has built-in methods to transform a Uri to an Absolute Uri, or other forms.
- `NavigationManager.NavigateTo(AbsoluteUri | RelativeUri)` will send the user to another component in a code-call. This could be applied to a button `onclick` event, for example.

The `<NavLink>` Component:

- Use these to render Anchor elements to automate toggling the `link:active` style.
- `<NavLink Match="matcher">` manages _when_ the link is highlighted.
- `NavLinkMatch.All`: Only highlighted when href matches _entire current URL_.
- `NavLinkMatch.Prefix`: Only highlighted when href matches _first part of the current URL_. Use this to help the user understand _which section of the website_ they are viewing.
- Is basically a drop-in replacement for `<a href...>` elements.

### Route Parameters

Capture a specifid parameter by using `@page "/BaseRelativePath/{parameter}`. This makes the parameter available to the component, like [Component Parameters](#component-parameters).

- Route parameters are case-insensitive.
- Route parameters are required by default.
- Route parameters will automatically get bound to a component parameter with the same name, by Blazor Router.
- Use a `?` question mark to make a route parameter optional. Set a default value within an appropriate Blazor Lifecycle Event such as `OnInitialized()` or `OnParametersSet()` (depending on what behavior is required).

### Route Constraints

`@page "/BaseRelativePath/{parameter:int}`

Use these to ensure the parameter Type is matched before the Blazor Router sends the parameter to the Component.

Various types are allowed in Route Constraints:

- bool
- datetime
- decimal
- double
- float
- guid
- long

#### Catch-all Route Parameter

Use `*` prefix to capture multiple parameters: `@page"/BaseRelativePath/{*parameter}`

A match of 3 parameters could be stored in a string `[parameter]` on the page and displayed to the user, or processed as input.

### Blazor Layouts

Use Layout Componets to set reusable page fragments for:

- Consistent branding across pages.
- Reduce code duplication and reuse common UI elements.
- Share rendered markup with all components that reference the Layout Component.

Layout files:

- Use the `.razor` extension.
- Use `@code` razor syntax code blocks.
- _Must_ inherit from `LayoutComponentBase`.
- _Must_ include a `@Body` directive in the location where referencing components will render their content.

_Do not_ include an `@page` directive in Layout files - they do not handle requests and do not have routes created for them.

The default Layout file in new Blazor Projects is `Shared/MainLayout.razor`.

Using Layouts in Blazor Components:

1. Add the `@layout` directive with the name of the Layout to apply to this component.
2. Add the `@body` directive to the targeted Layout for the Component to render into.

Apply a Template to all Blazor Components by using `_Imports.razor`. In this case, using `@layout` is not necessary, and instead the rendering will apply to all Components in the same folder as `_Imports.razor`, and all its sub-folders.

Apply a default layout to every Component in _all folders_ by configuring the `<RouteView>` element and the `DefaultLayout` attribute in `App.razor`.

- Simplifies applying a Layout to an entire site.
- Components _can_ still declare their own `@layout` directive that will _override_ the settings from `App.razor`.

App.razor:

- Declares how pages are routed.
- Defines which default Layout is to be used.

## Blazor Forms and Validation

Overview:

- Use Blazor event handlers to improve interactivity.
- Use Forms in Blazor for data entry.
- Server- and Client-side validation of Forms in Blazor.

Events:

- Triggered in the DOM: Clicks, Focus/Lost Focus, Content change, or Lifecycle such as Loading.
- Options are to ignore (usually the default), or run custom event handlers in JS or Blazor C#.
- Most Blazor Events correspond to DOM Events.
- Custom Blazor Events can be written in C# by using Event Binding.
- EventArgs carry information about the Event.
- Blazor Directive `@` is used to identify Blazor-handled Events and custom event handlers in Blazor.
- In JS with JQuery, events run in the client browser.

Event Args:

- Blazor automatically makes these available for Event Handler methods to take as parameters.
- `MouseEventArgs`, ..., all inherit from base `EventArgs` .NET Class.

Blazor Events, Handling:

- In Blazor, Events are handled on the _server_ which only updates the UI when _it needs to be_.
- Events can change state in the UI, which will cause a refresh, or they can change data behind the scenes, which does _not_ require a page refresh. Blazor Server handles that _for you_.
- Blazor Server allows Event Handlers to access _static data_ between sessions (JS does not).
- For events like `mousemove` or other common events that don't change UI state, it might be better to handle the event client-side using JavaScript.
- Supressing default behavior is possible in Blazor by adding `:preventDefault` to the `<input>` element attributes list. See example below.

```c#
// code reference: MSLearn "Blazor Improve How Forms Work
<input value=@data @onkeypress="ProcessKeyPress" @onkeypress:preventDefault />`
```

Asynchronous Event Handling:

- Blazor event handlers are _not async_ by default and _will block_.
- Designate event handlers as `async` with an appropriate return like `Task` or `Task<T>` to free the UI thread when the `await` operator is used.

`FocusAsync` method:

- Force the user to focus on a specific page element, regardless of Tab Order.
- Create an `ElementReference` field to store the InputField reference.
- Use `@ref` attribute in-line with the HTML to tie-in the event to the handler.
- Write the async Task event handlers for `ChangeFocus()` and `HandleFocus()` to perform actions.

```c#
// code reference: MSLearn "Blazor Improve How Forms Work"
<button @onclick="ChangeFocus">Click to change focus</button>
<input @ref=InputField @onfocus="HandleFocus" value="@data" />
@code {
  private ElementReference InputField;
  private string data;
  private async Task ChangeFocus()
  {
    await InputField.FocusAsync();
  }
  private async Task HandleFocus()
  {
    data = "Received focus";
  }
}
```

_Note_: This example is not best practice. Forcing focus to a specific element is best utilize when there is an error on an input, especially within a Form, and the user needs to change the incorrect input before continuing. Avoid using this code to force users' navigation through a page.

Inline Event Handlers:

- Lambda expressions are supported, and will create an anonymous function.
- Use Lambdas for _simple_ event handlers that don't need to be reused anywhere else.
- Write the Lamgda _inline with the HTML_.

Event Default Behaviors and Propagation:

- See above code regarding `preventDefault` property on the input element event attribute. This is useful when _only the event handler code_ should be run, but screen-update(s) should _not happen_.
- Recall that events propagate _up the DOM tree_ and if the Parent pages shouldn't operate on an event, leveraging `stopPropagation` attribute will keep parent event handlers from handling the same event type triggered by a descendant.

Event Callbacks:

- Use these to handle events across components.
- A descendant can call a Parent or Grand-parent component's event handler with an event callback.
- Event Callbacks take a single parameter `EventCallback<T>` that carries the data.
- Use `[Parameter]` attribute on a `public` property of type `EventCallback<T>` where 'T' is the type of Event that is being captured.
- The Event Callback is propagated similarly to [Cascading Parameters](#cascading-parameters).
- Use appropriate typed `EventArgs` parameters to directly wire-up the event callback.
- The grand/parent component must have an appropriatly types handler method for the event callback.

### Blazor EditForm

Input and Form are common web elements to capture user inputs. Blazor adds-on to these with capabilities to validate and manipulate form inputs.

The EditForm:

- Takes the place of a standard HTML `<form>` element.
- Includes data binding to assciate an Object with the form.
- Validation through use of attributes and validation rules.
- Submission: Follows the Blazor Event Model using C# event handlers to capture the `OnSubmit` event.
- Input elements: Blazor adds to the standard HTML `<input>` element to implement binding and validation features.
- Implementes _two-way binding_ by default!

To create an EditForm with Data Binding:

1. Create a public class that defines the form input elements as public properties.
2. Bind the EditForm to the model using a standard private property in the Razor page that implements the Type of the Form. For example, if a new user Form is asking for username and email address, a new Class can be created to represent the Form data such as `public class NewFormUser { public string UserName { get; set; } ...}` etc.
3. `@inject` any service that provides a factory for the class, or other functionality that supports the Form-generated class.
4. Implement event handlers to do things like pre-load an EditForm with existing data using a `OnInitializedAsync()`, or to handle changes in specific Input elements such as a button click or item selection.

### Blazor Control Input Components

Each Blazor Input Component is rendered as a specific HTML element as explained in this table from [MS Learn](https://learn.microosft.com/en-us/training/modules/blazor-improve-how-forms-work):

| Input component      | Rendered as (HTML) |
|----------------------|--------------------|
| `InputCheckbox`        | `<input type="checkbox">` |
| `InputDate<TValue>`    | `<input type="date">` |
| `InputFile`            | `<input type="file">` |
| `InputNumber<TValue>`  | `<input type="number">` |
| `InputRadio<TValue>`   | `<input type="radio">` |
| `InputRadioGroup<TValue>` | Group of child radio buttons |
| `InputSelect<TValue>`  | `<select>` |
| `InputText`            | `<input>` |
| `InputTextArea`       | `<textarea>` |

About Blazor Control Input Components:

- Elements have attributes including `@ref` for referencing C# variables.
- Unrecognized elements are not changed by Blazor and are passed to the HTML renderer.
- Mixing Blazor Controls with standard HTML controls is supported.

### Form Submission

Declarative client-side validations are performed prior to sending to server-side.

- Basic input errors such as too long, or missing character classes.
- Other errors including skipped required fields or incorrect data types.

Server-side enables handling complex validations:

- Compare data against existing database data such a duplicate or bad lookup value.
- Processing errors such as invalid classifications based on several form input datum.
- Unauthorized or unauthenticated submissions.
- Stict type checking.

EditForm Events:

- `OnValidSubmit`: Input fields all pass validation rules (attributes). Use for basic validation.
- `OnInvalidSubmit`: One or more input fields fail validation rules. Use for basic validation.
- `OnSubmit`: Regardless of valid/invalid state, this event is fired. Use when data should be processed by more complex validation functions.
- Pick either the top 2, or the bottom one, but _not all three_. This is _not checked at build time_ and could result in a Run Time error if `OnSubmit` is used when either/both of the other 2 are used as well.

EditContext object:

- Data from the EditForm are instantiated in a new EditContext instance.
- This is the parameter for `submit` events.
- Event handlers can use the `Model` field to retrieve the inputted values.

Validation Failure Notification:

- Create an element to capture the value of a parameter that is set with a value when there is a validation error.
- This way, every time validation occurs, a message appears when validation fails, or the message is removed if validation succeeds.

### Annotate Models For Validation

Validate user input as soon as possible in Blazor Forms:

- Missing information can make an order impossible to complete.
- Null or corrupt values can cause the code to misbehave or the website to crash.
- Nefariously injected code can be a security or denial-of-service threat.

Use the following to help users understand what is necessary:

- Use a label to idenfity the field as required.
- Use colorization, highlighting, or changes in an input border to identify areas where the user needs to focus.
- Green outlines usually portray "valid" or "good", and red outlines usually portray a problem that the user needs to resolve.
- Use messages somewhere near the form that explain what (if any) problems there are with the input.
- Failed validation messages should tell the user what must be done to fix them e.g. Phone numbers must be at least 10 digits including an area code.

Many annotations are available including:

- ValidationNever
- CreditCard
- Compare
- Phone
- RegularExpression
- StringLength
- Url

### Control Blazor Form Validation

Field Validation: User tabs _out_ of a field.

Model Validation: User _submits_ the form and validation is handled server-side.

- `<DataAnnotationsValidator />`: Checks the model annotations against the entered values.
- `<ValidationSummary />`: Displays a summary of validation errors.

To implement Field Validations (client-side):

1. Add annotations to the model: `[Required]`, `[EmailAddress]`, [Range(int start, int stop)]`, etc.
2. Include messages in the annotations such as `[Required(ErrorMessage = "Phone number is required")]`
3. Add `<DataAnnotationsValidator />` and `<ValidationSummary />` Blazor Elements to the `<EditForm>` so that the validation attributes are utilized.

To implement Model Validations (server-side) using `OnSubmit`:

1. Annotations are still necessary.
2. Use `EditContext` parameter for checking input data: `editContext.Validate()`.
3. Write handlers with validation logic.
4. Add `<ValidationMessage For="@(() => model.Property)" />` to execute a lambda indicating validation errors.

To implement Model Validations (server-side) using `OnValidSubmit` and `OnInvalidSubmit`:

1. Annotations are still necessary.
2. Add `OnValidSubmit=@OnValidHandler` and `OnInvalidSubmit=@OnInvalidHandler` to the `<EditForm>` attributes.
3. Implement the `OnValidSubmit()` and `OnInvalidSubmit()` handlers that take `EditContext editContext` as a parameter.
4. For `OnValidSubmit()` implement storing the valid data in the handler.
5. For `OnInvalidSubmit()` impelment activating an error message explaining what the user needs to do.

### Custom Validation Attributes

Create one only if the existing Validation Attributes are not sophisticated enough to validate a particular case:

- Create a class that inherits from `ValidationAttribute`.
- Override the `IsValid` method.
- Impelment the validation function in the `IsValid` method.
- Add the custom validation attribute to the model class.

### Server-Side Form Validation

When using `OnValidSubmit()` and `OnInvalidSubmit()`, server-side validation is triggered:

- Validate form inputs against an annotated class via the `<DataAnnotationsValidator />` element.
- Provide rich validation messaging to the user within the Form via `<ValidationSummary />`.
- Perform deeper validation such as RegEx or validation against other data sources prior to storing user-inputted data.

## Leverage JavaScript and Template Components in Blazor

Use JS Interop to execute JavaScript Libraries and functions from Blazor apps.

### JS Blazor Interop

- For the most part, JavaScript is not necessary in Blazor.
- Existing JavaScript Libraries can be helpful in many situations.
- Custom JS Code can also be reused.
- JS Interop allows callsing JavaScript, and allows calling .NET _from_ JavaScript.
- Use `<script>` tag to load JavaScript code in Blazor. Can be a `.js` file ref or in-line JS code.
- Add custom JS script tag just after the `<script src="_framework/blazor.*.js"></script>` block in `Pages/_Host.cshtml`.
- Avoid adding script blocks to the `<head>` element of a page because Blazor only controls content within the `<body>` element.
- Use `IJSRuntime` to call a JavaScript function from .NET code by `@inject`ing into the Component.
- `InvokeAsync` and `InvokeVoidAsync` become available to run JavaScript code. Use `await` as per usual.

### Blazor JS Interop Failure Modes

If SignalR has not made a connection between the server and the web page, JS Interop will fail.

- Once rendering lifecycle event fires, the SignalR channel is open.
- Use `OnAfterRender` or `OnAfterRenderAsync` to detect when rendering has completed.
- Updating the DOM with custom JavaScript can cause the DOM copy at the server to become out of sync with the web page. Avoid doing this!

### Use ElementReference To Update The DOM

- Create a placeholder element in the Blazor component like `div @ref="placeHolder"></div>` so that Blazor does _not_ attempt to track its contents. Add JavaScript elements here to avoid corrupting server-side DOM copy.
- `ElementReference` holds the reference to the empty element as a field.
- Passed-in JavaScript functions use this reference to add content to the empty div element, safely.

### Call .NET From JS

Use `invokeMethod` and `invokeMethodAsync` helper functions. The async version returns a JavaScript `promise`.

- Devine the callback .NET Method as async.
- Return type must be void or _better yet_ `Task` or `Task<T>` where T is JsonSerializable.
- Provide the name of the assembly that has the static method so the function can call it back.
- `JSInvokable` attribute allows specifying an alias for the method reference name.
- `DotNetObjectReference` is provided by JS Interop to create an object ref in .NET code so it can be safely passed to JavaScript code.
- Be sure to dispose the object ref when done to avoid memory leaks.

## Blazor Component Lifecycle

Tracks a Component from creation through destruction:

1. Initialization
2. SetParametersAsync
3. OnInitialized and OnInitializedAsync _Note_: These will cause a call to StateHasChanged
4. OnParametersSet and OnParametersSetAsync _Note_: These will cause a call to StateHasChanged
5. Render UI :arrow_left: BuildRenderTree :arrow_left: ShouldRender :arrow_left: StateHasChanged :arrow_left: Possible UI or External events, or awaited calls from step 3 and 4.
6. OnAfterRender and OnAfterRenderAsync
7. Dispose and DisposeAsync

Handle an Event by overriding the corresponding method.

Multiple Render cycles might happen before a page finishes rendering.

A `ParameterView` object is used to pass parameters between Components.

The `SetParametersAsync` method accepts `ParameterView` in its argument list. Therefore, calling `base.SetParametersAsyc` with your own parameters will inject new "state" into the initializing Component. Also, any processing the parameters need prior to this Component rendering them should be done here.

Overriding Lifecycle Parameters is a common practice to handle specific needs at various places during the Component lifecycle.

Use `SetParametersAsync` to _reinitialize_ a Component when the paremeters change.

### Blazor Render Mode And Component Lifecycle

Set `render-mode` in `Pages/_Host.cshtml` controls which Component Lifecycle Methods are available:

- Set to `Server`: `OnInitialized` and `OnInitializedAsync` methods run only _once per instance_.
- Set to `ServerPrerendered`: `OnInitialized` and `OnInitializedAsync` methods run _twice_: Once during _prerender_ phase (generates static page output), and _again_ when SignalR connects with the browser. Therefore when retreiving or processing data in this method overrides, _cache_ the operation output the first time and _avoid running it again_ to reduce UI load latency.

Objects that are injected by Component dependencies can be used within `OnInitialized` and `OnInitializedAsync` methods _but not before_.

_Note_: Calls to JavaScript code _will not work_ during prerender phase. Instead, add JS Interop processing to `OnAfterRender` and `OnAfterRenderAsync` method overrides.

Use `OnParametersSet` and `OnParamtersSetAsync` to complete initialization tasks taht depend on compontn parameter values i.e. Calculating values for display or instance properties. Keep the processing short to avoid UI load latency.

About `OnAfterRender` and `OnAfterRenderAsync`:

- Run _every time_ the Blazor Runtime needs to update the view.
- Runs when `OnInitialized` or `OnInitializedAsync`, or `OnParametersSet` or `OnParametersSetAsync` methods run.
- Anytime a UI Event is triggered.
- App code calls `StateHasChanged()` Component method.

Order of invokation following call to `StateHasChanged()`:

1. `StateHasChanged`: Component is marked for rerendering.
2. `ShouldRender`: Getter returns boolean 'should render'. This method _can be overridden_ but must return boolean.
3. `BuildRenderTree`: Renders the component. Can be overriden to build the render tree in a custom way.

About `bool firstRender`:

- `OnAfterRender` and `OnAfterRenderAsync` parameters list accepts `bool firstRender`.
- `firstRender` is `true` th first time the method is run, and `false` after that.
- Evaluate this parameter to do one-time operations like retreiving (and caching) data, so the operation is only initialized once.

### Dispose and DisposeAsync

Release any unmanaged resources by implementing one or both of these methods.

### Lifecycle Exceptions and SignalR

The SignalR connection will be closed if an Exception is thrown!

Blazor _stops functioning_ at this point.

Be sure to _handle exceptions_ as part of the logic of Lifecycle Methods to ensure the SignalR connection remains open!

### Common Blazory Things To Know and Understand

- To _register_ a data access service to the Blazor Server application, implement a Data Model and a Service that can call an ORM or obtain the data from a file or REST call (etc), then register the data access Service in `Program.cs` like `builder.Services.AddSingleton<DataGetterService>();`.
- OnInitializedAsync(): Event fires when component's initialization is complete and it has received initial parameters but the page has not rendered yet. Override this method to fetch data asynchronously.
- Work with data access services by using the Blazor Directive `@inject`.
- EntityFrameworkCore 6.0.8 supports Sqlite 6.0.8 and integrates well with Blazor Server.
- Adding EntityFrameworkCore and registering a `DbSet<T>` allows adding an ASP.NET Controller that can access the database data.
- If an _error page_ is returned after creating a new `Controller`, be sure to use `cURL` or similar to query the path and see what is actually returned. _A common scenario_ is routing is not correct and the returned page is _not_ the MVC Controller content, but an _error page_.
- When passing Parameters around, use `Microsoft.AspNetCore.Components.EventCallback`. This is an event handler delegate type (struct) that can be used to cast an event handler (i.e. onclick() or lambda) to a parameter on the Fragment/Child Razor Component. Similar to passing a function using React `props`.
- Blazor Server _maintains a copy of the client-side DOM_. Avoid corrupting this but _not_ updating the DOM server-side.
- JavaScript code can be injected using `@inject IJSRuntime JS` in the top portion of a Razor Page. Utilize the `JS` Runtime code like you would anywhere else, such as in an event handler: `await JS.InvokeVoidAsync("alert", msg);`. This is called _JavaScript Interop_, and it enables doing things in JS, that Blazor cannot do natively.
- When using JavaScript Interop and calling `InvokeAsync<T>()` to run JavaScript code, it might be necessary to include _triple quotes_, which enforces a literal string to be passed, for times when embedded quote marks are necessary in the encapsulated JavaScript code.
- There are 3 ways to include JavaScript code into HTML: Write the code in-line within a `<script>` element, reference a JavaScript library on the file system within a `<script>` element, or reference a _remote JavaScript package_ by referencing a web url i.e. `<script src="https://cdn.jsdelivr.net/npm/package@latest/dist/thePackage.min.js"></script>`.
- Implement an Interface in a Razor Component using `@implements`, such as `@implements IDisposable`, then implement the required method(s).
- Force a Component to _rerender_ by calling `StateHasChanged()`, a Component built-in method!
- Remember: The entire point of a component is to display a page with a state, therefore the Component Lifecycle _must be adhered to_, ensuring the page rendering is correct for the state of the data it carries or updates.
- CTOR Injection is _not supported_ in Blazor Components. Use `@inject` syntax instead.


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

### Data Binding in ASP.NET

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

[ASP.NET Core Blazor Event Handling](https://learn.microsoft.com/en-us/aspnet/core/blazor/components/event-handling?view=aspnetcore-8.0).

[ASP.NET Core Blazor Forms Overview](https://learn.microsoft.com/en-us/aspnet/core/blazor/forms/?view=aspnetcore-8.0).

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../READMD.html)
