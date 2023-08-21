# WPF MVVM Learnings

A collection of notes related to developing and building upon MVVM in DotNET WPF.

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

Add the following to `<ResourceDictionary>` in App.xaml:

```xml
<Application.Resources>
    <ResourceDictionary>
        <ResourceDictionary.MergedDictionaries>
            <ResourceDictionary>
                <local:Bootstrapper x:Key="Bootstrapper" />
            </ResourceDictionary>
        </ResourceDictionary.MergedDictionaries>
    </ResourceDictionary>
</Application.Resources>
```

## Random Notes

- Assembly name can be edited to cause the EXE to be named something other than the project name. See Project Properties to do this.
- WPF Tools for UI Debugging: Remove it by going to Tools -> Options -> Debugging -> General -> Enable UI Debugging Tools for XAML -> Uncheck "Show Runtime Tools in Application"

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
