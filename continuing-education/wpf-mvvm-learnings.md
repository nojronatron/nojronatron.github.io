# WPF MVVM Learnings

A collection of notes related to developing and building upon MVVM in DotNET WPF.

## Table of Contents

- [Requirements](#requirements)
- [WPF with MVVM Project Setup](#wpf-with-mvvm-project-setup)
- [Caliburn.Micro](#caliburnmicro)
- [Random Notes](#random-notes)
- [Footer](#footer)

## Requirements

Visual Studio 2019 or newer.

DotNET Framework 4.7+

## WPF with MVVM Project Setup

Reference: [WPF with MVVM Project Setup](https://www.youtube.com/watch?v=p-fmOJMLl0A&list=WL&index=2&ab_channel=IAmTimCorey) video by Tim Corey.

Install NuGet Package Caliburn.Micro (Tim used 3.2.0 but a newer version is currently available that might not support DotNET 4.7 Framework.

The UI Layer is broken-out into Models, ViewModels, and Views.

- Data Access should be in a different Project (a Class Library) or elsewhere in the Project tree.
- Models hold the data for the Views to display.
- ViewModels take the models and bind them to the View.

### Steps

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

## Caliburn.Micro

Relies on naming conventions:

- Binds ViewModel to View to launch the correct XAML
- By default: Models, Views, and ViewModels
- Can be changed but must be configured in Caliburn.Micro to support your custom naming conventions

### Binding Values in ViewModel to a View

Caliburn.Micro:

1. Create a public Property in ViewModel for the data. Use a _full Property_ not just a backing Field or 'auto get-set' notation.
2. Add a Control in the View and give it an `x:Name` that matches the ViewModel's Property.

WPF OneWay Binding:

- Set the control value property (e.g. `Text` for a TextBlock) to `{Binding Path=OtherProp, Mode=OneWay}`
- `OtherProp` refers to the value to copy from.
- The Binding _name_ must match an existing property.
- OneWay means the Binding will accept a value but not change when the other property value changes.

### NotifyOfPropertyChanged

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

### Child Forms

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

### Binding Collections

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

### Binding Events

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

## Random Notes

- Assembly name can be edited to cause the EXE to be named something other than the project name. See Project Properties to do this.
- WPF Tools for UI Debugging: Remove it by going to Tools -> Options -> Debugging -> General -> Enable UI Debugging Tools for XAML -> Uncheck "Show Runtime Tools in Application"

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
