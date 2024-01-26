# Nojronablog 2024

A space for collecting thoughts and technical walk-thrus and takeaways during my coding journey through CY 2024.

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
