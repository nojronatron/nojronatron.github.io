# Nojronablog 2024

A space for collecting thoughts and technical walk-thrus and takeaways during my coding journey in 2024.

## Week 1

Working through implementing a usable About page for MobWxApp:

- Implementing a "Hyperlink" Style for things like opening the GitHub Project or LinkedIn Profile in a browser is fairly straightforword so long as you _do not_ use `<span>`s.
- The problem implementation is documented at [.NET MAUI UI Controls: Label - Create a Hyperlink](https://learn.microsoft.com/en-us/dotnet/maui/user-interface/controls/label?view=net-maui-8.0#create-a-hyperlink), however it does not work as described.
- MAUI Project GitHub [Issue 14410](https://github.com/dotnet/maui/pull/14410) for an overview of the issue. There are similar issues linked, and the bug-fix schedule seems to get pushed-back quite often.
- The core of the problem seems to be use of `<span>` elements, and can be worked around by using `<Label>` instead. Below is an example of the problem XAML and the work-around XAML.
- A secondary issue is the use of the `Launcher` class, instead of an IBrowser implementation (see C# code, below).

```xml
<!-- from .NET MAUI 8 documentation at learn.microsoft.com -->
<Label>
    <Label.FormattedText>
        <FormattedString>
            <Span Text="Alternatively, click " />
            <Span Text="here"
                  TextColor="Blue"
                  TextDecorations="Underline">
                <Span.GestureRecognizers>
                    <TapGestureRecognizer Command="{Binding TapCommand}"
                                          CommandParameter="https://learn.microsoft.com/dotnet/maui/" />
                </Span.GestureRecognizers>
            </Span>
            <Span Text=" to view .NET MAUI documentation." />
        </FormattedString>
    </Label.FormattedText>
</Label>
```

```xaml
<!-- Avoid using SPAN elements -->
<Label Text=".NET MAUI Project Documentation"
       TextColor="DarkBlue"
       TextDecorations="Underline"
       VerticalAlignment="Center"
       >
  <Label.GestureRecognizers>
    <TapGestureRecognizer Command="{Binding TapCommand}"
                          CommandParameter="https://learn.microsoft.com/dotnet/maui/" />
  </Label.GestureRecognizers>
</Label>
```

The problematic C# Code uses `Launcher.OpenAsync(uri)` to navigate to a page:

```c#
using System.Windows.Input;
public partial class MainPage : ContentPage
{
    // Launcher.OpenAsync is provided by Essentials.
    public ICommand TapCommand => new Command<string>(async (url) => await Launcher.OpenAsync(url));
    public MainPage()
    {
        InitializeComponent();
        BindingContext = this;
    }
}
```

...what is really necessary for an external hyperlink is a Browser method to call the uri using the 'System Preferred' web browser:

```c#
// note: this could be done using ICommand but my implementation uses 
// the MVVM CommunityToolkit so I went with IAsyncRelayCommand instead
public partial class Mainpage : ContentPage
{
  public IAsyncRelayCommand<string> TapCommand => 
    new AsyncRelayCommand<string>(
        async (url) => await BrowserOpen(url)
        );
}
...
private async Task BrowserOpen(string url) {
  // check for null/whitespace string and open a try-catch block, then:
  try 
  {
    Uri uri = new Uri(url);
    bool result = await Browser.Default.OpenAsync(uri, BrowserLaunchMode.SystemPreferred);
  }
  catch (Exception ex)
  {
    // handle, notify, etc
  }
}
```

The code I implemented for launching the browser and displaying a "link"-like Label are functional on Windows and Android (emulator API 32+).

_Note:_ [`IBrowser.OpenAsync()` documentation](https://learn.microsoft.com/en-us/dotnet/api/microsoft.maui.applicationmodel.ibrowser?view=net-maui-8.0) does not mention any Exception type that might get thrown.

## Footer

Return to [Root README](../README.html)
