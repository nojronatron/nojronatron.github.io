# MS Reactor From Mobile to Desktop DotNET MAUI

## Introduction

Luis Beltran @darkicebeam - Microsoft MVP

James Montemagno @JamesMontemagno and on YouTube, Program Manager at MSFT

Bruno Capuano @elbruno - 'not powered by AI'

## Overview

MSFT Learn has several paths that cover topics presented here.

DotNET MAUI was preceeded by Xamarin.

DotNET "Unified base for any operating system..." powering multiple devices and presentation types such as web, desktop, phone, console, and tablet.

Build apps from a single code-base.

- WinUI
- Mac Catalyst
- iOS
- Android

Flexibility:

- Blazor: Websites and PWAs.
- Device: Native controls and APIs.
- Hybrid: Both of the above.
- C# is common among the OS platforms.
- UI and resources are shared across platforms.
- Native-application build tools.

## New Project Demo Notes

MAC or VSCode or VS on Windows.

ToolBox will insert a new XAML element for a UI Control including newer DotNET MAUI items.

Accessibility elements are included e.g. Announcing Messages via screen reader.

Live Preview during Dev-Run time for UI changes, and "Hot Reload" capability for code-behind changes. :fire:

Android Emulators are available for Debug Time using "Native Compilation", allowing Breakpoints and live debugging.

Android App compilation tool enables deploying to GooglePlay and Amazon ecosystems.

Developing iOS Apps is possible:

1. Register for Apple Developer account.
2. Use a Mac and develop using Visual Studio for Mac.
3. Otherwise, in Visual Studio, use tools to develop and launch the app to your iPhone. Leashed with a USB cable, Live Preview is available.

Android and iPhone Emulators utilize theh native device capabilities such as Airplane Mode, and other features.

Multi-Window APIs are included!

## Hybrid Development

Bring native client capabiliies to tyour web apps.

Blazor is full stack web apps for server or browser, built on top of ASP.NET Core.

DotNET MAUI builds for client.

Blazor Hybrid allows running Blazor _within a DotNET MAUI Application_:

- Mix and match native UI.
- Enable front-end webapp development.
- Logic reuse of code.

Razor Files are files containing HTML and C-sharp together.

Blazor Web-view ends up being the parent display component within the DotNET MAUI build executable.

Native UI elements are utilized despite being a Blazor base-element format!

Example: Presenting a MessageBox is abstracted behind the scenes so the native UI Control is utilized for web, Android, or iOS platforms (whichever is needed at compilation).

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

- AppShell.xaml: MAUI Application main structure (styling, URI-based navigation, layout options, etc). Jon: Consider this the 'Root' view a-la React.
- App.xaml: Just like WPF, this is the default XAML Resource-defining file. Resource Dictionaries (and Merged Dictionaries) are supported, as in WPF.
- App.xaml.cs: Like WPF, defines the App Class, and initializes the Application. Common (platform neutral) lifecycle events can be overridden here (OnStart, OnResume, OnSleep...). Also, MainPage is initialized as a new AppShell.
- MainPage.xaml: The UI-defining code page. Controls View items and Controls like Stacks, Images, labels, etc.
- MainPage.xaml.cs: Define event handler logic triggered by the XAML-defined controls.
- MauiProgram.cs: Platform-specific code calls CreateMauiApp method which is leveraged when building for the specified platform. Register fonts, configure DI services and ncustom handlers for controls, etc.
- Resources Folder: Contains various resources such as Styles, Fonts, Images, etc.
- Platforms Folder: Platform-specific initialization code files and resources.

_Note_: `SemanticScreenReader` is a MAUI class with a static member `Announce(string)` that tells a screen reader what to say. Apply this to event handlers in code-behind.

### Project File Noteworthy Elements

Initial `PropertyGroup` specifies platform frameworks to target, app title, AppID, version, display, and supported OSes. These can be ammended as needed.

`ItemGroup` following that allows specifying image and color for splash screen (app loading visual). Set default locations for fonts, images, and other assets used by the app. See `Resources Folder` for storing the actual items referenced. These should be REGISTERED using `MauiApp.CreateBuilder()` in `MauiProgram.cs`.

### Debug Mode

### Android MAUI App

Tools -> Android -> Android Device Manager: Create a new phone (emulator) and API Level (Google API implementation version).

## About Tizen

Tizen is an open-source Linux distribution that supports IoT, TV, Mobile, and Wearable device profiles.

Tizen supports headed and headless products.

Driven by [The Linux Foundation](https://www.linuxfoundation.org/)

[Tizen Org](https://www.tizen.org/)

Question: Does this mean .NET MAUI can target Linux devices like RPi or full x86/AMD architectures?

## References

MSReactor YouTube Channel for past [recordings](https://www.youtube.com/@MicrosoftReactor).

DotNET MAUI Cloud Skills [challenge](https://aka.ms/Summer.NETMAUI-CSC1).

SummerCoding Adventure Workshop [GitHub Repo](https://github.com/icebeam7/SummerCoding).

## Footer

Return to [Conted Index](./conted-index.html)
Return to [Root README](../README.html)
