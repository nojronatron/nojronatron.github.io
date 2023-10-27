# DotNET MAUI Learnings Log

This markdown file exists to capture additional learnings about .NET MAUI.

For starters, notes will be made while following MSFT Learn modules.

## Table of Contents

- [Build Mobile and Desktop Apps Training Notes](#build-mobile-and-desktop-apps-training-notes)
- [Installing MAUI](#installing-maui)
- [MAUI UI](#maui-ui)
- [Debug Mode](#debug-mode)
- [Create a UI in a DotNET MAUI App By Using XAML](#create-a-ui-in-a-dotnet-maui-app-by-using-xaml)
- [Customize XAML Pages Layout](#customize-xaml-pages-layout)
- [Static and Dynamic Resources](#static-and-dynamic-resources)
- [App Navigation in MAUI](#app-navigation-in-maui)
- [Consuming REST Web Services](#consuming-rest-web-services)
- [Storing Data Locally](#storing-data-locally)
- [Preferences](#preferences)
- [File System](#file-system)
- [SQLite Database Storage](#sqlite-database-storage)
- [Android Emulator](#android-emulator)
- [About Tizen](#about-tizen)
- [Resources and References](#resources-and-references)
- [Footer](#footer)

## Build Mobile and Desktop Apps Training Notes

MAUI assists with architecture between platforms:

- While the processing libraries can be similar (or the same) on various platforms, the UI and hardware devices differ between desktop, and various mobile and wearable devices.
- User interface implementations, APIs, various sizes, and capabilities like rotation need to be addressed.

MAUI supports creating consistent interfaces on varying hardware platforms, all within a unified project.

### MAUI Tech Stack

A common layer pulls all the API differences together, called a Base Common Library, starting with .NET 6.

- Mono is an open-source version of the .NET Runtime, and supports Android, iOS, and macOS.
- Win32 does the same with various optimizations for mobile and other form-factor devices.
- Platform-specific Libraries are leveraged to access specific hardware features and capability.

### New Dot Nets

These come with .NET MAUI:

- .NET for Android
- .NET for iOS
- .NET for mac
- WinUI

_Note_: WinUI3 is provided by the Mono project.

### DotNET BCL 6

The new Dot Net Libraries sit on top of BCL.

BCL sits on top of Mono Runtime and WinRT runtime.

### Mono and WinRT

These parallel APIs are layered on top of Android, macOS, iOS, and Windows platform APIs.

DotNET MAUI ties these components together in the stack to get cross-platform build-and-run capability.

### XAML

Use XAML to describe the UI and Controls, just like in WPF.

Semantic Properties are used to support Accessibility throughout the UI.

_Note_: UI can be assembled using pure code to enable dynamic responsiveness on the fly.

### Native Code

MAUI always generates native code for the target platform.

Optimizations are performed during the build.

### DotNET MAUI UI Provisions

- Layout Engine
- Page Types for rich navigation
- Data Binding
- Custom Handers for events and presentation
- Access to abstracted APIs (for the target platform)

## Installing MAUI

Requirements, App creation, App structure, and Startup.

### MAUI Install Requirements

Visual Studio 2022 v17.3 or newer and '.NET MAUI Multi-platform App UI Development' workload.

_Note_: There is a preview version of Visual Studio that supports MAUI development on Mac.

### Creating a MAUI App

Three Project Templates are available with .NET MAUI:

- .NET MAUI App
- .NET MAUI Blazor
- .NET MAUI Class Library

_Note_: Create projects _as close to a drive's root folder as possible_ because directory structure lengths can get very long _especially for Android_ projects.

### MAUI App Structure and Startup

- AppShell.xaml: MAUI Application main structure (styling, URI-based navigation, layout options, etc). Jon: Consider this the 'Root' component, a-la React.
- App.xaml: Just like WPF, this is the default XAML Resource-defining file. Resource Dictionaries (and Merged Dictionaries) are supported, as in WPF.Creates the initial Window for the App.
- App.xaml.cs: Like WPF, defines the App Class, and initializes the Application. Common (platform neutral) lifecycle events can be overridden here (OnStart, OnResume, OnSleep...). Also, MainPage is initialized as a new AppShell.
- MainPage.xaml: The UI-defining code page. Controls View items and Controls like Stacks, Images, labels, etc.
- MainPage.xaml.cs: Define event handler logic triggered by the XAML-defined controls.
- MauiProgram.cs: Platform-specific code calls CreateMauiApp method which is leveraged when building for the specified platform. Register fonts, configure DI services and ncustom handlers for controls, etc.
- Resources Folder: Contains various resources such as Styles, Fonts, Images, etc.
- Platforms Folder: Platform-specific initialization code files and resources.

_Note_: `SemanticScreenReader` is a MAUI class with a static member `Announce(string)` that tells a screen reader what to say. Apply this to event handlers in code-behind.

App Class:

- Contains the MAUI App as a whole.
- Inherits default behaviors from the Application class.
- Creates AppShell instance and assigns it to the MainPage property (assigning the first screen the user sees upon launch).
- Methods handle lifecycle events including background/foreground.
- Methods create new `Windows` for the App. Default is a single window but additional can be launched.

Shell Class:

- Contains fundamental features most apps require.
- Common Navigation scheme and methodology (URI-based).
- Integrated Search handler.
- `Flyout`: Parent object to `FlyoutItem`s.
- `TabBar`: Bottom bar used for bottom-of-screen navigation. Contains `Tab` items representing each navigation point.
- `ShellContent`: Represents the ContentPage objects for each Tab.

Pages Class:

- Root of UI hierarchy.
- Inside of `Shell` Class.
- `ContentPage` displays contents (most common page type).
- `TabbedPage`: Used for tab navigation.
- `FlyoutPage`: Enables Master/Detail style presentation. Lists Items for display in a child view.

Views Class:

- Content pages display Views, typically.
- Retreive and present data.
- `ContentView`: The default View.
- `ScrollView`: Adds a scroller to move contens in the View.
- `CarouselView`: Scrollable view using 'swipe' to move through content.
- `CollectionView`: Retreive data from named data source, presenting each using \_format template_s.

_Note_: Create a `Screen` using the `Page` Class.

### Project File Noteworthy Elements

Initial `PropertyGroup` specifies platform frameworks to target, app title, AppID, version, display, and supported OSes. These can be ammended as needed.

`ItemGroup` following that allows specifying image and color for splash screen (app loading visual). Set default locations for fonts, images, and other assets used by the app. See `Resources Folder` for storing the actual items referenced. These should be REGISTERED using `MauiApp.CreateBuilder()` in `MauiProgram.cs`.

## MAUI UI

Controls and Layouts, and modifying Control properties.

### Controls and Layouts

Views contain a single Control (button, label, etc).

Layouts define rules for how Controls are arranged in a View.

StackLayouts:

- Vertical: Top-to-bottom.
- Horizontal: Left-to-right.
- StackLayout.StackOrientation: Adjusts display when user rotates the device.

Other Layouts:

- AbsoluteLayout: Based on _exact coordinates_.
- FlexLayout: Similar to StackLayout, it wraps child controls if they won't fit. Apply alignment rules (like FlexBox child-targeting rules) to align contents left, right, center, etc.
- GridLayout: Defines layout based on rows and columns.

### Modifying Control Properties

Can do this in C# code:

```c#
CounterBtn.Text = $"Clicked {count} times";
```

A View can be _definied purely in C#_ if wanted:

1. Create a partial class and inherit from `ContentPage`.
1. Add fields as needed. Controls can be declared a Class member!!
1. In the constructor, initialize the Views and Layouts, and assign initial values to Fields (like a Label, Button text, etc).
1. Add Event Handler members to execute when Controls are clicked, etc.

_Note_: It will be necessary to take the instantiated Controls and add them to View instances, updating layout options such as `LayoutOptions.Center` and so-on.

Margin and Padding are properties of Controls that the various Layout classes will respect.

VerticalStackLayout and HorizontalStackLayout also have a `Spacing` property that affects the Margin of the child items within the layout.

## Debug Mode

Setup Debugging for Android. Other modes are possible but are not yet documented here.

### Debug Android MAUI App

Tools -> Android -> Android Device Manager: Create a new phone (emulator) and API Level (Google API implementation version).

Debug (Green Arrow) drop-down -> Andoid Emulator -> Pick the correct emulator.

_Note_: Enable Hyper-V on the workstation to improve emulator performance.

_Note2_: A dedicated graphics processor and a Mid- to High-end processor will be necessary to run the Android Emulator without crashing or severe lagging.

### Android Manifest Updates

Make updates to the Android Manifest to allow using native implementation such as dialing the phone.

MAUI abstracts these away into namespaces like `Microsoft.Maui.ApplicationModel.Communication`.

Drill-in to the `Platforms` folder to get to the manifest file for each platform.

If the default Manifest view does not show the needed item(s), use `Open With` dialog to use `Automatic Editor Selector (XML)` to make the edits.

For example, to use the Phone, create an intent element with action and data:

```xml
<...>
  <queries>
    <intent>
      <action android:name="android.intent.action.DIAL" />
      <data android:scheme="tel" />
    </intent>
  </queries>
</...>
```

## Create a UI in a DotNET MAUI App By Using XAML

- Benefits of XAML over code-based UI definition.
- Available types for defining UI in XAML.
- Handling UI Events in XAML.
- Create and use XAML mark-up extensions.
- Set platform-specific values in XAML.

### XAML over Code

- Extensible Application Mark-up Language (XAML) provides a way to generate static UI at _compile time_.
- Separate UI design from behavior using XAML + code, making both easier to manage.
- Code-only design can get difficult for a human to read, especially when the UI is complex.
- XAML is purely _declarative_, and _represent_ objects instantiated in the App.
- XAML is based on MSFT 2009 XAML spec, but are _only sytactical_ specifications.
- WPF, UWP, WinUI 3 all use XAML and elements will change.
- .NET MAUI changes some of the Class names and Properties (from WPF, Xamarin).
- XAML can generate a simple login page in fewer lines than using C# to do the same (although code-behind will add to the count in most instances).
- `InitializeComponent` is _not_ necessary if XAML is not used to define a page layout and controls.

Most importantly: Separate the definition of the UI from the logic of the app.

### Types and Properties

XAML Parser takes XAML and creates objects given the elements with set properties from the XAML definitions.

Most MAUI Controls are located in `Microsoft.Maui.Controls` namespace.

Most Common Types are located in `Microsoft.Maui.Dependencies` and `Microsoft.Maui.Extensions` packages (NuGet).

Utility Types are defined in `Microsoft.Maui` namespace. Example: `Thickness` Utility Type.

Graphics Types are defined in `Microsoft.Maui.Graphics` namespace. Example: `Color`.

XAML Elements, .NET Types, and Custom Types can all be rolled into a custom App with XAML.

Instantiating types in XAML and C# are done differently, but the result is the same:

```XML
// instantiate a Label object
<Label TextColor="Azure" />
```

```C#
// instantiate a Label object
var label = new Label {
  TextColor = Color.FromArgb(255, 0, 127, 255)
};
```

Bringing MAUI Types and other Types into scope can be done in both XAML and C#:

```XML
<!-- import namespaces -->
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" />
<!-- Namespaces are aliases for the assemblies that bring all the things into scope
     first one is .NET MAUI Controls
     second one is intrinsic types (strings, numerics, properties, etc) -->
```

```C#
// import a namespace
using Microsoft.Maui;
// same result!
```

The result of `x:Class="..."` is a reference to the named class within quotes.

```XML
<!-- bring in a custom type called Utils -->
<ContentPage ...
             xmlns:mycode="clr-namespace:Utils"
             ... />
```

### Type Converters

Use Type Converters to convert XML Attributes from `string` to the correct Type.

MAUI has Type Converters for most built-in classes, and they are used automatically.

Custom Type Converters can be written to handle custom cases! Once implemented, associate the conversion to your custom Type to make it usable in XAML.

#### Complex Type Assignment

Some Types are "complex" and need specific setup within XAML.

The example MSFT provides shows a Label with is necessary Attributes (Text, TextColor, etc) and an inner `<Label.GestureRecognizers>` (a complex Type) and an instantiation Property Element form of `<TapGestureRecognizer NumberOfTapsRequired="2" />`.

So using this format `Element.Property` is "Property Element Form", and adds the complex Type to the parent element.

### Default Content

A property that is sometimes set in MAUI Types.

The example given shows a `<VerticalStackLayout>` parent element with a `<Label Text="..." />` child element that does NOT require `<VerticalStackLayout.Children>` Property Element form.

### Event Handling in XAML

- Uses standard event handling via .NET code patterns.
- Controls need unique `x:Name`s.
- `x:Name` represents a POCO private field for interacting with the element.
- `x:Name` represents a path for other XAML elements to access the element.
- `InitializeComponent()` must be executed in order for `x:Name` fields to become available.

#### Event Signatures

Required event handler signature components by .NET convention:

- Must return void.
- Must take 2 parameters, an `object` representing what triggered the event, and an `EventArgs` parameter containing args passed by the sender.
- Should be marked `private`.
- Optional: Async if it needs to execute asynchronous code.

#### Separation of Concerns

Some issues:

- Event handling as described above tightly couples behaviors to the UI.
- Compiler does _not_ catch missing Fields in XAML e.g. "A removed handler isn't caught by the compiler".

Wiring Event Handlers in Code:

- Use subscription syntax `Counter.Clicked += OnCounterClicked;`
- Add the event handler method e.g. `private void OnCounterClicked(object sender, EventArgs e) {...}`
- Optionally, un-subscribe using `Counter.Clicked -= OnCounterClicked;`

### XAML Markup Extensions

Most XAML definitions will be settled at compile time.

Run-time determined variables are sorted using XAML Markup Extensions.

- Specialized class.
- Allows XAML to access runtime values.
- Helps to define attributes with same value settings in one place.
- Replaces hard-coded literal value assignment.

Create a XAML Markup Extension - Implement the ProvideValue method as defined by IServiceProvider interface:

- Accessibility: public.
- Returns: An `object` type.
- Input parameter must match `IServiceProvider` interface.
- Name must be `ProvideValue`.

Drawbacks:

- Must _know_ the actual return value for example a FontSize attribute will expect a `Double` value.
- Added Class is necessary.
- Added Class must implement IMarkupExtension.

Benefits:

- Simply define default values within the code-behind as a static Property.
- Write the value once then use Markup Extensions reference in XAML to use it.

Apply the Markup Extension to a Control:

- Import the namespace in which the Extension Class and its `ProvideValue` member are defined in.
- For the attribute where the value is needed, the value should be defined like: `"{mycode:NameOfExtensionMethod}"`.

_Note_: MAUI XAML recognizes the naming convention with the suffix `Extension` as a XAML Markup Extension, so the namespace import and alias does not need to include `Extension` during assignment in the XAML header.

#### StaticExtension Class

StaticExtension (aka 'Static') is a short-hand way of creating and using a XAML Markup Extension.

```C#
[ContentProperty("Member")]
public class StaticExtension : IMarkupExtension
{
  public string Member {get; set;}
  public object ProvideValue (IServiceProvider serviceProvider)
  {
    // code returns a type that inherits from Object
  }
}
```

Utilize this extension the same way as before:

- Import the namespace where the StaticExtension class is defined.
- Define the value for the attribute using `"{x:Static Member=mycode:MainPage.NameOfExtensionMethod}"`

### Platform Specific Values in XAML

Fine-tune your UI for each platform.

Layout management is provided in MAUI.

`DevinceInfo` Class:

- Provides device-specific info about the device on which the code is running.
- Properties are used to expose the information.
- `DeviceInfo.Platform` returns a string such as "Android", "iOS", "WinUI", or "macOS".

For situations where applying an attribute (like `Padding`) to solve a layout problem on one device _won't solve the problem_ on all devices, necessarily.

Use a turnary clause to provide the correct values depending on the device type return by `DeviceInfo.Platform`.

Example provided by _[MSFT Learn]_:

```C#
MyStackLayout.Padding =
  DeviceInfo.Platform == DevicePlatform.iOS // struct iOS returns a string
    ? new Thickness(30, 60, 30, 30) // shift content down for iOS only
    : new Thickness(30); // default margin for non-iOS devices
```

_Note_: Since the tweak is for the UI, it is usually preferred to make these types of changes in the UI layer, i.e. XAML. The next sub-section addresses this.

#### OnPlatform Markup Extension

Enables detecting the runtime platform within XAML!

- Apply extension as part of XAML code that sets a property value.
- Requires providing type of property.
- Requires setting values to property via series of `<On Platform="..." Value="..." />` blocks.
- OnPlatform is generic and accepts a `type` parameter.

Example provided by _[MSFT Learn]_:

```XML
<VerticalStackLayout>
  <VerticalStackLayout.Padding>
    <OnPlatform x:TypeArguments="Thickness">
      <On Platform="iOS" Value="30,60,30,30" />
      <On Platform="Android" Value="30" />
      <On Platform="WinUI" Value="30" />
    </OnPlatform>
  </VerticalStackLayout.Padding>
  <!-- XAML for other controls go here -->
</VerticalStackLayout>
```

Use this extension to define other attribute values such as `x:TypeArguments="Color"`, etc.

Key Takeaway: Customize the UI for each platform using `OnPlatform`.

##### OnPlatform Reduced Syntax

Simplify by using a Default Value for any non-match _[MSFT Learn example]_:

```XML
<VerticalStackLayout Padding="{OnPlatform iOS='30,60,30,30', Default='30'}">
  <!-- XAML for other controls go here -->
</VerticalStackLayout>
```

## Customize XAML Pages Layout

Specify View Size:

- Various devices have varying default view sizes and pixel ensities.
- Mobile, tablet, phone, desktop, wearable, etc.
- Layout Panels build consistent UIs, controlling sizing and positioning of child controls.

### Layout Panel

- Hold collections of child views (Controls).
- Determines size and position.
- Recalculation of position and size are automatic.
- Support device rotation.
- Stack, Absolute, Grid, and Flex Layout Panels are available.
- StackLayout: Single row or column.
- VerticalStackLayout, HorizontalStackLayout: Vertical or horizontal alignment, respectively.
- AbsoluteLayout: Utilizes x,y coordinates to place child Controls.
- FlexLayout: Enables wrapping child Controls if they don't fit into a single row or column.
- Grid: Child Controls are placed within identified row or column IDs, and can be told to stay within that 'cell', or to span cells (rows or columns).

_Note_: RelativeLayout is similar to FlexLayout, but _FlexLayout should be used due to better performance_.

### View Size Configuration

Affects how the parent element sizes itself around its content.

- Un-set: Element will auto-grow to be large enough to fit around its content.
- Set: WidthRequest and/or HeightRequest attribute(s) are configured on the element.

The `Request` portion means at run time the App will make a final decision on size based on available space for the element and its contents.

### Platform Sizing Considerations

Size units are different on some platforms:

- iOS: points.
- Android: DIPs (density-independent pixels).

MAUI _does not use device-specific values at all_:

- Stores the value as a `double`.
- Abstracts the actual unit concerns away from the developer.
- The Device OS makes the final conversion during run time.

Rendered Size of a View:

- The View Class stores actual rendered size values.
- Hidden properties store actual _rendered values_.
- Width and Height (as expected).
- Request\* property will still be as set at build time, but actual Width and Height (rendered) properties might be different.

### Positioning Considerations

Left, right, or center of the screen?

Left, right, or center of the parent element?

View base class has VerticalOptions and HorizontalOptions properties:

- Enables aligning with one of the 'four edges' of the content 'box'.
- Allows centering within the box.
- Properties are of type `LayoutOptions`: A struct with properties `<LayoutAlignment>Alignment` and `<bool>Expands`.
- `LayoutAlignmnet` Type is an `enumeration` of Start, Center, End, and Fill.
- `LayoutAlignmnet` controls how child view is positions within the box, given inheritance from it's parent Layout Panel.
- `Expands` property allows requesting extra space if available (from `Xamarin.Forms`). Is obsolete in MAUI, use `Grid` instead!

### Layout Properties

- StackLayout Spacing: Add units to put space between each child Control.
- Stack Orientation in XAML: `<StackLayout x:Name="stack" Orientation="Horizontal">`
- HeightRequest and WidthRequest get swapped (rotated) when Orientation is changed from default (StackLayout default=Vertical, HeightRequest={width}, WidthRequest={height}).

_Note_: Recall VerticalStackLayout and HorizontalStackLayout handle StackLayout `Orientation` property automatically.

`Expands` deprecated property replaced by `StartAndExpand`, `CenterAndExpand`, `EndAndExpand`, or `FillAndExpand`:

- In Xamarin.Forms, `AndExpand` option should be replaced with the MAUI versions.

Optimized StackLayouts:

- `VerticalStackLayout` and `HorizontalStackLayout`.
- Simpler to use than `StackLayout` plus its options.
- Offers best layout performance.
- Also simplifies `Spacing` property setting.

### Grid Layout Panel

- Rows and Columns (think Grid in Bootstrap and React-Bootstrap).
- Content (and Controls) are placed inside the 'cells' at teh intersections of each ROW and COLUMN.
- Rows and Columns can be different sizes or set to auto-adapt to the size of child items within the cells.
- Use `RowDefinition` and `ColumnDefinition` to set the height of each row and the width of each column.
- Width and Height properties are of type `GridLength`, with its own properties `GridUnitType` and `Value`.
- GridUnitType value Absolute: A specified unit e.g. 1-100.
- GridUnitType value Auto: Sets row/col size to fit child Controls.
- GridUnitType Star (\*): Proportional sizing, determined using a ration formula from total available space and requested space by all cols/rows.

GridUnitTypeStar, same effect, both ways:

- Code: `new GridLength(2, GridUnitType.Star);`
- XAML: `<RowDefinition Height="2*" />`

_Note_: The default size for any Row or Column is `1*`.

XAML definitions can be shortened like this:

```XML
<Grid RowDefinitions="*, *, *" ColumnDefinitions="*, *">
  <!-- row and grid controls -->
</Grid>
```

#### Grid Layout Attached Properties

Attached Properties are defined in one class but set on objects of other Types.

- KVP's that are part of a View.
- IDs are zero-indexed (starting with 0 for the first cardinal instance).
- Use `<BoxView Grid.Row="1" Grid.Column="2" ... />` to tell the BoxView to stay in Row 1, Column 2 of the Grid.

#### Grid Spanning

Span BoxView across 2 columns (cols must be previously defined): `<BoxView Grid.Row="1" Grid.Column="0" Grid.ColumnSpan="2" ... />`

## Static and Dynamic Resources

Define style information in one place and have MAUI "look them up" so they are applied consistently across your APp.

- Fonts
- Font and Foreground Colors
- Background Colors
- Borders and other style settings

### XAML Resources

Symbolic constants are defined in one place and referenced everywhere it is needed.

`Style` and `OnPlatform` instances can be set as Resources!

Define a XAML Resource _[MSFT Learn example]_:

```XML
<Color x:Key="PageControlTextColor">Blue</Color>
```

Store Resources in a Resource Dictionary

### XAML Resource Dictionary

.NET MAUI has a specific class for this: `ResourceDictionary`.

- Customized for use with UI resoruces.
- Stores Key-Value pairs.
- Create an instance of ResourceDictionary before tyring to use it.

```XML
<ContentPage.Resources> <!-- this is REQUIRED -->
  <ResourceDictionary> <!-- this is actually OPTIONAL -->
    <Color x:Key="PageControlTextColor">Azure</Color>
    <!-- more Resources defined here -->
  </ReseourceDictionary>
</ContentPage.Resources>
```

Ways to use Resource Dictionaries:

- Create Control-specific Resources and Resource Dictionaries in-line with the Control definition.
- Create page-specific Resource Dictionariese within the Page where the resources are needed.
- Create a separate Resource Dictionary code page that multiple pages within the App can use.

_Note_: The order of entries within a Resource Dictionary are important, especially in cases where Style [BasedOn](#basedon-style-inheritance) and Style [overrides](#override-a-style) are used.

### Apply a Static Resource

Markup Extension looks up resources in a resource dictionary, by Key.

Static Resources are only looked up _once_. Changing the resource during Run Time will _not have an effect_.

Code courtesy of _[MSFT Learn]_:

```XML
<Label TextColor="{StaticResource PageControlTextColor}" ... />
<!-- Key is 'PageControlTextColor' and the value returned will be placed in the TextColor attribute at Run Time -->
```

_Note_: Static Resources will throw a Runtime Exception if the Key is not found.

### Intrinsic Types

Remember these in C#? Well, they exist in XAML, too!

For example, initializing a Double variable in XAML is this simple: `<x:Double x:Key="MyDouble">12.3</x:Double>`.

This applies to FONTs as Strings, Font Size as Double, and other intrinsic Types like Boolean, Int64, Byte, etc.

### Platform-Specific Values for a Resource

Use `OnPlatform` to get slightly different UI Control Styles and settings based on the Platform at build time.

Code courtesy of _[MSFT Learn]_:

```XML
<ContentPage.Resources>
  <OnPlatform x:Key="textColor" x:TypeArguments="Color">
    <On Platform="iOS" Value="Silver" />
    <On Platform="Android" Value="Green" />
    <On Platform="WinUI" Value="Azure" />
    <On Platform="MacCatalyst" Value="Pink" />
  </OnPlatform>
</ContentPage.Resources>
```

### Dynamic Resources

Another Markup Extension!

- Performs a dictionary lookup, like Static Resoruces.
- Lookup happens when Control is _created_.
- Listens for _changes_ to the Resource Dictionary and when detected, _automatically updates the UI_ during Run Time.

Places to use Dynamic Resources instead of Static:

- Values that must be changed at Run Time.
- User-controlled theme color schemes.
- User-preferences are stored in a DB and loaded at next login, then applied to the user's UX.

Dynamic Resources are scanned dynamically at RunTime, whereas Static Resources are scanned just once, and that scanned-in value is used for the lifetime of the App.

Imposes a small resource penalty on the Application, vs Static Resources.

#### Update Dynamic Resources at Run Time

Add new, Remove or Update existing Resources!

Code-behind allows making these changes _[MSFT Learn example]_:

```C#
this.Resources["PanelBackgroundColor"] = Colors.Green;
```

Reference Dynamic Resources similarly to Static Resources in XAML _[MSFT Learn example]_:

```XML
<StackLayout BackgroundColor="{DynamicResource PanelBackgroundColor}">
```

### Style Setters

Using StaticResource and DynamicResource can start to clutter XAML.

Defining new, or editing existing Controls takes a fair amount of XAML code and can make a Page XAML code hard to read and maintain.

Use a Setter to help solve this problem:

- Container for a property/value pair.
- Represents an _assignment statement_.
- Specify a property, then assign a value.
- Values can be hard-coded, StaticResource, or a DynamicResource!

_Note_: All Properties on Controls in .NET MAUI whose name suffix is `Property` is a _Bindable Property_ and is necessary for use in Setters. For example, `TextColorProperty` is a BindableProperty and can be used directly in a Setter. Other Properties of Controls that are not already bindable properties must be handled differently. Thankfully, _most of the time_ MAUI's built-in Control Properties already have a bindable property definition.

Styles are a collection of Setters targeting a specific Control Type.

- This is a Type-safe operation.
- Ensures Properties that a Control _can_ take are applied, and not ones it cannot support.
- If a collection of Setters (a Style) targets on Control Type and has properties that another Type does not support, it _cannot_ be applied to that other Control Type.

Define Styles as resources within a Resource Dictionary object.

- Simplifies use across multiple Controls.
- Applies across an entire page _or the entire application_, you choose.
- Use Key-Value syntax to create Style using Setters.

Example from _[MSFT Learn documentation]_

```XML
<ContentPage.Resources>
  <Style x:Key="MyButtonStyle" TargetType="Button">
    <!-- Setter collection here -->
  </Style>
</ContentPage.Resources>
```

### Applying a Style

Attach a Style through the Style property of a Control (_[MSFT Learn example code]_):

```XML
<Button Text="OK" Style="{StaticResource MyButtonStyle}" />
<Button Text="Cancel" Style="{DynamicResource CancelButtonStyle}" />
```

### Implicit Styles for Multiple Controls

Apply the same Style to all Controls on a page (or App):

- Add a Style to a resoruce dictionary.
- Do _not_ assign an `x:Key` identifier.
- `TargetType` is used instead, to apply Style to all Controls of the same Type.

Limitations:

- `TargetType` _must be an exact match_.
- Inheritance _does not count_ and the Style Setters will be ignored.
- Instead use `Style.ApplyToDerivedTypes` attribute and set to `True` in the Style definition.

### Override a Style

Use this technique when a closely-matched Control exists, and just override a few of the Setters.

Explicitly set Style settings are applied _after_ the base Control styles, so they will override.

Steps:

1. All buttons except one need to have the same Style applied.
2. Create the Style using Setters and assign an `x:Key` KVP name and `TargetType` so the styles will be applied.
3. For the button that needs Style overrides, only update the properties that need to be changed.

For example, all buttons are configured to have a Green background and Grray foreground, except the 'Exit' button which needs to be Black background and White foreground:

```XML
<!-- Buttons will have Green background, Gray text, and a medium-thin border with curved corners -->
<Style x:Key="MyButtonStyle" TargetType="Button">
  <Setter Property="BackgroundColor" Value="Green" />
  <Setter Property="BorderRadius" Value="12" />
  <Setter Property="BorderWidth" Value="4" />
  <Setter Property="TextColor" Value="Gray" />
</Style>

<!-- set Exit button overrides TextColor and BackgroundColor just for itself -->
<Button Text="Exit"
        Style="{StaticResource MyButtonStyle}"
        TextColor="White"
        BackgroundColor="Black" />
```

### Target an Ancestor

Use `TargetType` set to 'VisualElement', a base Class for several Controls (e.g. Button and Label).

### BasedOn Style Inheritance

Many Style definitions will repeat lots of the same Setters, such as BackgroundColor.

Example _[MSFT Learn]_ code:

```XML
<!-- base Style to base another off of -->
<Style x:Key="MyVisualElementStyle" TargetType="VisualElement">
  <Setter Property="BackgroundColor" Value="Blue" />
</Style>

<!-- altered Style based on MyVisualElementStyle, simplifying the code -->
<Style x:Key="MyButtonStyle" TargetType="Button" BasedOn="{StaticResource MyVisualElementStyle}">
  <Setter Property="BorderColor" Value="Navy" />
  <Setter Property="BorderWidth" Value="5" />
</Style>
```

### Application-Wide Resources

When defining Resources within a specific Page of an App, those Resources are _only available to that same page_.

Avoiding repeated code throughout your application, especially as it gets bigger and more complex, will require an App-Wide Resource Dictionary - a single place to set UI Control Styles.

About `VisualElement`:

- A Class.
- Defines `Resources` property.
- Controls, pages, and layouts inherit from VisualElement.
- `Application` Class defines its own Resources property.
- Each Resources property can hold their own `ResourceDictionary` of Resources.

Diagram of MAUI Application Organization:

```text
=================================================
|           Application Layer                   |
- - - - - - - - - - - - - - - - - - - - - - - - -
|     Page            |   |   Page              |
- - - - - - - - - - - -   - - - - - - - - - - - -
|     Layout          |   |   Layout            |
- - - - - - - - - - - -   - - - - - - - - - - - -
| View | View | View  |   | View | View | View  |
=======================   =======================
```

Therefore, define Application-level Resources at the Application layer through the `Application` Class like this example from _[MSFT Learn]_:

```XML
<Application.Resources>
  <Color x:Key="MyTextcolor">Azure</Color>
</Application.Resources>
```

#### How MAUI Searches for a Resource

Searches the tree for the _first instance of the key_ and then uses that value.

1. Search the VisualElement instance ResourceDictionary.
2. Search the parent Control ResourceDictionary e.g. Layout.
3. Search the parent Control ResourceDictionary e.g. Page.
4. Search the Application Class ResourceDictionary.
5. If Key is not found, App will use default values for Styling.

`x:Key` definitions can be duplicated across layers without issue (technically).

- Code might be more difficult to understand if Layout, Page, and Application all have the same Key with different settings!
- Debugging the UI might be more difficult.

Jon's Advice: Push Style setters to the highest possible Resource Dictionary.

- Putting it too high causes the Search for the ID to consume more resources.
- Putting it too low (e.g. in the View), blocks Layout or Page level Controls from using that same key setting.

## App Navigation in MAUI

Flyout:

- Window of menu items slides (flies) from the side of the device screen.
- Invoked by tapping a "hamburger menu" icon like [:hamburger:].

Tab:

- A row of touchable controls is permanently displayed at top or bottom of the screen.
- Mechanism to select between pages in a multi-page app.

Stack:

- URI-based navigation.
- Allows drilling-down into content.
- Routes to any page in the app, forward and backwards.

### Flyout Navigation

Composed of:

- Header
- FlyoutItems
- MenuItems
- Footer

Usually used to allow navigation between different pages of an App.

Class: `FlyoutItem`

- Implements flyout navigation.
- Part of the [Shell App Developpment paradigm](https://learn.microsoft.com/en-us/dotnet/maui/fundamentals/shell/) in MAUI.
- Subclass of `Shell` class.
- Sibling to `TabBar` class.
- `ShellContent` property defines the page that is displayed when the flyout... flies out.
- Requires hosting within a `Shell` page.
- Unlimited number of Flyouts are allowed within a Shell page.

Implicit Conversion simplifies implementation:

- Container Hierarchy: `Shell` can only contain `FlyoutItem` or `TabBar` objects, both of which can only contain `Tab` objects, which can only contain `ShellContent` objects.
- Therefore a `Shell` class can contain `ShellContent` objects directly.

Example code snippets from _[MSFT Learn]_:

```XML
<Shell xmlns="..."
  >
  <ShellContent Title="Cats"
                Icon="cat.png"
                ContentTemplate="{DataTemplate views:CatsPage}" />
  <!-- additional ShellContent instances here -->
</Shell>
```

#### Flyout Menu Items

`MenuItem` object:

- Similar to `Button` Class.
- Tappable.
- Can add these to a Flyout.
- Order of declaration determines visual order in the Flyout.

#### Flyout Header and Footer

Content that optionally appears at top (or bottom) of Flyout.

Appearance defined by `Shell.FlyoutHeader` (or `Shell.FlyoutFooter`) bindable property.

Code snippet from _[MSFT Learn]_:

```XML
<Shell ...>
  <Shell.FlyoutHeader>
    <Grid>
      <Image Source="....jpg" />
    </Grid>
  </Shell.FlyoutHeader>
</Shell>
```

Same with Footer.

### Tab Navigation

Navigate a user on a permanent tab strip at the top or bottom of their device screen.

- Each Tab in a tab strip represents specific section or page of an App.
- Tabs are usually indicated using icons, usually with single-word descriptions.
- Tab strips are _always visible_ on the screen.
- Upon clicking/tapping, user is navigated to the connected page.
- Use to connect frequently access pages within the App.

_Note_: If more than 4-5 items in a tab strip, consider using a different navigation scheme.

#### TabBar Object

Implement Tab navigation using `TabBar`:

- Displays a set of tabs.
- Automatically switches displayed content when user selects a tab.
- Contains a content area that displays a `Page`.
- Contains `Tab`s with icons + short words for navigating the App.

TabBar _must_ be instantiated as a child to the `Shell` class.

Add `Tab` objects to the `TabBar`.

Within a Tab object, a `ShellContent` object should be set to a `ContentPage` object.

Create a Tabbed Page:

1. Define an xmlns path to the folder that will contain the Tab Pages.
1. Define `<TabBar>` within `<Shell>`.
1. Instantiate a `<Tab>` with a Title and perhaps an Icon property.
1. Set a `<ShellContent>` object with a `ContentTemplate` property pointing to a DataTemplate property referencing the `Page` that should be displayed.

### Stack Navigation

Shell class defines navigation properties:

- `BackButtonBehavior` of type `BackButtonBehavior` is an attached property. Defines behavior of the Back button.
- `CurrentItem` of type `ShellItem`: The currently selected Item.
- `CurrentPage` of type `Page`: The currently selected Page.
- `CurrentState` of type `ShellNavigationState`: Current navigation state of the Shell.
- `Current` of type `Shell`: Type-casted alias for `Application.Current.MainPage`.

This is a good choice when there are any number of target content pages to navigate to:

- More than 4-5 tabbed or flyout items could be replaced with Stack Navigation using Registered Routes.
- Other external (to the visual tree) content should be referenced through Stack Navigation.

#### Stack Nav Routes

Navigation requires a URI to navigate TO:

- Route: Defines path to content that is part of Shell visual hierarchy.
- Page: Can be 'pushed' onto the Navigation Stack as required.
- Query Parameters: Can be passed to destination Page during navigation.
- All three components results in: `//route/page?queryParameters`.

##### Register Routes

Routes can be defined on these Types by using their `Route` properties:

- FlyoutItem
- TabBar
- Tab
- ShellContent

Example Route property from _[MSFT Learn]_:

```XML
<Shell ...>
  <FlyoutItem ...
    Route="astronomy">
      <ShellContent ...
        Route="moonphase" />
      <!-- etc -->
  </FlyoutItem>
</Shell>
```

Absolute route URI to moonphase is `//astronomy/moonphase`.

##### Register Detail Routes

For any content that is not in the Visual Hierarchy, register the route then navigate to it using the registered name value:

- `Routing.RegisterRoute`: Supply description and a `typeof()` with the pagename as the type argument.
- `await Shell.Current.GoToAsync("myCustomPageIdentifier");`: Navigates to the registered route.

This includes navigating between pages _within tabbed pages_.

Backward Nav:

- Similar to traversing a folder hierarchy, use `..` as the target definition.

Passing Data:

- Primitives can be passed as `string`-based query params.
- Just like in REST-based query, use the `?` symbol and `ID=value` syntax.

Retreiving Data:

- Use the `QueryPropertyAttribe` decorator when defining the body page class.

## Consuming REST Web Services

- Use `HttpClient`.
- Perform basic CRUD operations.
- Detect when connected to the internet.
- Utilize native networking stacks.

### Handling Network Connectivity Overview

Connections could be WiFi or Cellular so your App needs to not fail when connectivity changes:

- WiFi bandwidth might be higher than Cellular.
- Cellular might be available but WiFi not, even though WiFi radio is on.
- Connections are not guaranteed especially while travelling by car, bus, airplane, etc.

Responding to network-related issues:

- App could handle the loss of connectivity silently.
- If network connection is required but not available, App should tell user what is wrong and whether changing a setting could fix it.

### Detecting Network Connectivity

Use `Connectivity` class.

- Exposes `NetworkAccess` property, which has an enumeration called `NetworkAccess`.
- Event `ConnectivityChanged` is also exposed
- `NetworkAcess` property is available via the `Current` property.
- Platform-specific code is managed under the `Current` property.

NetworkAccess enumeration:

- `ConstrainedInternet`
- `Internet`
- `Local`
- `None`: No access to the internet!
- `Unknown`

Example code from _[MSFT Learn]_:

```c#
if (Connectivity.Current.NetowrkAccess == NetworkAccess.None)
{
  ...
}
```

Event `ConnectivityChanged` is triggerred automatically when network connectivity changes.

- `ConnectivityChangedEventArgs`: Passed to the event handler.
- `IsConnected`: Boolean, member of `ConnectivityChangedEventArgs`.

Portions of this code are from _[MSFT Learn]_:

```c#
// register the event handler
Connectivity.Current.ConnectivityChanged += Connectivity_ConnectivityChanged;

// event handler
void Connectivity_ConnectivityChanged(object sender, ConnectivityChangedEventArgs e)
{
  // leverage the EventArgs inheritor built-in property to get connectivity status
  bool stillConnected = e.IsConnected;
}
```

### Consume a REST Service

REST architecture uses well-defined _verbs_ representing operations in requests.

REST verbs enable CRUD operations (Create, Read, Update, and Delete).

REST service respond to requests in a standardized way.

The `HttpClient` class:

- `System.Net.Http`.
- Use to send HTTP requests.
- Use to receive HTTP responses from a REST service.
- URIs are used to identify web service endpoints and include the "address" and "name of the resource" the REST endpoint.
- Uses a _Task-based API_.
- Exposes HTTP Headers.
- Exposes Request message bodies.

CRUD to REST translation:

> CREATE <==> POST
> READ <==> GET
> UPDATE <==> PUT
> DELETE <==> DELETE

#### Create a Resource

Create a new Resource with code from _[MSFT Learn]_:

```c#
// this is an async method code block
HttpClient client = new HttpClient();
// request contains http verb 'Post' and url 'url'
HttpRequestMessage message = new HttpRequestMessage(HttpMethod.Post, url);
// serialize the 'parp' variable into JSON for sending to REST service
message.Content = JsonContent.Create<Part>(part);
HttpResponseMessage response = await client.SendAsync(message);
```

#### Read a Resource

Convenience methods are included with HttpClient that shorten code in an HTTP Request:

Example code portions from _[MSFT Learn]_:

```c#
HttpClient client = new HttpClient();
// response will be returned as a string, which could be XML, JSON, or some other formatting
string text = await client.GetStringAsync(url);

// if response is going to be JSON then use the following instead
client.DefaultRequestHeaders.Accept.Add(new TypeWithQualityHeaderValue("application/json"));
// only response message body is returned within an HttpResponsemessage object instance
```

#### Update a Resource

Use `HttpRequestMessage` initialized with `PUT` verb (code snippets from _[MSFT Learn]_):

```c#
HttpClient client = new HttpClient();
HttpRequestMessage message = new HttpRequestMessage(HttpMethod.Put, url);
message.Content = JsonContent.Create<Part>(part);
HttpResponseMessage response = await client.SendAsync(message);
```

Idempotency: The same operation will always have the same result. Submitting multiple PUT requests in a row with the same data will perform the exact same action as the 1st request. Submitting multiple POST requests with the same data will continue to create new items at each request. Server-response codes and messages might be different in subsequent identical requests regardless of the idempotency of the request type.

#### Handle Response from Request

Always expect a response message.

- Includes which 'verb' was used.
- Potentially, the requested resource.
- A response code (200, 201, 202, 400, 403, 404, 500, etc).

Redirection codes:

- Codes in the 3xx range are 'redirect' codes.
- A different address might actually be handling the request.

Verify the status code in a response message, from _[MSFT Learn]_:

```c#
static readonly HttpClient client = new HttpClient();

...
// call asynchronous network methods in a try-catch block to handle exceptions
try
{
  // initiate the HttpRequest
  HttpResponseMessage response = await client.SendAsync(msg);
  response.EnsureSuccessStatusCode(); // check that code IS WITHIN the 2xx range otherwise throw HttpRequestException
  string responseBOdy = await response.Content.ReadAsStringAsync();
  // handle the response
  ...
}
catch(HttpRequestException hrex) {
  // handle status codes from `e.StatusCode` that indicate the error condition
}
```

### Platform-Specific Features

MAUI Templates map HttpClient to a layer that handles native networking stacks of each platform.

Varying platforms have different security layer implementations, but MAUI manages that for you -- to a point.

#### App Transport Security on iOS

ATS requires Http Apps to use TLS 1.2 or above.

Apps that don't use ATS will be denied network access.

How to work with ATS:

1. Change endpoint to adhere to ATS policy, or
2. Opt-out of using ATS altogether.

Opt-out:

1. Add new key to `Info.plist` file (a Dictionary) called `NSAppTransportSecurity`.
2. Add a new key to `Info.plist` called `NSExceptionDomains`.
3. Add children to it for each endpoint your App will taget.

Editing `Info.plist` can be done using Visual Studio's generic PList Editor, or by editing the XML directly.

Targeting Keys look like this example from _[MS Learn]_:

```xml
<key>NSAppTransportSecurity</key>
<dict>
   <key>NSExceptionDomains</key>
      <dict>
      <key>dotnet.microsoft.com</key>
      <dict>
        <key>NSExceptionMinimumTLSVersion</key>
        <string>TLSv1.0</string>
        <key>NSExceptionAllowsInsecureHTTPLoads</key>
        <true/>
      </dict>
   </dict>
</dict>
```

It is helpful to use the OPT-OUT method for locally debugging a service on the dev machine like this example from _[MS Learn]_:

```xml
<key>NSAppTransportSecurity</key>
<dict>
    <key>NSAllowsLocalNetworking</key>
    <true/>
</dict>
```

Optionally, ATS can be disabled completely using code like this example from _[MS Learn]_:

```xml
<key>NSAppTransportSecurity</key>
<dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
</dict>
```

#### Configure Android Network Security

API Level 28 (Android 9) introduced a policy that disables non-HTTP clear text traffic.

This policy blocks downloading images or files from servers that are not configured for HTTPS, or there are no development certificates installed during dev or debug time.

To permit clear text traffic:

1. Create a new AML file in `Resources/xml` and name it `network_security_config.xml`.
2. Add element `network-security-config` with a `domain-config` child element.

Permitting clear text traffic look like this example from _[MS Learn]_:

```xml
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
  <domain-config cleartextTrafficPermitted="true">
    <domain includeSubdomains="true">10.0.2.2</domain> <!-- Debug port -->
    <domain includeSubdomains="true">microsoft.com</domain>
  </domain-config>
</network-security-config>
```

Securing _all_ traffic on Android device regardless of target API level:

1. Set `domain-config` child element `cleartextTrafficPermitted` to false in `network_security_config.xml`.
2. Enable Android to use the xml by setting the `application` element according to the examle code from _[MSF Learn]_, below.

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest>
    <application android:networkSecurityConfig="@xml/network_security_config" ...></application>
</manifest>
```

#### Debug Apps Locally

Use iOS Simulator and Android Emulator to consume ASP.NET Core web services running locally over HTTP.

- iOS: Opt-out of ATS by specifying `NSAllowsLocalNetworking`.
- Android: Use IP address `10.0.2.2`, an alias for `127.0.0.1`, and set up the network security configuration for using the loopback address.

For example the `GET` request would be sent to localhost by configuring `http://10.0.2.2:/api/myEndpoint`.

#### Detect the Operating System

Use `DeviceInfo` class to determine OS the App is running on.

Set the `BaseAddress` for calling the API Endpoint to a different value based on the detected OS value.

Example code snippet from _[MSFT Learn]_:

```c#
public static string BaseAddress = DeviceInfo.Platform == DevicePlatform.Android
  ? "http://10.0.2.2:5000"
  : "http://localhost:5000"
public static string ItemsUrl = $"{BaseAddress}/api/items/";
```

## Storing Data Locally

Mobile apps often store data locally for performance reasons, same is true for .NET MAUI.

There are several storage options in .NET MAUI applications:

- Filesystem: Device files store the data locally.
- Preferences: KVP storage.
- SQLite: Light-weight relational data storage.

## Preferences

- Simple data types such as string, boolean, integer, etc.
- Often used to store User Selections.
- Application configuration.
- Key-value pairs.
- Cannot store complex types such as Lists, Collections, or Arrays (use File System or Database instead).

`Preferences` can be used directly to set and get KVPs:

```C#
string dataToStore = "data to be stored locally.";
Preferences.Set("dataKeyAlpha", dataToStore);
var savedPreference = Preferences.Get("dataKeyAlpha", false);
```

`Preferences` also has methods:

- `ContainsKey` -> boolean
- `Remove` -> removes a key
- `Clear` -> all Preference data is removed

## File System

Appropriate for:

- Saving 'loose' files like XML, binary, or text.
- Log data.
- Serialized data structures.
- Data structures to store during shutdown/restart that will be reconstituted to memory on startup/login.
- JSON formatted is fairly universal, but other plain text formats will suffice.

Use `System.Text.Json` and `System.IO`:

```C#
using System.Text.Json;
using System.IO;

List<Item> items = ...;

// serialize and save
string fileName = "data-store.json";
var serializedData = JsonSerializer.Serialize(Items);
File.WriteAllText(fileName, serializedData);

// read and deserialize
var rawData = File.ReadAllText(fileName);
items = JsonSerializer.Deserialize<List<Item>>(rawData);
...
```

### App Sandbox

Private area within the MAUI App for writing and reading files.

Only the Platform OS and the current User can access the App Sandbox.

`AppDataDirectory` is a static property of `FileSystem` that returns a string representing the sandbox path.

- Is an abstraction.
- Each platform has it's own underlying implementation.
- Developers do _not_ have to access drive-specific paths in code.
- Best practice is to use the Sandbox path instead of drive-specific paths.

Apple Sandbox Guidelines:

- Library: Returned by `AppDataDirectory`. Use to store App-generated data.
- Documents: `Environment.SpecialFolder.MyDocuments`. Store user-generated data (stored in direct response to a user action).

## SQLite Database Storage

When to use a database:

- Using Relational data.
- Using complex data types like Lists, Collection, Arrays, and etc.
- Unique data should be stored.
- Filtering of data is necessary.
- Searching data is necessary and search performance is important.

Database _is a file_ that must be stored.

- Recommend `AppDataDirectory`.
- Common SQLite implementation is `SQLite-net`.
- Lightweight local DB.
- Cross-platform.
- Industry standard for mobile.
- Not server required.
- Single-file storage on device file-system.
- Read/Write operations are done _directly against the DB file_.

A Caveat: Android and iOS native SQLite implementation support C/C++ but not .NET directly.

Note: There are other C# "wrappers" for SQLite.

### SQLite-net Features

- An Object-Relational Mapper (ORM).
- Simplifies schema design.
- Use native-code models to define the schema and entities.

Requires:

- NuGet
- `sqlite-net-pcl`
- For Android support also include `SQLitePCLRaw.provider.dynamic_cdecl` package

See the SQLList Project Home and Wiki links in the [Resources and References](#resources-and-references) section.

_Note_: Skipping `SQLitePCLRaw.provider.dynamic_cdecl` package will ensure an initialization error in the SQLite Connection constructor. See [Type Initializer for SQLite.SLiteConnection threw an exception](https://stackoverflow.com/questions/46915404/the-type-initializer-for-sqlite-sqliteconnection-threw-an-exception) on StackOverflow.

### SQLite Connect

Use `SQLiteConnection` object.

- Pass-in the filename for the DB file.

```C#
using System.IO;
using SQLite;
string filename = Path.Combine(FileSystem.AppDataDirectory, "my-sqlite.db");
SQLiteConnection connection = new SQLiteConnection(filename);
```

### SQLite Create a Table

Define a C Sharp Class and use `CreateTable` on the `SQLiteConnection` class to generate a table.

```C#
[Table("myData")]
public class MyData
{
  // PK is usually numeric
  [PrimaryKey, AutoIncrement, Column("_id")]
  public int Id { get; set; }

  [MaxLength(100), Unique]
  public int bibNumber { get; set; }

  // more class-code...
}
```

Table Attributes:

- Table: Needs a name. Default is the name of the Class.
- PrimaryKey: Column must be specified.
- AutoIncrement: Boolean. If true, increases column value when new row is inserted.
- Column: Needs a Name. Default is the Class Property for which it represents.
- MaxLength: Max number of _characters_ that can be used in the column.
- Unique: Boolean. Enforces uniqueness at the Table level.

Create the table:

```C#
connection.CreateTable<MyData>();
```

_Note_: If table exists and schema is different, `CreateTable<T>()` attempts to update the schema to the properties of Type 'T'.

### SQLite Read and Write Operations

Insert:

- Provide an object.
- Must be properly typed.
- Data is inserted.

```C#
public int AddNewBib(Bib bib)
{
  // todo: verify bib is not null?
  int result = connection.Insert(bib);
  // returns the number of row(s) that were updated
  return result;
}
```

Read _All_ Rows in a Table:

- Use the `Table` method.
- Returns a Collection of objects.
- Collection _could be empty_.

```C#
public List<Bibs> GetAllBibs()
{
  List<Bib> bibs = connection.Table<Bib>.ToList();
  return bibs;
}
```

### SQLite Queries Using LINQ

Selecting data within a table can be done using LINQ queries. Supports:

- Where
- Take
- Skip
- OrderBy
- OrderByDescending
- ThenBy
- ElementAt
- First
- FirstOrDefault
- ThenByDescending
- Count

Use _extension method syntax_ to extend the LINQ query to a fully functional query:

```C#
public List<Bib> GetByAction(string action)
{
  var bibs = from b in connection.Table<Bib>()
             where b.Action == action
             select b;
  return bibs.ToList();
}
```

### SQLite Update and Delete

Use the `SQLiteConnection` object.

The `Update()` method updates a single record in a Table:

- Returns the number of row(s) changed (should be 1 right?).
- Accepts a plain-old C# Class/Object.

```C#
public int UpdateItem(Item item)
{
  int result = 0;
  result = connection.Update(item);
  return result;
}
```

The `Delete(key)` method removes row(s) from a Table:

- Requires the primary key of the item in teh Table.
- Method is generic, requiring a Type parameter.
- Returns the number of row(s) affected.

```C#
public int DeleteItem(int itemID)
{
  int result = 0;
  result = connection.Delete<Item>(itemID);
  return result;
}
```

### SQLite Asynchronous Operation

Use Async operations to ensure the UI remains responsive to the user.

Asynchronous features execute queries on a separate thread, not the UI thread.

All operations are Task-based to support background usage:

- Async API via `SQLiteAsyncConnection` class: `var connection = new SQLiteAsyncConnection(databasePath);`.
- Create Table asynchronously: `await connection.CreateTableAsync<Item>();`.
- `DropTableAsync(class)`: Drop Table, by correlated Class.
- `GetAsync(primaryKey)`: Gets record in table based on class, matching PK.
- `InsertAsync(newItem)`: Insert new record.
- `UpdateAsync(updatedItem)`: Updates existing record.
- `DeleteAsync(primaryKey)`: Remove record that matches table, PK.
- `QueryAsync()`: Direct SQL query and returns an object.
- `ExecuteAsync()`: Direct SQL query returns count of affected rows.
- `ExecuteScalarAsync()`: Direct SQL query returns _single result_.
- `ToListAsync()`: Converts Table Query result to a `List<T>` type.

## Android Emulator

Requirements:

1. Reboot, enter UEFI/BIOS and Enable Trusted Execution Environment, save and exit.
2. Add the Hyper-V Windows Feature (Apps -> Add Feature), reboot the computer.
3. Load the Android Device Manager and click Start on the Device to start.
4. Once booted, click Debug (Android phone model and API Level) to load the app into the Emulator.
5. Stuff works instead of crashing or opening message box warnings.

## About Tizen

Tizen is an open-source Linux distribution that supports IoT, TV, Mobile, and Wearable device profiles.

Tizen supports headed and headless products.

Driven by [The Linux Foundation](https://www.linuxfoundation.org/)

[Tizen Org](https://www.tizen.org/)

Question: Does this mean .NET MAUI can target Linux devices like RPi or full x86/AMD architectures?

## Resources and References

[Learn.Microsoft.com](https://learn.microsoft.com/en-us/training/modules/create-user-interface-xaml)

Code segments copied from various Modules at [Microsoft Learn](https://learn.microsoft.com/en-us/training/)

[File System Helpers](https://learn.microsoft.com/en-us/dotnet/maui/platform-integration/storage/file-system-helpers?tabs=windows)

[SQLite](https://github.com/praeclarum/sqlite-net) project home

[SQLite Wiki](https://github.com/praeclarum/sqlite-net/wiki/Getting-Started)

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root README](../README.html)
