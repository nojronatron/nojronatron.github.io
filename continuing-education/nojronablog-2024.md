# Nojronablog 2024

A space for collecting thoughts and technical walk-thrus and takeaways during my coding journey through CY 2024.

## Week 1

### MAUI Color and Theming

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

Theming In Particular:

- It seems like a good idea to leverage `AppThemeBinding`s everywhere once it is used somewhere on a View, otherwise there can be some unexpected results.
- Use `transparent` color type when necessary to allow the Theme application to a parent View/Control to show through.

Link-Like Label Styling:

The code I implemented for launching the browser and displaying a "link"-like Label are functional on Windows and Android (emulator API 32+).

_Note:_ [`IBrowser.OpenAsync()` documentation](https://learn.microsoft.com/en-us/dotnet/api/microsoft.maui.applicationmodel.ibrowser?view=net-maui-8.0) does not mention any Exception type that might get thrown.

Custom Images and Icons:

Miro is really helpful creating materials for images and icons. Some things to keep in mind when creating materials for .NET MAUI 8:

- Seems like FlyoutIcon must be black-and-white, or a Font or other Glyph.
- Sizing images for their intended use makes for less troubleshooting when adding and troubleshooting issues rendering images.
- Creating a DataTemplate to enable color-image rendering as an icon is a possibility, however `Shell.FlyoutIcon` doesn't seem to accept a `FlyoutItem` as an acceptable input.
- Images _must_ be named starting with a letter character, all characters lower-case, and numbers are acceptable _except_ for the 1st character in the filename.
- So long as Images are placed into the Resource hierarchy at `Project\Resources\Images\`, they will automatically be assiged the Build property `MauiImage`.
- When adding/removing images from a MAUI project it is a good idea to check the Project file for `<ItemGroup>` entries with both `include` and `remove` attributes. Clean-up the entries with `remove` attribute before the next build-deploy cycle to avoid some possible deployment errors.

### Publishing a Private Android APK using Visual Studio

So many times I've done this and yet the process is just un-obvious enough that I stumble through it pretty much everytime. The goal here is to document it so that I no longer need to look it up. :smiley:

1. Build the MAUI App using `Rebuild` on the Solution.
2. Select the Android emulator and run the app, confirming there are no errors then close the app.
3. Select the target emulator for Android in the Debug configuration.
4. Select `Release` in the Solution Configuration.
5. Select `Publish` on the Project to deploy. If there is already a Publish Configuration, a build cycle will execute, otherwise the configuration must be set first.
6. When the Archive Manager is done creating and packaging the APK, look at the bottom of the screen for `Distribute...` and click it to open the 'Distribute - Select Channel' window.
7. Click `Ad Hoc`.
8. Add a Signing Authority (have a secure password ready), or select an existing one.
9. Click `Save As` to save the APK. _Note_: If there is already in an APK in that folder _be certain to overwrite it_ otherwise the new deployment will not complete successfully.
10. Confirm `Overwrite file?` and then enter the secure password.
11. When that process completes, review the screen for any errors or problems.
12. If there were no problems, click `Open Distribution` at the bottom of the Archive Manager window to gain access to an APK file that can be side-loaded onto an appropriate Android API Level phone.

Note: Select `Open Folder` to see the signed-apks folder, archive.xml, and deployable APK file.

### Week 1 JavaScript Fun

Areas where I've been struggling with JavaScript recently: Arrow Functions!

- Creating a Function as if it were a class with its own members.
- When to use Arrow functions, anonymous functions, etc inside of a Class or Function-style class.

```javascript
// Functional "class"
const MyThing = function() {
  this.kvpStore = {};
  this.has = (key) => {
    return this.kvpStore.hasOwnProperty(key);
  };
}
```

I need to sort this out in my head so it is less frustrating next time:

- [ ] Why are we using `this.has = (param) => {}` here, instead of `this.has = function(param) {}`? The problem is they don't have their own meaning of `this`, resulting in unexpected results. So method definitions should _not_ use this syntax. Normal methods should be written using class 'method' syntax (see below). _[MDN JavaScript Reference]_

```javascript
// anonymous function
(function (num) {
  return num / 100; 
});

// basic arrow function removes keyword 'function' and parens and braces not necessary for one-line code block and single (simple) params
num => num / 100;

// braces and 'return' keyword required for multi-line code blocks
num => {
  const temp = num / 100;
  return temp + 100;
};
```

- Do _not_ return expression body syntax e.g. `const func = () => { foo: 'baz' };`
- Instead, wrap object literal in parenthesis: `const func = () => ({ foo: 'baz' });`
- Don't do this either `const func = () => { foo: function () {...} };`
- Don't return a function like this either: `const func = () => { foo() {...} };`
- There is no concept of `arguments` binding in arrow functions.
- Arrow functions lack a `prototype` property, and will throw an error when called with the `new` keyword. 

Note: The above examples are slightly modified versions from _[MDN Javascript Reference]_, accessed 5-Jan-24.

```javascript
// class method syntax example with public function definitions
const obj = {
  foo() {
    return 'bar';
  },
};

// the slightly longer form of the above:
const obj = {
  foo: function () {
    return 'bar';
  },
};
```

- MDN Reference Material about [Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions).
- MDN Reference Material about [Class Method Definitions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Method_definitions).

JavaScript Delete Operator

This is an odd one! Delete operator allows removing a property from an Object. Identify the object and property to perform the removal.

```JavaScript
var HashTable = function() {
  this.collection = {}; // a key-value pair storage i.e. [hashcode, value]
  this.remove = (key) => {
    delete this.collection[key];
  }
  // add, has, and other functions...
}
```

## Footer

Return to [Root README](../README.html)