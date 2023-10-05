# DotNET MAUI Learnings Log

This markdown file exists to capture additional learnings about .NET MAUI.

For starters, notes will be made while following MSFT Learn modules.

## Table of Contents

- [Build Mobile and Desktop Apps Training Notes](#build-mobile-and-desktop-apps-training-notes)
- [Create a UI in a DotNET MAUI App By Using XAML](#create-a-ui-in-a-dotnet-maui-app-by-using-xaml)
- [Customize XAML Pages Layout](#customize-xaml-pages-layout)
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

#### New Dot Nets

These come with .NET MAUI:

- .NET for Android
- .NET for iOS
- .NET for mac
- WinUI

_Note_: WinUI3 is provided by the Mono project.

#### DotNET BCL 6

The new Dot Net Libraries sit on top of BCL.

BCL sits on top of Mono Runtime and WinRT runtime.

#### Mono and WinRT

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

### MAUI Install Requirements

Visual Studio 2022 v17.3 or newer and '.NET MAUI Multi-platform App UI Development' workload.

_Note_: There is a preview version of Visual Studio that supports MAUI development on Mac.

### Creating a MAUI App

Three Project Templates are available with .NET MAUI:

- .NET MAUI App
- .NET MAUI Blazor
- .NET MAUI Class Library

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

#### Controls and Layouts

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

#### Modifying Control Properties

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

### Project File Noteworthy Elements

Initial `PropertyGroup` specifies platform frameworks to target, app title, AppID, version, display, and supported OSes. These can be ammended as needed.

`ItemGroup` following that allows specifying image and color for splash screen (app loading visual). Set default locations for fonts, images, and other assets used by the app. See `Resources Folder` for storing the actual items referenced. These should be REGISTERED using `MauiApp.CreateBuilder()` in `MauiProgram.cs`.

### Debug Mode

### Android MAUI App

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
- XAML is based on MSFT 2009 XAML spec, but is _only sytactical_ specifications.
- WPF, UWP, WinUI 3 all use XAML and elements will change.
- .NET MAUI changes some of the Class names and Properties (from WPF et al).
- XAML can generate a simple login page in fewer lines than using C# to do the same (although code-behind will add to the count in most instances).
- `InitializeComponent` is _not_ necessary if XAML is not used to define a page layout and controls.

Most importantly: Separate the definition o fthe UI from teh logic of the app.

### Types and Properties

XAML Parser takes XAML and creates objects given the elements with set properties from teh XAML definitions.

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

Example provided by MSFT Learn:

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

Example provided by MSFT Learn:

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

Simplify by using a Default Value for any non-match (example provided by MSFT Learn):

```XML
<VerticalStackLayout Padding="{OnPlatform iOS='30,60,30,30', Default='30'}">
  <!-- XAML for other controls go here -->
</VerticalStackLayout>
```

## Customize XAML Pages Layout

Specify View Size:

- Various devices have varying default view sizes and pixel ensities.
- Mobile, tablet, phone, desktop, wearable, etc.
  -Layout Panels build consistens UIs, controlling sizing and positioning of child controls.

### Layout Panel

- Hold collections of child views (Controls).
- Determines size and position.
- Recalculation of position and size are automatic.
- Support device rotation.
- Stack, Absolute, Grid, and Flex Layout Panels are available.
- StackLayout: Single row or column.
- VerticalStackLayout, HorizontalStackLayout: Columnar or horizontal alignment, respectively.
- AbsoluteLayout: Utilizes x,y coordinates to place child Controls.
- FlexLayout: Enables wrapping child Controls if they don't fit into a single row or column.
- Grid: Child Controls are placed within identified row or column IDs, and can be told to stay within that 'cell', or to span cells (rows or columns).

_Note_: RelativeLayout is similar to FlexLayout, but _FlexLayout should be used due to better performance_.

### View Size Configuration

Affects how the parent element sizes itself around its content.

Un-set: Element will auto-grow to be large enough to fit around its content.
Set: WidthRequest and/or HeightRequest attribute(s) are configured on the element.

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

[Learn.Microsoft.com](https://learn.microosft.com/en-us/training/modules/create-user-interface-xaml)

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root README](../README.html)
