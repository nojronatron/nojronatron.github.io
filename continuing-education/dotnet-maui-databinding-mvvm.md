# Data Binding in DotNET MAUI

## Presenters

- Bruno Capuano @elbruno
- Luis Beltran, MSFT MVP, @darkicebeam, [GitHub](https://github.com/icebeam7)

## MVVM Overview

MVVM: Model, View, ViewModel.

- View: How to display info.
- ViewModel: What to display, flow of interaction.
- Model: Business Logic and data objects.

Note: INotifyPropertyChanged interface must be implemented in the ViewModel where it applies.

Data and Events are passed between View and ViewModel:

- Data: Bidirectional
- Events: From View to ViewMOdel

Data flows between ViewModel and Model:

- Bidirectional

### Application Tasks

View represent values from underlying sources.

Data Binding:

- Links data between View and ViewModel.
- Links properties and events too.

`INotifyPropertyChanged`: Whenever a View changes like data entered into a text control, a property is modified:

- `OnPropertyChanged(propertyName)`: Receives change event.
- `<Label Text="{Binding propertyName}"/>`: Binds View Label element to 'propertyName'.

What about Action Bindings?

- Write event handlers to manage clicks, selections, etc.
- Code-behind must be written to handle.
- `ICommand` interface simplifies managing event binding.
- `<Button Text="Give Bonus" Command="{Binding GiveBounus}" />`
- `public ICommand GiveBonus { get; }`
- Combines XAML and C# code to get the job done.

### DataBinding Basics

Links paris of properties between two objects.

One object is typically a UI object.

- Destination: Target is the object and property on which the data binding is established.
- Source: The object and property that the data binding refers to.

### Data Bindings with Context

Automates the task of setting an event (e.g. 'ValueChanged' of a Slider element) to get the Value property of the element, and set that value to the element Property that should be changed (e.g. 'Rotation' property of a Text element).

No C# Code is required!

- Create the Slider element control.
- Add BindingContext to the Text Element that will have its property changed.
- Add the name of the Text Element property that will be changed and assign it `"{Binding Path=Value}"`.

More:

- `x:Reference` is required to refer to the source objects (Slider).
- `Binding` markup extension links the Label element property to the Value property of the Slider element.

### Implementing a Model

Types contain Properties that store data and sometimes allow modification.

Note: Other functionality (methods) were not mentioned.

### Implement a ViewModel

Must implement INotifyPropertyChanged interface.

- Can create a base class with the interface, others will inherit it.
- Can be done at each Model explicitly if needed.

Define public properties:

- Read-only properties.
- getter/setters.
- Invoke `OnPropertyChanged()` within a Setter.

OnPropertyChanged() notifies any subscribers that the property change changed.

## Dependency Injection

You can use DI in .NET MAUI through the Builder class:

- Interfaces, ViewMOdels, and Views
- AddSingleton your test service
- AddTransient your ViewModel
- AddTransient your specific View/Page

Registered Member access is allowed in the constructor in any class:

- Already available when needed!
- Inject your ViewModel specifically in the CTOR.
- `this.BindingContext = vmViewModel` (your ViewModel specifically).

## Resources

- Check out the Dotnet Community Toolkit [MVVM](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/mvvm/).
- DotNET [MAUI Cloud Skills Challenge](https://aka.ms/Summer.NETMAUI-CSC1).

## Footer

- Return to [ContEd Index](conted-index.html)
- Return to [Root README](../README.html)
