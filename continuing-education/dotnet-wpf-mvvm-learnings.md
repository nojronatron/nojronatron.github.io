# WPF MVVM Learnings

A collection of notes related to developing and building upon MVVM in DotNET WPF.

## Table of Contents

- [Caliburn Micro - Requirements](#caliburn-micro---requirements)
- [Caliburn Micro - WPF with MVVM Project Setup](#caliburn-micro---wpf-with-mvvm-project-setup)
- [Caliburn.Micro - Uses Naming Conventions](#caliburnmicro---uses-naming-conventions)
- [WPF Input Validation](#wpf-input-validation)
- [Random Notes](#random-notes)
- [Resources](#resources)
- [Footer](#footer)

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
- WPF Tools for UI Debugging: Remove it by going to Tools -> Options -> Debugging -> General -> Enable UI Debugging Tools for XAML -> Uncheck "Show Runtime Tools in Application"

## Resources

YouTube [Tosker's Corner](https://www.youtube.com/watch?v=5KF0GGObuAQ&ab_channel=ToskersCorner)

[WPF with Caliburn.Micro Project Setup](https://www.youtube.com/watch?v=p-fmOJMLl0A&list=WL&index=2&ab_channel=IAmTimCorey)

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
