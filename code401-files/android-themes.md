# Applying Styles and Themes to an Android App

## Resources

Android Developer [Styles and Themes](https://developer.android.com/guide/topics/ui/look-and-feel/themes)

Android Styles and Themes from [Medium.com](https://medium.com/androiddevelopers/android-styling-themes-vs-styles-ebe05f917578)

## Overview

Separate details of app design from UI structure and behavior.

Think web stylesheets.

Style: Collection of attributes for a single View => font color, font size, background color, etc.

Theme: Collection of attributes applied to:

- Entire App
- Activity
- View Hierarchy

Status Bar and Window background are "non-view elements" and Themes *can apply* to those.

## Themes vs Styles

### Styles

Can apply to specified items like Buttons.

Are lists can be set in the Layout file.

Extract all attributes from Style to use them across multiple widgets.

### Themes

Defines a collection of named resoures that can be referenced by Styles, Layouts, Widgets, etc.

Themes apply semantic names to Android resources.

Semantic names e.g. "colorPrimary".

### Both

Styles and Themes meant to work together.

Style definitions are within the Theme.

Themes can be switched e.g. "Night Mode" theme vs "light" theme.

Themes use same semantic style names, so light/dark switching does *not* require changing values in resource names.

### Create and Apply a Style

To create a style, follow these steps, repeat for each style to create:

1. edit `res/vlues/styles.xml`
1. add `<item>` element for each style attribute to define
1. `name` in each item specifies an attribute name; `value` in each item specifies the value to apply to that attribute
1. use `parent=` to identify the parent element for the style name to *extend* (see below)

Apply a style to a View:

```xml
<TextView style="@style/GreenText" ...>
```

*Note*: A View might not accept a style and will ignore the attribute.

#### Extend Existing Styles

Always better to extend from the framework or support library to maintain compatibility.

To extend a style:

1. Specify style to extend using `parent=...`
1. Override style attributes or Add new ones

```xml
<style name="Foo" parent="@android:style/TextAppearance">
  <item name="android:textColor">#0FA12E</item>
</style>
```

Styles in the Android Support Library: Compatibility with API 14 and higher.

`AppCompat` is used to indicate Android Support Library implementation for API 14 through (current), which apply to Elements with *similar* names through the version history.

To inherit from a Library or your own project, do *not* use `@android:style/` prefix to element names.

```xml
<style name="Foo" parent="TextAppearance.AppCompat">
  <item name="android:textdColor">#0F1E2D</item>
</style>
```

Inherit styles by exsting style's existing name and use dot notation instead of parent attribute.

Prefix name of style to inherit, add a dot, then append the name of your custom style.

*Note*: Only do it this way when *extending your own styles* and not from other Libraries.

Increase text size:

```xml
<style name="Foo.Large">
  <item name="android:textSize">20dp</item>
</style>
```

Inherit (through chaining) to create more.

Using `parent` attribute will *override chained custom styles*.

## Apply Style as a Theme

Similar to creating Styles.

Apply a theme with `android:thme` attribute.

Apply theme attribute to `<application>` or `<activity>` tag in `AndroidManifest.xml`.

```xml
<manifest ...>
  <application android:theme="@style/Theme.AppCompat" ...>
  </application>
</manifest>
```

Apply a "light" theme to a single Activity:

```xml
<manifest ...>
  <application ...>
    <activity android:theme="@style/Theme.AppCompat.Light" ...>
    </activity>
  </application>
</manifest>
```



## Footer

Back to [Root README](../README.html)
