# DotNET MAUI Handlers and Native Controls

## Table of Contents

- [Presenters](#presenters)
- [Overview](#overview)
- [Xamarin FOrms Custom Renderers](#xamarin-forms-custom-renderers)
- [Steps](#steps)
- [References](#references)
- [Footer](#footer)

## Presenters

- Bruno Capuano @elbruno
- Luis Beltran, MSFT MVP, @darkicebeam, [GitHub](https://github.com/icebeam7)

## Overview

There are optimizations make to MAUI Handlers Native Controls. This presentation aims to go over these details.

## Xamarin FOrms Custom Renderers

- Used to implement 'native controls'.
- Native Controls are those provided by the target platform the app/service will run on top of.
- Xamarin.Forms.Map branches Controls to Mac, Android, and Windows platforms.
- Some Map controls _are not available_ in all platforms.

### Map Renderer

Responsible for rendering Map Controls in the platform UI.

Intermediate layer for each platform manage the hand-off:

- Xamarin.Forms.Maps.iOS -> MKMapView
- Xamarin Forms.Maps.Android -> MapView
- Xamarin.Forms.Platform.UWP -> MapControl

### Architecture Problems in Xamarin.Forms

- Renderes are tightly coupled to Xamarin.Forms components.
- Assembly Scanning is slow.
- Difficult to reach native platform from cross-platform one.

Reference Material: 'MonkeyFest - .NET MAUI Handlers Presentation' from Javier Suarez Ruiz.

### Motivation for New Implementation

- Performance: IoC, avoiding assembly scanners and reflection, layout improvements, and handlers that are "fast renderers"
- API: Allow more possibilities to utilize in a simple way on each platform.
- Homogeneity: Separate APIs behave differently by platform.
- Simplfy: Project structure; Handler vs Renderer

### New Implenetation in MAUI Handlers

Example was:

```text
Button: Mocroosft.Maui.Controls
^
|
IButton: Microsoft.Maui
|||
vvv
Button Handler (Microsoft.Maui.Handlers) ButtonHandler (Microsoft.Maui.Handlers)  ButtonHandler (Microsoft.Maui.Handlers)
IOS UIButton (UIKit) MacOS NSButton (AppKit) Android AppCompatButton (AndoirdX...) Windows Button (Windows.UI.Xaml.Controls)
```

"Handlers are in charge of applying requests in the MAUI platform to the native controls." _[Luis Beltran]_

- VirtualView (was Element): Cross-platfrom definition of visual component.
- PlatformView (was Control): Native control.
- Mapper: Map of properties and actions, to native implementations.
- Handler: Handle changes to VirtualView and applies natvie deployment, e.g. 'OnElementPropertyChanged' method of Custom Renderers.
- CreatePlatformView: Creates teh native control instance.
- ConnectHandler: Initializes the native control.
- DisconnectHandler: Used to free resources, controllers, delegates, memory, controls, and other elements.

## Steps

1. Create new class for cross-platform control.
2. Inherit from View for a new control, or from a specific component to extend (Entry, Button, Image, etc).
3. (Luis went on a long code-review at this point)...
   Create native implemntation using same class name (e.g. Viewhandler partial class) within the same namespace.
4. (More code review and explanation)...

_Tip_: Create an interface tha timplements IView, then make your class implement that interface.

_Also_: Create public static readonly BindableProperty MyPropertyName... to define the Property Control (this will make more sense by reading the [DotNET MAUI BindableProperty documentation](https://learn.microsoft.com/en-us/dotnet/maui/fundamentals/bindable-properties)).

## References

[Previous Event Recordings in this series](https://developer.microsoft.com/en-us/reactor/series/S-1171/)

Microsoft Learn [Install .NET MAUI](https://learn.microsoft.com/en-us/dotnet/maui/get-started/installation?tabs=vswin) for development.

Microsoft Learn [Create a .NET MAUI app](https://learn.microsoft.com/en-us/dotnet/maui/tutorials/notes-app/).

GitHub [.NET MAUI Public Repository](https://github.com/dotnet/maui).

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
