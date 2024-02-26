# WPF MVVM Learnings

A collection of notes related to developing and building upon MVVM in DotNET WPF.

## Table of Contents

- [Community Toolkit - MVVM Toolkit](#community-toolkit---mvvm-toolkit)
- [Community Toolkit - Concerns and Possible Gotchas](#community-toolkit---concerns-and-possible-gotchas)
- [Community Toolkit - Observables](#community-toolkit---observables)
- [Community Toolkit - ObservableProperty Attribute](#community-toolkit---observableproperty-attribute)
- [Community Toolkit - RelayCommand Attribute](#community-toolkit---relaycommand-attribute)
- [Community Toolkit - INotifyPropertyChanged](#community-toolkit---inotifypropertychanged)
- [Community Toolkit - ObservableObject](#community-toolkit---observableobject)
- [Community Toolkit - ObservableRecipient](#community-toolkit---observablerecipient)
- [Community Toolkit - Inversion of Control](#community-toolkit---inversion-of-control)
- [Caliburn Micro - Requirements](#caliburn-micro---requirements)
- [Caliburn Micro - WPF with MVVM Project Setup](#caliburn-micro---wpf-with-mvvm-project-setup)
- [Caliburn.Micro - Uses Naming Conventions](#caliburnmicro---uses-naming-conventions)
- [WPF Input Validation](#wpf-input-validation)
- [Random Notes](#random-notes)
- [Resources](#resources)
- [Footer](#footer)

## WPF Reference Notes

### WPF Bindings Overview

- `TargetProperty` must be a dependency property.
- Most dependency properties can use data Binding unless they are read-only.
- Any object that inherits from DependencyObject can define dependency properties.
- UI Element properties are dependency properties by default in WPF.
- Binding Source is usually a .NET Custom object.
- UIElements, List objects, ADO.NET or Web Services objects, and XmlNodes that contain data can be a `BindingSource`.

Data flows from target properties to binding source objects by default:

- OneWay: Target property :arrow_right: binding source.
- TwoWay: Data can flow in both directions (requires extra overhead under the hood so use wisely).
- OneTime: Only the initial value is propagated from source to target. No other changes are propagated.
- OneWayToSource: Target property :arrow_left: binding source.

MSFT documentation on [WPF Data Bindings in .NET 8](https://learn.microsoft.com/en-us/dotnet/desktop/wpf/data/?view=netdesktop-8.0).

## Community Toolkit - MVVM Toolkit

Adds lots of common Types that support:

- Observables.
- Dependency Injection.
- Relay Commands.
- Asynchronous operations/commands.
- Messaging.

See [MVVM Toolkit Introduction](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/mvvm/) for the detailed list of Types.

Adds Roslyn source generators to reduce boilerplate coding.

- Observable property setup reduced to just adding the Attribute `[ObservableProperty]` to Fields. The Property with `SetProperty(ref name, value)` is generated during build.
- Creating new Commands is reduced to an Attribute on a private void method - no `ICommand` type Field and associated `ICommand` type Property needed to initiate `new RelayCommand(DoCommandMethod)`.

MVVM Toolkit is a collection of tools and types:

- No need to migrate an entire existing app to it.
- Can piecemeal features into a new or existing app (ex: Use the Roslyn generators and no other Types or features).

## Community Toolkit - Concerns and Possible Gotchas

How well supported and active is the core project? Seems to be fairly active with recent Issues resolved, and several PRs waiting and recently closed. One hitch is the [CommunityToolkit Samples Repo](https://github.com/CommunityToolkit/MVVM-Samples) is relatively complex and does a poor job supporting comprehension of the Toolkit syntax and capabilities. My humble opinion.

Does the MVVM Toolkit have a lifecycle timeline published? The [CommunityToolkit dotnet repo](https://github.com/CommunityToolkit/dotnet) points to a [Milestones](https://github.com/CommunityToolkit/dotnet/milestones) section of the repo, and it is _empty_. The [CommunityToolkit Documentation](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/introduction) does _not_ provide any additional Milestone or Lifecycle information at all.

The _two things_ that it has going for it:

1. MSFT has dedicated money and employees to the toolkit.
2. The DotNET Foundation supports the toolkit (among many others).

## Community Toolkit - Observables

- Add `[ObservableProperty]` to a Field.
- Field can be private (recommended) or public.
- Generated code will assume Field is 'lowerCamel', '_lowerCamel', or 'm_lowerCamel' cased.
- Generated code will create 'UpperCamel' cased Property and methods.
- Generated code adds `partial void` methods using Field name, like `OnNameChanging(string?)` and `OnNameChanged(string?)`.
- OnChanging and OnChanged methods are overloaded with `string? oldValue, string? newValue` versions.
- Generated code methods _can be called by my code_!
- Partial Methods without a user-coded implementation will be removed at compile time.

## Community Toolkit - ObservableProperty Attribute

The `[ObservableProperty]` attribute can be applied to _partial class_ fields:

- A simple value type or object such as int or string.
- A custom .NET object like Person or Location.
- An `ObservableCollection<T>` where T could be any Type.
- Complex, nested types in an Observable Collection. Additional implementation will need to be coded to get Notifications to function.

There is a [StackOverflow question about NotifyPropertyChanged not working on Observable Object](https://stackoverflow.com/questions/76405547/notifypropertychangedfor-not-working-on-observableobject).

- `[NotifyPropertyChangedFor()]` attribute applies to the container of the complex (nested) object.
- Raising `PropertyChanged` events for the nested object properties will be required.
- Example code below, lifted from _[StackOverflow]_.

```c#
private readonly IMyNestedIocService _myService;

public MyViewModel(IMyNestedIocService myService)
{
  _myService = myService;
  _myService.PropertyChanged += (s,e) =>
  {
    OnPropertyChanged(nameof(TargetPropertyToNotify));
  }
}
```

### Basic Notification

Raise a notification whena property changes by using `NotifyPropertyChangedFor` attribute.

Example code from _[MSFT MVVM Toolkit Official Documentation]_:

```c#
[ObservableProperty]
[NotifyPropertyChangedFor(nameof(FullName))]
private string? name;
```

### Evaluate Command CanExecute

To re-compute whether a Command `Enabled` state should be changed when a property is changed, leverage `[NotifyCanExecuteChangedFor(nameof(MyCommand))]` as an attribute above the depended Field.

- This generates code that sets `CanExecute` type methods to set them true/false depending on the Field state every time it changes.
- Command _must_ be an `IRelayCommand` property.

_Warning_: Adding custom attributes on a field will require using a traditional manual property (i.e. You write the code yourself). This is true of fields that have custom validation, rather than relying on `ValidationAttribute` alone.

### Requesting Property Validation

Use the following attributes on the Field:

- `[ObservableProperty]`
- `[NotifyDataErrorInfo]`
- Optionally `[Required]`
- Include any Validation Attributes such as e.g. `[MinLength()]`

This results in:

- A full property that includes `ValidateProperty(value, "Value2");` in the getter.
- Updates the state of the `ObservableValidator` object.

*Note*: Adding more cuatom attributes will *not* apply them to the generated property. Write the code yourself to work around this limitation.

### Sending Notification Messages

Properties whose Type inherits/implements `ObservableRecipient` can use `[NotifyPropertyChangedRecipients]` attribute.

- Instructs generator to insert `PropertyChanged()` message notifications.
- _All_ registered recipients consume the change notification to process it.
- Relies on `IMessenger` instance at the current ViewModel.

Decorate the Field with `[ObservableProperty]` and `[NotifyPropertyChangedRecipients]` attributes:

- Enables sending Notification Messages through `IMessenger`.
- Generated code will include `Broadcast(oldValue, value)` in the Property setter.

### Adding Custom Attributes

Use:

- `[property: ]` target over annotated fields.
- Custom Attribute(s) get forwarded to the generated properties.

## Community Toolkit - RelayCommand Attribute

Eliminates relay command property boilerplate for annotated methods.

- _partial class_ required to declare annotated methods, and any others in nested Types where these annotations are used.
- Annotate a method in a partial type with `[RelayCommand]`
- Generated code method name will be based on the annotated Field name, with a 'Command' suffix, and without the 'On' prefix.
- Generated async methods will _also lack_ the 'Async' part in the generated code.

Parameters can be included, and will convert the generated Command code into the generic `IRelayCommand<T>` version.

Async commands are wrapped in `IAsyncRelayCommand` or `IAsyncRelayCommand<T>` when defined with a `Task` return type.

- Remember to not use `void` as an async return type.

Enable `CanExecute` using the Relay Command attribute: `[RelayCommand(CanExecute = nameof(CanGreetUser))]`

Control the state of a Command by adding the following to the Field definition:

- `[ObservableProperty]`
- `[NotifyCanExecuteChangedFor(nameof(MyCustomCommand))]`

_Note_ about updating the visual state of a button:

- Command not auto-aware of return value changes from `CanExecute` method.
- Implement `IRelayCommand.NotifyCanExecuteChanged` to invalidate the command and signal `CanExecute` to re-evaluate.
- The UI Control must be updated from there.

### Handling Concurrency

Async command?

- Command can be configured to allow concurrency or not via the `AllowConcurrentExecuteions` property.
- `CancellationToken` is supported, however any previously pipelines command will run without being awaited (although I could be mis-understanding the documentation comment here).

Handling Async Exceptions:

- Use `[RelayCommand(FlowExceptionsToTaskScheduler = bool)]`
- Await and rethrow: Default configuration. Re-throws Exceptions using the same sync Context. This is likely to crash the App!
- Flow exceptions to the Task Scheduler: Re-thrown Exceptions are accessible via `IAsyncRelayCommand.ExecutionTask` and will bubble up to `TaskScheduler.UnobservedTaskException`. This is more complex to use but allows UI configuration to respond to Exceptions.

_Note_: When set to `true`, unrelated Exceptions might not be rethrown automatically!

Cancel Commands:

- Use `[RelayCommand(IncludeCancelCommand = bool)]`
- An `ICommand` wrapped async relay command.
- Signals state indicating whether the linked command is executable or not.
- These can be bound to the UI for allowing Users to cancel pending async operations.

Custom Attributes:

See [Custom Attributes](#adding-custom-attributes) subsection above - it applies here.

## Community Toolkit - INotifyPropertyChanged

Method to insert MVVM support code into existing types:

- Consider this a way to decorate code that enables a multiple-inheritance when target types are already implementing/inheriting from another type.
- Annotated types must be in a partial class, and if nested, all nested classes must also be marked partial.
- This enables code generation _into_ the existing code!
- Do _not_ use this unless the target type cannot inherit/implement from another existing Class.

How to do it, per _[Community Toolkit MVVM Documentation]_:

```c#
[INotifyPropertyChanged]
public partial class MyViewModel : InheritedType
{
  // the partial class-level attribute identifies it as
  // the recipient of the code that will be generated.
  // Other helpers will be included:
  // Implements:
  //   INotifyPropertyChanged
  //   ObservableObject
  //   ObservableRecipient
}
```

## Community Toolkit - ObservableObject

Features:

- Is a base class.
- Implement `INotifyPropertyChanged`
- Implement `INotifyPropertyChanging`
- Enables simplified support for change notifications.
- Provides `SetProperty` methods to set property values from types inheriting from ObservableObject.
- Automates raising appropriate events.
- Provides `SetPropertyAndNotifyOnCOmpletion` method that can set `Task` properties to support completion notification.
- Exposes `OnPropertyChanged` and `OnPropertyChanging`, which can be overridden to customize raising notification events.

Wrap a custom class with `ObservableObject`:

```c#
public class ObserableMyClass : ObservableObject
{
  private readonly Location location;
  public ObservableMyClass(Location location) => this.location = location;
  public string CityName
  {
    get => location.CityName;
    set => SetProperty(location.CityName, value, location, (l, c) => l.CityName = c);
  }
}
```

In the above example code, `ObservableMyClass.SetProperty` signature overload is `SetProperty<TModel, T>(T, T, TModel, Action<TModel, T>, string)`.

- `TModel`: Type argument of the model to be wrapped.
- `T`: Type of the property to be set. Infers TModel.
- `T oldValue`: Pass the current value of the wrapped object property.
- `T newValue`: New value to set to the property.
- `TModel model`: Target model that is being wrapped.
- `Action<TModel, T> callback`: Function to invoke if new value does not equal current one, which sets the new value if not equal to existing value. _Be sure to only use the input params_ for this and _not_ the wrapped object Fields (for performance reasons).

### Handling Task Properties

Always raise a notification event if a property is of a Task type.

- Bindings will be updated at the correct time.
- Task monitoring will be used to wait for completion before raising notifications.
- Task Property can be bound and automatically get the correct (completed) notification.

_Note_: This implementation is meant to replace `NotifyTaskCompletion<T>` from `Microsoft.Toolkit` package.

## Community Toolkit - ObservableRecipient

## Community Toolkit - Inversion of Control

Dependency Injection is a common solution to attaining IoC, but creating services that are injected into backend classes (as parameters to viewmodel constructors).

- APIs are not added to this toolkit for DI implementation.
- Use `Microsoft.Extensions.DependencyInjection` package instead.

### Microsoft Extensions Dependency Injection

- Fully featured.
- Utilizes `IServiceProvider` setup and use.

How to integrate this into Community Toolkit?

See [CommunityToolkit.Mvvm.DependencyInjection documentation](https://learn.microsoft.com/en-us/dotnet/api/communitytoolkit.mvvm.dependencyinjection.ioc?view=win-comm-toolkit-dotnet-7.0).

How To:

1. Install `Microsoft.Extensions.DependencyInjection`
2. Install `CommunityToolkit.Mvvm`
3. Create a helper class that will need to be shared between ViewModels.
4. Extract an interface for the helper class.
5. In App.xaml.cs: Implement a private static `IServiceProvider ConfigureServices()` method and implement a new `ServiceCollection()` instance. This is where services and ViewModels will get injected. Return the `ServiceCollection` instance.
6. In App.xaml.cs: Implement a public property `IServiceProvider Services` with a single getter.
7. In App.xaml.cs: Implement a static method `App Current()` method that returns an `Application.Current` cast as an `App`.
8. In App.xaml.cs: Create a CTOR that assigns `ConfigureServices()` to `Services` and calls `this.InitializeComponent`.
9. In each View CTOR that needs binding to its ViewModel: Add `this.DataContext = App.Current.Services.GetService<TViewModel>();` with the named ViewModel as the type.
10. In each ViewModel registered in `IServiceProvider` (probably as a Transient service): Add a private field for each service that the ViewModel will consume, and use `App.Current.Services.GetService<IServiceType>();` to inject it via the IoC. `IServiceType` is the interface name that the service implements.

## Caliburn Micro - Requirements

Visual Studio 2019 or newer.

DotNET Framework 4.7+

## Caliburn Micro - WPF with MVVM Project Setup

Reference: [WPF with MVVM Project Setup](https://www.youtube.com/watch?v=p-fmOJMLl0A&list=WL&index=2&ab_channel=IAmTimCorey) video by Tim Corey.

Install NuGet Package Caliburn.Micro (Tim used 3.2.0 but a newer version is currently available that might not support DotNET 4.7 Framework.

The UI Layer is broken-out into Models, ViewModels, and Views.

- Data Access should be in a different Project (a Class Library) or elsewhere in the Project tree.
- Models hold the data for the Views to display.
- ViewModels take the models and bind them to the View.

### Caliburn Micro - Setup Steps

1. Create a ViewModel
2. Create a View
3. Create a class called Bootstrapper that will inherit from BootstrapperBase (using Caliburn.Micro) (see code below)
4. Remove MainWindow.xaml (and its backing cs)
5. Update App.xaml and add a Merged ResourceDictionary that points to '<local:Bootstrapper x:Key="Bootstrapper" />' (see code below)

Bootstrapper.cs code:

```csharp
using Caliburn.Micro;
using System.Windows;
using MyDesktopApp.ViewModels;

namespace MyNamespace
{
    public class Bootstrapper : BootstrapperBase
    {
        public Bootstrapper()
        {
            Initialize();
        }

        protected override void OnStartup(object sender, StartupEventArgs e)
        {
            // tell Caliburn Micro to use ShellViewModel as the base view
            // similar to how XAML StartupUri tells WPF to use MainWindow.xaml
            // so be sure to remove StartupUri from App.xaml and add a new
            // ResourceDictionary
            DisplayRootViewFor<ShellViewModel>();
        }
    }
}
```

Add the following `<ResourceDictionary>` hive to `<Application.Resources>` in App.xaml:

```xml
<ResourceDictionary>
    <ResourceDictionary.MergedDictionaries>
        <ResourceDictionary>
            <local:Bootstrapper x:Key="Bootstrapper" />
        </ResourceDictionary>
    </ResourceDictionary.MergedDictionaries>
</ResourceDictionary>
```

## Caliburn.Micro - Uses Naming Conventions

- Binds ViewModel to View to launch the correct XAML
- By default: Models, Views, and ViewModels
- Can be changed but must be configured in Caliburn.Micro to support your custom naming conventions

### Caliburn Micro - Binding Values in ViewModel to a View

Caliburn.Micro:

1. Create a public Property in ViewModel for the data. Use a _full Property_ not just a backing Field or 'auto get-set' notation.
2. Add a Control in the View and give it an `x:Name` that matches the ViewModel's Property.

WPF OneWay Binding:

- Set the control value property (e.g. `Text` for a TextBlock) to `{Binding Path=OtherProp, Mode=OneWay}`
- `OtherProp` refers to the value to copy from.
- The Binding _name_ must match an existing property.
- OneWay means the Binding will accept a value but not change when the other property value changes.

### Caliburn Micro - NotifyOfPropertyChanged

- Automates updating properites.
- Once a Binding exists, use `NotifyOfPropertyChanged` in the ViewModel Property so edits to a OneWay Binding control also get updated.
- Use a lambda to _return the value of the property that needs the update_ in the bound View.

NotifyOfPropertyChanged code example:

```csharp
public string LastName {
  // field
  // prop getter
  set {
    _lastname = value;
    NotifyOfPropertyChange(() => LastName);
    NotifyOfPropertyChange(() => Fullname);
  }
}
```

### Caliburn Micro - Child Forms

Keyword `x:Name="ActiveItem"` enables parenting a child View for display.

Nest User Control (WPF) inside of a parent Window (WPF).

Caliburn.Micro 'Screen' is the simplest display model, but there are others:

- One child view at a time:
- Single child view with disposal:
- Multiple child views simultaneously:

ActivateItem():

- Create new Views to be presentation UI child forms.
- Create new ViewModels to bind data to child Views. These will inherit from `Screen`.
- Parent ViewModel will implement `Load___()` methods with `ActivateItem(new ChildnameViewModel());` to control child view instantiation.
- Add a `<Content Control x:Name="ActivateItem" />` to the parent View to placehold where a child View will appear.
- Tim added Buttons with `x:Name` attributes that call `LoadPageN` where N is a name that makes sense for the View that will get initialized.
- Use `ActivateItem()` in the `LoadPageN()` method(s) that instantiate a new instance of the child ViewModel that will drive the View.

```csharp
public namespace MyNamespace
{
  public class MyClass : Conductor<object>
  {
    // members...
    public void LoadPageOne()
    {
      ActivateItem(new FirstChildViewModel());
    }

    public void LoadPageTwo()
    {
      ActivateItem(new SecondChildViewModel());
    }
  }
}
```

```xml
<!-- Buttons trigger calls to LoadPageOne() and LoadPageTwo() methods in parent ViewModel -->
<Button x:Name="LoadPageOne" Grid.Row="5" Grid.Column="1">Load First Page</Button>
<Button x:Name="LoadPageTwo" Grid.Row="5" Grid.Column="2">Load Second Page</Button>
<!-- ContentControl calls ActivateItem -->
<ContentControl Grid.Row="6" Grid.Column="1" Grid.ColumnSpan="5" x:Name="ActiveItem" />
```

### Caliburn Micro - Binding Collections

Use `BindableCollection<T>` for multi-element controls like ComboBoxes.

```csharp
        private BindableCollection<PersonModel> _people = new BindableCollection<PersonModel>();
        public BindableCollection<PersonModel> People
        {
            get { return _people; }
            set { _people = value; }
        }
```

- Binding Mode `OneWayToSource` binds from the Control _to the Property_ in the ModelView.
- Binding a Property of an Object instance can be done using 'dot notation' _however use an UNDERSCORE instead of a dot_.

```xml
<!-- In the control, binding by x:Name -->
<TextBlock x:Name="SelectedPerson_LastName" />
```

### Caliburn Micro - Binding Events

Use the naming convention 'Can' + PropertyName. For example, to implement the ability to enable a button only under certain conditions on the state of a Property:

```csharp
public string FirstName
{
  get { return _firstName;}
  set {
    _firstName = value;
    NotifyOfPropertyChange(() => FirstName);
  }
}

public ClearText(string firstName)
{
  FirstName = string.Empty;
}

public bool CanClearText(string firstName)
{
  if (String.IsNullOrWhiteSpace(firstName))
  {
    return false;
  }
  return true;
}
```

## WPF Input Validation

I'll overview [Tosker's Corner](https://www.youtube.com/watch?v=5KF0GGObuAQ&ab_channel=ToskersCorner) demonstrations of using input validation in the next four subsections.

_Remember_: Updates to properties must include notifications, for example `IObservableCollection`, or `INotifyPropertyChanged`, etc implementations.

### WPF Input Validation By Exception

Throw an Exception type when the property value does not meet specific requirements.

It appears this is a handy way to deal with input validation upon Control submission during debug (because a thrown exception can be handled or ignored), but is useful in a fully developed app.

Attributes can be added to the Binding statement that will cause the App to update the input control decoration when the exception is thrown: `ValidatesOnExceptions=True` and `UpdateSourceTrigger` (set to Explicit, LostFocus, or PropertyChanged).

### WPF Input Validation by IDataErrorInfo

Use IDataErrorInfo interface to define to implement methods that support input validation and response.

Provide a property to evaluate using an indexer property.

Use a Switch-Case construct to identify each property to validate, the requirement to meet (e.g. `Username.Length < 5`), and what to return in both true and false cases.

Returning `null` tells WPF that there is no error. Returning a value indicates an error.

Attributes must be added to the input Binding: `ValidatesOnDataErrors` and `UpdateSourceTrigger`. This enables the control decoration (thin red border on error).

To allow displaying the return message from the indexing property, a Dictionary can be used to add items that the WPF attribute `ToolTip` can be bound to that provides feedback on the index return (if not null).

Perhaps one thing for me to try is to use a separate Label to show the error condition rather than a Tool Tip, to remain A11y compatible.

### WPF Input Validation by ValidationRule

This method utilizes a newly implemented class that inherits from `ValidationRule` and overrides `Validate(object value, CultureInfo cultureInfo)` method, performs the comparison for validation, and returns a `ValidationResult(bool, string)` for WPF to consume.

A valid result is identified by the `Validate()` method returning `new ValidationResult(true, null)`.

WPF must include Attached Properties with a Binding that identifies the Binding Path, `ValidatesOnDataErrors`, and `UpdateSourceTrigger` (just like the previous examples).

A `Binding.ValidationRules` Attached Property must be added that defines the rule argument (in `Validate()` method).

To display an error message, use a `ControlTemplate` in `Application.Resources` to override "errorTemplate", and define a new Control that includes an `AdornedElementPlaceholder` with a `TextBlock` that Binds to the _first error_ (identified as `[0]`) and its property `ErrorContent` e.g. `{Binding [0].ErrorContent}`.

Then, in the Control that needs the in-line error message, add `Validation.ErrorTemplate="{StaticResource errorTemplate}"` so the error message(s) will appear in-line. This might not be a great A11y solution either, but the simplicity in implementation and effectiveness for sighted users is pretty compelling.

### WPF Input Validation by Annotations

Requires adding a reference to `System.ComponentModel.DataAnnotations` (this might be a .NET Framework 4.x requirement - in .net6 and newer, the library might be available in a `using` statement without adding by library reference).

A `ControlTemplate` in `Application.Resources` will be needed here as well.

Ensure the ViewModel (or the data managing class) is inheriting from `ObservableObject`.

Add the Annotations `[Required(ErrorMessage=string)]` and `[Rule...(args, args, ErrorMessage(string))]` to the properties that require validation. TaskersCorner used `[StringLength(50, MinimumLength=5, ErrorMessage="Must be at least 5 characters.")]`.

As in previous methods, the XAML will need to be updated to include special Binding properties. In ToskersCorner, the example used a TextBox with the Text property set to `{Binding Username, ValidatesOnExceptions=True, UpdateSourceTrigger=PropertyChanged, Validation.ErrorTemplate="StaticResource errorTemplate}`.

The ViewModel (or data class) will need its Setter updated to include `ValidateProperty(value, string Property)` so that WPF can access a public Property that updates the validation data.

## Random Notes

- Assembly name can be edited to cause the EXE to be named something other than the project name. See Project Properties to do this.
- WPF Tools for UI Debugging: Remove it by going to Tools :arrow_right: Options :arrow_right: Debugging :arrow_right: General :arrow_right: Enable UI Debugging Tools for XAML :arrow_right: Uncheck "Show Runtime Tools in Application"

## Resources

YouTube [Tosker's Corner](https://www.youtube.com/watch?v=5KF0GGObuAQ&ab_channel=ToskersCorner).

[WPF with Caliburn.Micro Project Setup](https://www.youtube.com/watch?v=p-fmOJMLl0A&list=WL&index=2&ab_channel=IAmTimCorey).

_Warning_ might be dead :arrow_right: MSFT [MVVM Community Toolkit Samples Project Home](https://github.com/CommunityToolkit/MVVM-Samples).

MSFT [MVVM Community Toolkit Official Documentation](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/mvvm/).

.NET Foundation [Community Toolkit Github Repo](https://github.com/CommunityToolkit) which is the parent container to [CommunityToolkit.Mvvm components in 'src' folder](https://github.com/CommunityToolkit/dotnet/tree/main/src).

[Julian Ewers-Peters has a Blog](https://blog.ewers-peters.de/) that is occasionally updated with CommunityToolkit and DetNET MAUI technical details.

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
