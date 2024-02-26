# Nojronablog 2024

A space for collecting thoughts and technical walk-thrus and takeaways during my coding journey through CY 2024.

## Week 8

### Community Toolkit MVVM

Began reading up on DotNET Foundation project `CommunityToolkit MVVM`. I'm a little worried about this project but initial impressions are it is a handy code-generator for things like object observability, notification, commanding, and messaging in WPF (and UWP, Xamarin, and possibly others).

- Toolkit is very modular and easy to pick and use just the features that are wanted.
- Code generation (build-time) is pretty snappy and appears to do "all the right things".
- During the build, documentation claims code trimming is leveraged to remove unused partial implementations that are generated but not implemented (or overridden and referenced).

I'll do some experimentation before I decide whether to utilize the CommunityToolkit for BF-BMX.

### WPF - An Observable Queue?

I had a silly question, wondering if a WPF control could display a Queue of items. To further complicate the question, the queue would be accessed asynchronously by another process to enqueue and dequeue items.

- It appears WPF Controls like ListView are not natively capable of viewing items within a Queue or Stack. Understandable.
- ListView _can_ enumerate items in a `List<T>`.
- Adding enumeration to a Queue would take a bit of work.
- Overriding inherited `List` members to make it _look and act like a Queue_ makes sense.
- Ensuring all of the Notification infrastructure is in place is not too much work (although with Attribute-based code generation it gets a little abstract and confusing).

I came up with a Synchronous solution that involves inheriting from `List<T>` and overriding `InsertItem()` and `RemoveItem()`, and also adding `Enqueue(Object)` and `Dequeue()` methods for code readability.

First, set up EventArgs for the custom queue:

```c#
public class PersonChangedEventArgs : EventArgs
{
  public readonly Person ChangedItem;
  public readonly ChangeType ChangeType;
  public readonly Person? ReplacedWith;

  public PersonChangedEventArgs(ChangeType change, Person item, Person? replacement)
  {
    ChangedItem = item;
    ChangeType = change;
    ReplacedWith = replacement;
  }
}

public enum ChangeType
{
  Added,
  Removed,
  Replaced,
  Cleared
};
```

Next, inherit from `ObservableCollection<T>` and insert EventHandlers:

```c#
public partial class ObservableQueue : ObservableCollection<Person>
{
  public event EventHandler<PersonChangedEventArgs>? Changed;
  public List<Person> People { get; } = new List<Person>();

  // add an instance to the end of the List
  public void Enqueue(Person person)
  {
    People.Add(person);
    base.InsertItem(Count, person);
  }

  protected override void InsertItem(int index, Person newItem)
  {
    base.InsertItem(index, newItem);
    EventHandler<PersonChangedEventArgs>? temp = Changed;
    if (temp != null)
    {
        temp(this, new PersonChangedEventArgs(ChangeType.Added, newItem, null));
    }
  }

  // remove the first item (lowest indexed) from the List
  public void Dequeue()
  {
    RemoveItem(0);
  }

  protected override void RemoveItem(int index)
  {
    Person removedItem = Items[index];
    base.RemoveItem(index);
    EventHandler<PersonChangedEventArgs>? temp = Changed;
    if (temp != null)
    {
      temp(this, new PersonChangedEventArgs(ChangeType.Removed, removedItem, null));
    }
  }
}
```

Then, in the ViewModel, implement the code-generating Attributes:

```c#
public partial class MainWindowViewModel : ObservableValidator
{
  [ObservableProperty]
  private ObservableQueue people = new();
  // other observable property fields here like FirstName, LastName, etc
  [ObservableProperty]
  private string addPersonButtonText = "Add Person To Database";
  [ObservableProperty]
  private string removePersonButtonText = "Remove Person From Database";
  public string FullName => $"{FirstName} {LastName}";
  [RelayCommand(CanExecute = nameof(CanSetName))]
  public void AddPerson()
  {
    // instantiate newPerson and other processing, logging, etc code here
    People.Enqueue(newPerson); // add to end of the list (highest index)
    PeopleCount++;
    OnPropertyChanged(nameof(PeopleCount)); // notify change in count
    // null-out newPerson and FirstName and LastName fields
  }

  public bool CanSetName()
  {
    // if FirstName and LastName have text in them...
    AddPersonButtonText = $"Add {Fullname} To Database";
    OnPropertyChanged(nameof(AddPersonButtonText));
    return true;
    // else, log this situation...etc
    return false;
  }

  [RelayCommand(CanExecute = nameof(CanRemovePerson))]
  public void RemovePerson()
  {
    // other processing, logging, etc code here
    People.Dequeue(); // first item in the list
    PeopleCount--;
    OnPropertyChanged(nameof(PeopleCount));
  }

  public bool CanRemovePerson()
  {
    RemovePersonButtonText = $"Remove Person from DB ({PeopleCount})";
    OnPropertyChanged(nameof(RemovePersonButtonText)); // notify of button text change
    // if additional processing is necessary, expand
    // the return statement to a full if-then code block
    return PeopleCount > 0 ;
  }
}
```

Implementing asynchronous operations would be the next step, and enabling concurrent access to the List will be another hurdle. If the above code is used, added code to enable async and thread safe concurrency will be posted here.

### End of Week 8 Comments

The last few days I have been working on implementing code and tests for the BF-BMX project. I realized there was room for improvement in defining some data details so I'm reaching out to the primary end user to get their preference on what the data should look like. This shouldn't block my progress at all, but might require some refactoring later, depending on what the response is.

There will be several interruptions in the upcoming weeks that will slow project progress, so this next week will be a big push week to get the core of the BF-BMX project ready for building-out and testing functionality. I have time to get this done before Beta testing begins, but I want to stay ahead of the schedule as much as is practical.

## Week 7

Made some good progress the last few days with WPF Input Validation, implementing async functionality, and backup/restore of in-memory data (which was largely completed in week 6).

