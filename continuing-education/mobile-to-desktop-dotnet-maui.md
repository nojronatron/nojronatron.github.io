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

## References

MSReactor YouTube Channel for past [recordings](https://www.youtube.com/@MicrosoftReactor).

DotNET MAUI Cloud Skills [challenge](https://aka.ms/Summer.NETMAUI-CSC1).

SummerCoding Adventure Workshop [GitHub Repo](https://github.com/icebeam7/SummerCoding).

## Footer

Return to [Conted Index](./conted-index.html)
Return to [Root README](../README.html)