### WPF Input Validation

I'll overview [Tosker's Corner](https://www.youtube.com/watch?v=5KF0GGObuAQ&ab_channel=ToskersCorner) demonstrations of using input validation in the next four subsections.

Also check out [this response by StackOverflow user MrB](https://stackoverflow.com/questions/19539492/implement-validation-for-wpf-textboxes) for more.

_Remember_: Updates to properties must include notifications, for example `IObservableCollection`, or `INotifyPropertyChanged`, etc implementations.

ToskersCorner introduces four ways to accomplish validating input in WPF:

- By Exception
- By IDataErrorInfo
- By ValidationRule
- By Annotations

A couple of these actually rely on Validation by Exception behind the scenes, so there is plenty of crossover.

See my notes in [Conted: WPF MVVM Learnings](./wpf-mvvm-learnings.html#wpf-input-validation).

### Asynchronous Programming

This is a real rabbit hole, but it is pretty interesting albeit complex. I've written some notes in [dotnet async await notes](./dotnet-async-await-notes.html) to force my brain to process what Stephen Cleary is saying in his blog post/essay.

Some key takeaways:

- Do not mix synchronous and asynchronous code in GUI apps like ASP.NET, WPF, etc.
- Console App uses a Thread Pool that allows mixing sync and async code.
- ASP.NET and other GUI apps have a GUI Thread follow a 'one-chunk-at-a-time' thread calls, providing separate Contexts for the GUI and ASP.NET Controllers.
- Async methods need to return `Task` or `Task<T>`.
- Event Handlers are the _only_ method type that can return an async void.
- Prefer using `await Task.WhenAny()` and `await Task.WhenAll()` (use the await keyword).
- If a delay is needed, use `await Task.Delay()` instead of sleeping a Thread.
- If a Task Context must be changed using `ConfigureAwait(false)`, be aware that returning a result to the GUI thread will require additional code, so it is easier to add "fire and forget code" when using `ConfigureAwait(false)`.

For BF-BMX, I will probably want to look into using `AsyncCollection<T>` to manage multiple processes pushing data to a common repository.

I've added notes about TAP and Aynchronous programming patterns in [DotNET Aync Await Notes](./dotnet-async-await-notes.html).

The next thing to check out is [Data Structures for Parallel Programming](https://learn.microsoft.com/en-us/dotnet/standard/parallel-programming/data-structures-for-parallel-programming) at MSFT Learn - I have a feeling this will provide even more insight into patterns that could come in handly when developing BF-BMX.

### Feb 17 DSA

The other night I had a nightmare that I couldn't depict how to zip Linked Lists on paper. I took that as a sign that I am out of practice with DSA exercises. So I took a quick side-trek to review "Big-O Notation", and will prepare for a more regular review of algorithm and data structure challenges to keep my interviewing brain fresh.

### MVVM Cross

An open-source project supported by the DotNET Foundation, applies MVVM pattern to WPF, iOS, Android, and other platforms. I took a look at MVVM Cross as a possible framework to use in BF-BMX, replacing Caliburn Micro. Here are a few key takeaways:

- It is difficult to set up initially.
- There are templates to help get a project setup to start, but it is unclear whether these templates are fully supported in (or by) VSCode.
- There is a "Core" project and then "platform" projects (for example: WPF, or Ios) that make up an MVVM Cross Solution. Essentially it breaks down to the core MVVM framework bits and the developer implemented Models and ViewModels are placed in the "Core" project, and the developer designed Views are put in the "platform" project.
- The MVVM Cross documentation is voluminous, however I had a difficult time reading through it to get things up and running. I'm pretty context-sensitive so it's probably me, not them.
- Several references to how to set up MVVM Cross were out of date (MVVM Cross is currently at 9.1.1), dating back two or more years.
- In the end I developed a basic project following Time Corey's instructions (in an outdated video) and by following several MVVM Cross bugs, Example projects, and StackOverflow.

### Mobile Weather App Downloading Images

In the [Interleaving section of MSFT Learn article on Task-based Asynchronous Pattern](https://learn.microsoft.com/en-us/dotnet/standard/asynchronous-programming-patterns/consuming-the-task-based-asynchronous-pattern#interleaving), example code shows how to utilize `Task.WhenAny(func)` to download images for display to a UI, as they become available. This will apply nicely to Mob-Wx on the 7-day forecasts page.

## Week 6

Although I was out of town for most of week 5 some software development happened anyway:

- Challenged myself to create an ADIF file validation tool for very specific log files. This was mostly successful in that I have a working console app with separate library classes and a unit test project, and it provided lots of opportunity to refresh my memory on use of _Regex_ and its Syntax and best practices. Also, it provided an opportunity to use `dotnet` to build the solution from scratch, and manually add the Library and Unittest projects.
- Reorganized my plan for the MobWxApp. It is going longer than I had originally intended it to, and I have another project that I promised to deliver in a couple months so I need to move-on from MobWxApp for now. I intended to have it pushed to the Android Play Store, but that will have to wait. Meanwhile, I've cleaned up the UI and the data models a bit, and have generated another Release Build that I will be using on my personal Android phone.

### Iterating Through Characters In A String

- Use `string.IndexOf(char)` instead to avoid iterating.
- Leverage `Regex.Match` for single-instance searching within a string, and `Regex.Matches` for locating multiple instances of a string.
- `Match` and `Matches` have helpful properties like `Count` and `StartingIndex` that are probably more efficient than a `for` or `foreach` construct.

### Method Wrapping

While building the ADIF validator toy, I found myself creating "wrapper methods" to the library methods that actually did the work.

- This allowed the Console project to provide minimal information to get the Library method to fire, through a method proxy that would add the correct information for the Library function. This abstracts-away the complexity from the Console project.
- In the future I should _reconsider_ having wrapper methods do another other work that simply supplying details on behalf of the caller. Having the parent wrapper method change data before sending it to the child method makes bug-hunting and testing more difficult, with no other real benefit.
- Test the wrapper function _thoroughly_ prior to wiring-up the child (wrapped) method. Then don't edit the parent function again (or risk adding bugs that are difficult to find and squash).
- Try refactoring the code so that wrapper methods aren't necessary. This could be accomplished with a `ConsoleLib` class that is only used by a Console UI, or some other library that basically acts as an API but otherwise does not analyze or change any data passed in either direction.

### BF BMX Kickoff

Started working on the Bigfoot Bib Message eXtractor project. My current approach to development is:

- Start by designing and building the service that will access and process files.
- Focus on the data logging portion so other participants in the larger scope of this project have a chance to provide input or refine their tools before launch.
- Ensure unittests exist and pass for each component.
- Maintain a stable app that manages Exceptions so it can continue to operate without human intervention.
- Research other implementation details as necessary along the way.

There are still some questions I need to get answers to (non-exhaustive list):

- How to safely run and monitor multiple file-tracking service instances? Would it be better to just launch multiple client-side apps, or is there a simple enough way to manage multiple threaded tasks?
- Is Self-Contained App deployment supported in .NET 6? The app will need to support deployment to non-dev machines running Windows 10 and Windows 11.
- Sensible locations for logs.
- Sensible Environment Variable names (and not too many of them) so they are easy to remember and set.
- Whether or not to implement a local database feature. Generally this seems like a good idea, but comes with its own set of complexities. Maybe address this in a later cycle or if there is time prior to launch?

Exploring ways to get the API Server to utilize a database, item Collection, and logging. Here are a few takeaways:

- Set the ILogger instance to the Class it will be used in, for example `private readonly ILogger<MyClass> _logger;`, otherwise DI cannot inject it into that Class, and compile will fail.
- EF and EF Core (see notes in next subsection).
- Observable Collection is the way to go when it comes to updating other objects, especially the UI, whenever the collection changes.
- Other Collection features can include _being the interface to the database_ so that whenever data is CRUD in the Collection, it is also CRUD in the database.

Exploring file monitoring, asynchronous code, and regular expressions. Here are a few takeaways:

- Microsoft Regex documentation is a little wonky. For example, in the API documentation there are no formal sub-section entries for `Match.Value` and `Match.Success`, yet those properties (and some other methods) exist and are listed in an expansive table! [.NET 6 API Match Class](https://learn.microsoft.com/en-us/dotnet/api/system.text.regularexpressions.match?view=net-6.0)
- Leveraging async-await and Cancellation Tokens sounds like a good idea in order to get file monitor to monitor more than one directory, and process files as they are discovered, and log results.

### Entity Framework and EF Core

This 5-page feature comparison of EF Core and EF6 is probably the best TLDR: [MSFT Learn: Compare EF Core and EF6](https://learn.microsoft.com/en-us/ef/efcore-and-ef6/). It really pushes the idea that EF Core is the way to go with new projects. That's fine, but `which` EF Core? Turns out there are versions of EF Core that are not supported outside of .NET Core, .NET Framework, and .NET Standard 2.0. That's also fine, but it forces designers and developers of _existing_ products that use Entity Framework to more to EF Core (and cross their fingers) or stay with Entity Framework, which is very stable and reliable at this point. What is EF falls out of support completely, and EF Core doesn't support the features your application (or system) rely on?

Tough questions there. Thankfully, I am not going to worry (much) about using either one, outside of the immediate compatibility and feature requirements my current project needs.

Another sticky point is MSFT touts EF and EF Core as having support for so many database interfaces. While it is true there are multiple caveats and tradeoffs to consider. One example is Sqlite - It is supported, and there are EF/EF Core extensions that provide for integrating Sqlite, but Sqlite itself is less focused on being EF/EF Core compatible (and frankly, Windows-ready it seems). While Sqlite _is certainly_ in use and a good solution for many software shops on Windows, I'm chosing to not use it for this project to avoid headaches with platform and framework compatibility and interoperability.

So, I'm going to settle on EF Core and "In Memory Database" as a simple alternative to relying on only collections, or using EF/EF Core with SQL Server or Sqlite. More likely, I'll look to building a [Dapper ORM](https://github.com/DapperLib/Dapper) data layer, as is described by [Tim Corey in his YouTube video Data Access with Dapper and SQL - Minimal API Project Part 1](https://www.youtube.com/watch?v=dwMFg6uxQ0I) where he is using ASP.NET Core Web API in .NET 6.

### Old Project Unittests

I picked up where I left off with an exploratory project back in November 2023. At least 2 unittests were not working properly, and one of those was failing outright. At the time I had not worked out why the failing test was having the problem. Today I was able to sort it out:

- The collection inherited from `ObservableCollection<T>`, avoiding lots of boilerplate event handlers and `OnChanged()` coding.
- In what is now an obviously silly move, I had added a private `IList<T>` field to act as the collection. This is not necessary as the inherited `ObservableCollection<T>` manages an internal list, so the field was removed and implementing `IList<T>` on the class was no longer necessary.
- Some wrapper code I developed was handling add and remove functions, but were pointing to the shadowing list rather than the collection itself.
- In an attempt to be 'smart' I implemented an indexing function that would find items by name. A much better (and easier to read) implementation is a `GetByName()` method.

After removing the shadowing List, validating the wrapper code functions, and replacing the indexer with a proper Get function, the Collection would behave as expected and unit tests are now passing.

This is great because the code will get folded-in to a larger exploration that will get folded-in to the BF-BMX project (if it all works out).

```c#
// one way to find a simple List item by name while inheriting from ObservableCollection<T>
public class MyCollection : ObservableCollection<MyClass>
{
  public MyClass GetItemByName(string name)
  {
    foreach (var thing in this)
    {
      if (thing.name.Equals(name))
      {
        return thing;
      }
    }

    // A caller only know about an item that exists in this 
    // collection so an error here indicates a problem elsewhere  
    // in the application logic that would need to be dealt with.
    throw new KeyNotFoundException($"{name} not found in collection.");
  }
}
```

## Week 4

### ListView and MVVM

Implementing ListView with a Template in an MVVM environment is similar to what is described below, except for where in the component tree the data becomes available, and how bindings much be changed to accommodate that change:

- Template XAML does _not_ include an x:Name = "this" definition.
- `BindableProperty` properties are configured in the Template code-behind like before.
- The View code-behind does not include any reference to the incoming data (that will be up to the ViewModel now).
- The MVVM View class still needs XAML references to the binding source and template. So, in the View XAML a custom namespace ('xmlns') kvp is set to point to the ViewModels and associates an `x:TypeArguments` with the actual ViewModel class that contains the ObservableCollection. A `Class` namespace also points to the ViewModel. Another namespace points to the Templates directory, and in a local `ResourceDictionary`, an `x:Key` reference points to the Template file based on the template reference set in the xmlns declaration. See example XAML below.
- Unfortunately, it seems like the ViewCell in the View's XAML needs to have direct mappings to each Property that should be displayed. It's not clear to me why this is, but without these mappings, no data is displayed at all. See code below for an example of how this looks in the `<ListView.ItemTemplate>` element.

```xml
<!-- ForecastView.xaml code for MVVM environment, utilizing a ListView with a View Template -->
<?xml version="1.0" encoding="utf-8" ?>
<views:BaseView ...
                x:Class="MobWxUI.Views.MyView"
                xmlns:views="clr-namespace:MyProject.Views"
                xmlns:vm="clr-namespace:MyProject.ViewModels"
                x:TypeArguments="vm:MyViewModel"
                xmlns:controls="clr-namespace:MyProject.Templates">
    
    <views:BaseView.Resources>
        <ResourceDictionary>
            <controls:CustomCard x:Key="controls:CustomCard" />
        </ResourceDictionary>
    </views:BaseView.Resources>

    <ListView ItemsSource="{Binding MyCollection}">
        <ListView.ItemTemplate>
            <DataTemplate>
                <ViewCell>
                    <controls:CustomCard Name="{Binding Name}"
                                         Description="{Binding Description}" >
                    </controls:CustomCard>
                </ViewCell>
            </DataTemplate>
        </ListView.ItemTemplate>
    </ListView>
</views:BaseView>
```

_Note_: In my MVVM project, View and ViewModel inherit from abstract partial classes prefixed "Base". The BaseViewModel inherits from ObservableObject, and the BaseView partial class consumes a ViewModel type in the CTOR, and sets the `BindingContext` to the ViewModel parameter. This reduces duplicated code in every ViewModel class that is created, but makes it more difficult to realize a `BindingContext` does exist in each View.

The next step is styling the ListView items. Because the Bindings are now configured, _theoretically_ all that is needed is to add `BindableProperties` for each Style element and then a binding reference to `Resources\Styles`. First attempt to configure this showed that the default binding is to the Model class (where the data comes from), so there is more investigation needed to solve this part.

### MAUI ListView Control

I've been trying to understand how to leverage composition (loosely speaking) in .NET MAUI 8 to display a list of object instances within a scrollable page. In other frameworks I've been able to get this to do the work for me, including:

- React
- Spring Framework

The high-level problem is the same, and the solution includes composing bits of UI and data to get an iterated output, which improves code reuse and limits boilerplate boringness.

Here is the high level steps to get ListView to display properly in a Content Page view:

1. Define a data model. Ensure it has public properties with `get` accessors.
2. Define a "View Template" (a `ContentView`, _not_ `ContentPage`) that contains a Frame that binds the data model properties to Labels and other standard controls, common to each data model instance properties. Store this template in a separate folder such as "ViewTemplates".
3. In the View Template code-behind (also a `ContentView` class), create public, static, readonly `BindableProperty` properties - one for each data model property. Avoid naming conflicts.
4. Create a content page e.g. `PageView.xaml` and ensure it has `<ContentPage.Resources>` referencing the View Template (in this case "CardView") that will actually display the data, and also defines an `x:Class` that points to itself (I assume this is to ensure a reference to the collection and binding context that will be set in the next 2 steps).
5. In the content page code-behind, define a collection that is an ObservableCollection (or inherits from it or implements an Observable interface). Ensure it is a public property with at least a `get` accessor.
6. Also in the content page code-behind, set `BindingContext` to `this`.

Code samples to follow:

```c#
// DATA MODEL with get accessors
  public class Language
  {
  private string _title = string.Empty;

  public string Title
  {
    get { return _title; }
    set { _title = value; }
  }

  // ...more properties...

  // add customized colors or other styles if you really want to:
  private string _cardColor = "Azure";
  public string CardColor
  {
    get { return _cardColor; }
    set { _cardColor = value; }
  }
}
```

```xml
<!-- The "View Template" named "CardView" in this project -->
<?xml version="1.0" encoding="utf-8" ?>
<ContentView ...
             x:Class="MyProject.ViewTemplates.CardView"
             x:Name="this">
    <Frame BackgroundColor="{Binding CardColor}"
           BorderColor="{Binding BorderColor}">
        <Grid RowDefinitions="Auto,Auto,Auto"
              ColumnDefinitions="*">
            <Frame BorderColor="{Binding BorderColor}"
                   Grid.Row="0">
                <Label Text="{Binding Title}"/>
            </Frame>
            <Label Text="{Binding Name}"
                   Grid.Row="1"/>
            <BoxView BackgroundColor="{Binding BorderColor}"
                     Grid.Row="2"/>
            <Label Text="{Binding Description}"
                   Grid.Row="3"/>
        </Grid>
    </Frame>
</ContentView>
```

```c#
// View Template Code-Behind
public static readonly BindableProperty TitleProperty =
    BindableProperty.Create(nameof(Title),
        typeof(string),
        typeof(CardView),
        string.Empty);

public string Title
{
    get => (string)GetValue(CardView.TitleProperty);
    set => SetValue(CardView.TitleProperty, value);
}

// ... more BindableProperty properties here ...

public static readonly BindableProperty CardColorProperty =
    BindableProperty.Create(nameof(CardColor),
        typeof(string),
        typeof(CardView),
        string.Empty);
public string CardColor
{
    get => (string)GetValue(CardView.CardColorProperty);
    set => SetValue(CardView.CardColorProperty, value);
}
// CTOR
public ViewTemplate()
{
  InitializeComponent();
}
```

```xml
<!-- Content Page "PageView.xaml" -->
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage ...
             x:Class="MyProject.Views.MyContentPage"
             xmlns:controls="clr-namespace:MyProject.ViewTemplates"
             xmlns:views="clr-namespace:MyProject.Views"
             Title="MyContentPage">
    <ContentPage.Resources>
        <controls:CardView x:Key="controls:CardView" />
    </ContentPage.Resources>
    <ListView ItemsSource="{Binding Languages}">
        <ListView.ItemTemplate>
            <DataTemplate>
                <ViewCell>
                    <controls:CardView />
                </ViewCell>
            </DataTemplate>
        </ListView.ItemTemplate>
    </ListView>
</ContentPage>
```

```c#
// "View Template" code-behind
private ObservableCollection<Language> _languages = [];

public ObservableCollection<Language> Languages
{
  get { return _languages; }
  set {  _languages = value; }
}

public MyContentPage()
{
  InitializeComponent();
  // this could be a REST/JSON result object or database query result, etc
  // so long as it is an ObservableCollection<T>
  Languages = new ObservableCollection<Language>(
  [
    new Language { Name = "C#", Title = "C Sharp", Description = "The primary programming language that is used to develop apps for the Microsoft platform." },
    new Language { Name = "F#", Title = "F Sharp", Description = "Declarative-function, object-oriented, language for .NET apps." },
      // more entries...
  ]);
  this.BindingContext = this;
}
```

Some key ListView takeaways:

- Enables customization of the appearance of list items displayed on screen.
- Each item _automatically_ has its `BindingContext` set to the corresponding item in the data source, therefore only the _properties_ of the item need specific bindings.

### ListView Versus Content View

It seems that ListView is less-desireable to CollectionView. Performance and customizability were cited in the MAUI documentation as the reasons. I've moved the Forecast page of the Weather app over to CollectionView and it works _great_ in Windows and in Android _debug_ builds. Release builds are a problem though - the data did not show without jumping through a few hoops:

1. Clear all Release and Debug builds.
2. Remove x:DataType in the template xaml file (it was pointing to itself).
3. Add a ResourceDictionary element with the relative path to `Styles.xaml`, so it would be considered in the merged resources algorithm, and Style IDs could be found.

Now the Forecast page shows data in Android Release builds, including on a physical device!

Some references:

- [stackoverflow question "CollectionView working in debug but not in release in .NET MAUI"](https://stackoverflow.com/questions/75283345/collectionview-working-in-debug-but-not-in-release-in-net-maui).
- A related [MAUI Issue (Bug Report) in dotnet maui GitHub](https://github.com/dotnet/maui/issues/20002) that describes the problem and a potential work-around.
- [Babenlebricolo's DotnetMaui-DataTemplateBug repository](https://github.com/bebenlebricolo/DotnetMaui-DataTemplateBug/tree/main) has code demonstrating the 'broken' and 'fixed' states.

_Note_: The display problem was the same in my environment, but I believe the _cause was different_: In my case, the compiler was probably expecting Styles.xaml to exist alongside the Template xaml, or in the View xaml.

### MAUI Label, Span, and Style

There was a period where the Android Release version of MobWxApp wouldn't display the 7-day forecast data, and it wasn't apparent what the cause was. Also, since I assumed that a Release Build and Debug Build would be _similar enough_, testing in Debug mode would be enough. I was wrong, and here is what was going on:

- Forecast view utilizes a ContentView with various Layouts in a templated page, organizing data from a Collection for organized display.
- Within each data instance, I wanted to display a Key-Value text output like "Temperature 50 degrees and rising" all within a single Label or other string viewing element.
- The concatenated text would be styled per the Dark/Light Theme selected by the user, and would also follow the color palette selected for the app.
- Following .NET MAUI documentation, I applied `Label` elements with the `Label.ForemattedText` attached property, formatting the string text and bound string data within `Span` elements nested in a `FormattedString` element.
- During Debug build (and run) there were no warnings or errors in the Output tool regarding issues with XAML.
- During Release build there _were warnings_ indicating the problem: Label elements do not support a child Span elements.
- Removing the Span elements is an option and instead a custom ToString method could be developed (or edited) to force the output to match the requirements of the UI. _But this is not a good practice_ as the data layer should manage and process the data. _The UI Layer should manage the user interface_, which meant declaratively defining how the output should look.
- Removing the `Style` attributes that were bound to Styles.xaml seemed to clear up the problem and both Debug and Release builds no longer had the errors and the Forecasts view would work again.

So, what is the problem here?

- Are `Span` elements indeed _not supported_ within `Label`elements?
- Or is there an issue with my bindings to `Styles.xaml`?
- In either case, why does the program render and run in Debug, and only fail in Release builds?
- Also, why are other styles rendered properly within the `CollectionView`?

Debug mode compiles differently than Release mode (obvious, right?). Release build doesn't provide all the feedback that Debug mode does, most notably Breakpoints and Debug log output. Therefore, when developing XAML layouts, content handling, and style application, use Debug build for quick testing, then before moving on, do the following:

1) Perform a Release build.
2) Watch Debug view in Visual Studio's Output tool during build, it might show errors or warnings that could be clues to possible problems.
3) Test every control, page, etc to confirm they behave as expected.

The solution to the problem of syling `Span` elements within a parent `Label` is to:

1) Apply styles per usual to the `Span` itself, whether through in-line Style, or through Binding.
2) Ensure that `Span` supported properties are applied (and _not_ Label properties).

So for example instead of:

```xaml
<!-- Template View, within a Layout, with ResourceDictionary pointing to Styles.xaml -->
<Label LineBreakMode="NoWrap" Style="{Binding LabelStyle}">
    <Label.FormattedText>
        <FormattedString>
            <Span Text="Hello "
                  Style="{StaticResource LabelStyle}" />
            <Span Text="{Binding World}"
                  Style="{StaticResource LabelStyle}"
                  />
        </FormattedString>
    </Label.FormattedText>
</Label>

<!-- Styles.xaml showing only the SPAN and LABEL element Style definitions -->
<Style TargetType="Label" x:Key="LabelStyle">
  <Setter Property="VisualStateManager.VisualStateGroups">
    <!-- defined visual state groups that SPAN does not support -->
  </Setter>
</Style>
```

...add a Span-specific styling and avoid relying on Label Styling, like this:

```xaml
<!-- Template View, within a Layout, with ResourceDictionary pointing to Styles.xaml -->
<Label LineBreakMode="NoWrap">
    <Label.FormattedText>
        <FormattedString>
            <Span Text="Hello "
                  Style="{StaticResource SpanForecastItem}" />
            <Span Text="{Binding World}"
                  Style="{StaticResource SpanForecastItem}"
                  />
        </FormattedString>
    </Label.FormattedText>
</Label>

<!-- Styles.xaml showing only the SPAN and LABEL element Style definitions -->
<Style TargetType="Label">
  <Setter Property="VisualStateManager.VisualStateGroups">
    <!-- defined visual state groups that SPAN does not support -->
  </Setter>
</Style>
<Style TargetType="Span" x:Key="SpanStyle">
  <Setter Property="FontSize" Value="14" />
  <!-- more SPAN specific setters here -->
</Style>
```

Elements `Span` and `Label` do not share Styling properties, despite there being _some overlap_, so explicit bindings are required even through Debug Build will ignore the error, but Release Build and an actual Android platform deployment might not.

That completes the Forecast page style fix-up for the app. Next steps include:

- Implementing unit tests (I've gone way too long without them).
- Updating and cleaning up the response models.
- Implementing SQLite to cache responses.

## Week 3

Watched a MSFT Reactor presentation today on continous integration (CI) with LLMs and AI Models. There were two guests with the host, and one of them mentioned Vector Databases and briefly described it.

Here are my [notes about vector database](./msft-semantickernel-vectordb.html) and MSFT's Semantic Kernel.

Also see [About Machine Learning](./about-machine-learning.html) for somewhat related notes from a previous MSFT Reactor session.

### Git Console Commands and Flow

- Use a git-aware command line interface profile. I'm using [posh-git](https://github.com/dahlbyk/posh-git).
- `git init`: Start up a new git-tracked folder. Some framework initializers do this for you, others do not.
- `git status`: Posh-git has the ability to show status in-line with the prompt, but it lacks details like _which_ files have been added, modified, or deleted.
- `git log`: Answers the question "where am I in the commit history?" by reviewing (in reverse-time order) commits with their comments. Good git comments will help tell a story about the state of the code.
- `git diff {filename}`: Shows the added or removed code difference between the previous commit and the currently saved (and uncommitted) changes. Answers the question "why is _that_ file in the modified list?
- `git commit {filename} {comment}`: Can also use `.` in place of `{filename}` to include all new/modified/deleted files in stage or unstaged states. Comment size is not strictly limited but I stick with fewer than 50 characters so that the commit message is not cut-off in a code history window like GitHub's 'code' view. Use a line-feed (LF) or carriage return (CR) and LF to add comments beyond a 50 character 'title'.
- `git push {target} {branch}`: Pushing commits to a remote, or another branch. This is really a `git merge` command with the modification of a remote branch as the target, rather than the current (and local) branch.
- `git pull {target} {branch}`: Takes commits from named target's named branch (if it exists) and attempts to 'git merge' them to the current branch. This is the opposite of `git push` and is also based on `git merge` so use it accordingly. On occasion it can be helpful to merge from one branch to another, say for example to incorporate a remote development branch into a local development branch.

Other Git commands I rarely use:

- `git stage {filename}`: De-staging files is simpler and less risky than undoing a commit. Use stage to prepare to commit, then execute the project or solution and verify it works (tests pass, etc), before committing the staged files.
- `git rebase {branchname}`: Every branch has a 'base commit' that is the beginning of that branch history. Aside from the 'main' branch, every other branch will have a 'base commit' that most likely is _not_ the first commit that initialized the git repository. When working on a team, it can be helpful to rebase your own branch to a commit that is the latest commit on a working or main branch (or some other dev branch). This ensures the current branch has existing committed and approved necessary changes in it, which can help reduce pull-request merge conflicts. One downside is it alters the history of the current branch so it appears to derive from some later commit than it did originally. Some teams/organizations do not allow rebasing.
- `git merge {otherbranch}`: Takes commits from 'otherbranch' and attempts to merge them into the current branch. There are options here that effect how the merge is performed (fast-forward, squash, rebase, etc) that should be reviewed before using. This is useful when working in a local development branch and changes from another development branch are needed in the local branch. It can get confusing very fast when merging branches like this, and the git history (see 'git log') can also be harder to follow. Merging to a remote branch is also possible, and in fact `git push {target} {branchname}` is a merge operation for all intents and purposes.
- `git merge {namedcommit}`: Same as `git merge {otherbranch}` but specifies a commit name rather than a branch-name label. Be sure to review the git-merge help files for additional information.

_Note_: The posh-git repository is somewhat stale (2-years since last update/fix/response). This could mean it could fall out of compliance with newer PowerShell releases (currently I'm using 7.4.1).

Also note: After installing git (I usually select GIT-SCM latest), access the help files in the installation directory `./share/doc/git-doc/`, or by typing `git help` for an overview of commands, and `git help {topic}` for a rich (html) manual.

### MobWX Navigation Bug Fixups

I completed sorting out the issues with navigation in the mobile weather app. Also, the NWS managed to fix their 'Points Forecast' endpoint, but it has not been reliable, so occasionally there are REST results codes 404 and 5xx that my app will need to be better an handling.

- Took to Miro to redesign the startup process and navigating the app so it wouldn't get "stuck" on a page due to the navigation itself, or a processing error of some kind.
- Implemented more asynchronous Command instances to handle button pushes.
- Added a status notification for issues like when a forecast cannot be fetched right now, or a bod lat/lon entry was made and the forecast won't be returned.

There is more work to do, but the build is functional, publishing an APK works, and running on Windows and Android (both emulated and side-loaded) function without errors now.

The current version with navigation bug fixes is merged into main now and an updated side-loadable APK has been published privately.

### About Using Public APIs

As I have worked through using the NWS public API over the last two months, I've been learning how to better deal with user inputs, and less-expected (or unexpected) API responses.

An few takeaways:

1. Always look at the API documentation for updates about its operating state, especially known issues. The API publisher might have succinct conditional information that can be transformed into code to work around a problem. The publisher might also include information like "just try again and it should work". This research will reduce frustration trying to solve non-code problems by editing/refactoring code.
2. API Key protection is difficult within a distributable app. At Code Fellows training they pushed the idea of relying on a custom API server to basically relay/proxy requests to actual APIs (and perhaps cache them). At the time I thought this was a convenient way to enforce learning how to build client-server architecture (probably still true), however a more important takeaway is: It is much simpler (and obvious how) to hide secrets like API Keys at the server level than it is to do it within a client itself. I'm sure there are simpler ways to hide secrets within an app, but I haven't gone deep into that rabbit hole yet.
3. Leveraging a custom API proxy server allows separating the vagaries of API web-request-response-cycle (WRRC) transactions from the client app, so the client can concentrate on user experience (UX), while the server-side deals with data processing, handling errors, managing partial or incomplete API-call-chain responses, etc. This will also make the client-side code smaller.
4. When relying on environment variables, always check that a value is actually returned _and_ that the value isn't an empty string. Do this very early in the code so that no successful API calls are wasted when an invalid API call (lacking an environment variable) exits a multi-call chain of events. In other words: Identify and handle failure points as early as possible.

## Week 1

### MAUI Color and Theming

Working through implementing a usable About page for MobWxApp:

- Implementing a "Hyperlink" Style for things like opening the GitHub Project or LinkedIn Profile in a browser is fairly straightforword so long as you _do not_ use `<span>`s.
- The problem implementation is documented at [.NET MAUI UI Controls: Label - Create a Hyperlink](https://learn.microsoft.com/en-us/dotnet/maui/user-interface/controls/label?view=net-maui-8.0#create-a-hyperlink), however it does not work as described.
- MAUI Project GitHub [Issue 14410](https://github.com/dotnet/maui/pull/14410) for an overview of the issue. There are similar issues linked, and the bug-fix schedule seems to get pushed-back quite often.
- The core of the problem seems to be use of `<span>` elements, and can be worked around by using `<Label>` instead. Below is an example of the problem XAML and the work-around XAML.
- A secondary issue is the use of the `Launcher` class, instead of an IBrowser implementation (see C# code, below).

```xml
<!-- from .NET MAUI 8 documentation at learn.microsoft.com -->
<Label>
    <Label.FormattedText>
        <FormattedString>
            <Span Text="Alternatively, click " />
            <Span Text="here"
                  TextColor="Blue"
                  TextDecorations="Underline">
                <Span.GestureRecognizers>
                    <TapGestureRecognizer Command="{Binding TapCommand}"
                                          CommandParameter="https://learn.microsoft.com/dotnet/maui/" />
                </Span.GestureRecognizers>
            </Span>
            <Span Text=" to view .NET MAUI documentation." />
        </FormattedString>
    </Label.FormattedText>
</Label>
```

```xaml
<!-- Avoid using SPAN elements -->
<Label Text=".NET MAUI Project Documentation"
       TextColor="DarkBlue"
       TextDecorations="Underline"
       VerticalAlignment="Center"
       >
  <Label.GestureRecognizers>
    <TapGestureRecognizer Command="{Binding TapCommand}"
                          CommandParameter="https://learn.microsoft.com/dotnet/maui/" />
  </Label.GestureRecognizers>
</Label>
```

The problematic C# Code uses `Launcher.OpenAsync(uri)` to navigate to a page:

```c#
using System.Windows.Input;
public partial class MainPage : ContentPage
{
    // Launcher.OpenAsync is provided by Essentials.
    public ICommand TapCommand => new Command<string>(async (url) => await Launcher.OpenAsync(url));
    public MainPage()
    {
        InitializeComponent();
        BindingContext = this;
    }
}
```

...what is really necessary for an external hyperlink is a Browser method to call the uri using the 'System Preferred' web browser:

```c#
// note: this could be done using ICommand but my implementation uses 
// the MVVM CommunityToolkit so I went with IAsyncRelayCommand instead
public partial class Mainpage : ContentPage
{
  public IAsyncRelayCommand<string> TapCommand => 
    new AsyncRelayCommand<string>(
        async (url) => await BrowserOpen(url)
        );
}
...
private async Task BrowserOpen(string url) {
  // check for null/whitespace string and open a try-catch block, then:
  try 
  {
    Uri uri = new Uri(url);
    bool result = await Browser.Default.OpenAsync(uri, BrowserLaunchMode.SystemPreferred);
  }
  catch (Exception ex)
  {
    // handle, notify, etc
  }
}
```

Theming In Particular:

- It seems like a good idea to leverage `AppThemeBinding`s everywhere once it is used somewhere on a View, otherwise there can be some unexpected results.
- Use `transparent` color type when necessary to allow the Theme application to a parent View/Control to show through.

Link-Like Label Styling:

The code I implemented for launching the browser and displaying a "link"-like Label are functional on Windows and Android (emulator API 32+).

_Note:_ [`IBrowser.OpenAsync()` documentation](https://learn.microsoft.com/en-us/dotnet/api/microsoft.maui.applicationmodel.ibrowser?view=net-maui-8.0) does not mention any Exception type that might get thrown.

Custom Images and Icons:

Miro is really helpful creating materials for images and icons. Some things to keep in mind when creating materials for .NET MAUI 8:

- Seems like FlyoutIcon must be black-and-white, or a Font or other Glyph.
- Sizing images for their intended use makes for less troubleshooting when adding and troubleshooting issues rendering images.
- Creating a DataTemplate to enable color-image rendering as an icon is a possibility, however `Shell.FlyoutIcon` doesn't seem to accept a `FlyoutItem` as an acceptable input.
- Images _must_ be named starting with a letter character, all characters lower-case, and numbers are acceptable _except_ for the 1st character in the filename.
- So long as Images are placed into the Resource hierarchy at `Project\Resources\Images\`, they will automatically be assiged the Build property `MauiImage`.
- When adding/removing images from a MAUI project it is a good idea to check the Project file for `<ItemGroup>` entries with both `include` and `remove` attributes. Clean-up the entries with `remove` attribute before the next build-deploy cycle to avoid some possible deployment errors.

### Publishing a Private Android APK using Visual Studio

So many times I've done this and yet the process is just un-obvious enough that I stumble through it pretty much everytime. The goal here is to document it so that I no longer need to look it up. :smiley:

1. Build the MAUI App using `Rebuild` on the Solution.
2. Select the Android emulator and run the app, confirming there are no errors then close the app.
3. Select the target emulator for Android in the Debug configuration.
4. Select `Release` in the Solution Configuration.
5. Select `Publish` on the Project to deploy. If there is already a Publish Configuration, a build cycle will execute, otherwise the configuration must be set first.
6. When the Archive Manager is done creating and packaging the APK, look at the bottom of the screen for `Distribute...` and click it to open the 'Distribute - Select Channel' window.
7. Click `Ad Hoc`.
8. Add a Signing Authority (have a secure password ready), or select an existing one.
9. Click `Save As` to save the APK. _Note_: If there is already in an APK in that folder _be certain to overwrite it_ otherwise the new deployment will not complete successfully.
10. Confirm `Overwrite file?` and then enter the secure password.
11. When that process completes, review the screen for any errors or problems.
12. If there were no problems, click `Open Distribution` at the bottom of the Archive Manager window to gain access to an APK file that can be side-loaded onto an appropriate Android API Level phone.

Note: Select `Open Folder` to see the signed-apks folder, archive.xml, and deployable APK file.

### Week 1 JavaScript Fun

Areas where I've been struggling with JavaScript recently: Arrow Functions!

- Creating a Function as if it were a class with its own members.
- When to use Arrow functions, anonymous functions, etc inside of a Class or Function-style class.

```javascript
// Functional "class"
const MyThing = function() {
  this.kvpStore = {};
  this.has = (key) => {
    return this.kvpStore.hasOwnProperty(key);
  };
}
```

I need to sort this out in my head so it is less frustrating next time:

- [ ] Why are we using `this.has = (param) => {}` here, instead of `this.has = function(param) {}`? The problem is they don't have their own meaning of `this`, resulting in unexpected results. So method definitions should _not_ use this syntax. Normal methods should be written using class 'method' syntax (see below). _[MDN JavaScript Reference]_

```javascript
// anonymous function
(function (num) {
  return num / 100; 
});

// basic arrow function removes keyword 'function' and parens and braces not necessary for one-line code block and single (simple) params
num => num / 100;

// braces and 'return' keyword required for multi-line code blocks
num => {
  const temp = num / 100;
  return temp + 100;
};
```

- Do _not_ return expression body syntax e.g. `const func = () => { foo: 'baz' };`
- Instead, wrap object literal in parenthesis: `const func = () => ({ foo: 'baz' });`
- Don't do this either `const func = () => { foo: function () {...} };`
- Don't return a function like this either: `const func = () => { foo() {...} };`
- There is no concept of `arguments` binding in arrow functions.
- Arrow functions lack a `prototype` property, and will throw an error when called with the `new` keyword.

Note: The above examples are slightly modified versions from _[MDN Javascript Reference]_, accessed 5-Jan-24.

```javascript
// class method syntax example with public function definitions
const obj = {
  foo() {
    return 'bar';
  },
};

// the slightly longer form of the above:
const obj = {
  foo: function () {
    return 'bar';
  },
};
```

- MDN Reference Material about [Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions).
- MDN Reference Material about [Class Method Definitions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Method_definitions).

JavaScript Delete Operator

This is an odd one! Delete operator allows removing a property from an Object. Identify the object and property to perform the removal.

```JavaScript
var HashTable = function() {
  this.collection = {}; // a key-value pair storage i.e. [hashcode, value]
  this.remove = (key) => {
    delete this.collection[key];
  }
  // add, has, and other functions...
}
```

## Footer

Return to [Root README](../README.html)
