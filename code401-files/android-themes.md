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

If a view supports only some of the attributes declared in the style only those are applied.

### Apply Different Theme to Specific Activity

To modify theme for *specific view and its child views* at API Level 21 through v22.1: Specify `android:theme` attribute to view in Layout file.

## Style Hierarchy

Ways to set attributes:

- Directly in a layout
- Apply style to a View
- Apply Theme to a Layout
- Set attributes *programatically*

Advice:

- Use themes and styles as much as possible for consistency
- Attributes specified in multiple places may not show, depending on on hierarchical precedence

Hierarchical Precedence:

1. Apply character- or paragraph-level styling via text spans to `TextView`-derived classes
1. Applying attributes programmatically
1. Applying individual attributes directly to a View
1. Applying a style to a View
1. Default styling
1. Applying a theme to a collection of Views, an activity, or your entire app
1. Applying certain View-specific styling, such as setting a `TextAppearance` on a `TextView`

For example:

- Applying attributes programmatically overrides style applied to a View
- Applying individual attributes directly to a view overrides default and theme-based stylings

## Limitations and TextAppearance

A View can have but one single style applied to it.

`TextAppearance` attribute act similarly to Style

```xml
<TextView
  ...
  android:textAppearance="@android:style/TextAppearance.Material.Headline"
  android:text="Foo Bar!" />
```

Using `TextAppearance` leaves a View's *style* available for use.

Applying text attributes *directly* to  the View (or via a Style) the `TextAppearance` values will be overridden.

THere are subsets of styling attributes offered through `TextView`. See [TextAppearance](https://developer.android.com/guide/topics/ui/look-and-feel/themes#textappearance) subsection for details.

## Customize the Default Theme

Material design theme is apply to App by default upon project creation.

Material design theme is defined in `styles.xml` file.

Material design theme extends a suport library theme and overrides `appbar` and `floating action button` elements.

Color Resources are found in the project's `res/values/colors.xml` file.

Use the `Material Color Tool` to preview colors prior to applying them.

After previesing the colors, update values in `res/cavlues/colors.xml`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <!--   color for the app bar and other primary UI elements -->
    <color name="colorPrimary">#3F51B5</color>

    <!--   a darker variant of the primary color, used for
           the status bar (on Android 5.0+) and contextual app bars -->
    <color name="colorPrimaryDark">#303F9F</color>

    <!--   a secondary color for controls like checkboxes and text fields -->
    <color name="colorAccent">#FF4081</color>
</resources>
```

Once this is updated, override whatever other styles needed.

```xml
<style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
    ...
    <item name="android:windowBackground">@color/activityBackground</item>
</style>
```

Look at [R.styleable](https://developer.android.com/reference/android/R.styleable#Theme) theme table for a lookup of standard attributes that make up a complete theme.

*Remember*: All Views support *XML attributes from the base `View` class*.

### Add Version Specific Styles

This is possible by adding another `styles.xml` file in the `values` directory that includes the resource version qualifier:

`res/values/styles.xml`: Themes for all versions
`res/values-v21/styles.xml`: Themes for API level 21+ only

Themes in `values-v21/styles.xml` can inherit from `values/styles.xml` extending the base theme and adding version-specific styles.

See the subsection [Add Version Specific Styles](https://developer.android.com/guide/topics/ui/look-and-feel/themes#Versions).

### Customize Widget Styles

Button is an example of a Widget.

`Widget.AppCompat.Button` is how it can be styled.

Apply a 'Borderless" style to all Button widgets:

```xml
<style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
  <item name="buttonsStyle">@style/Widget.AppCompat.Button.Borderless</item>
  ...
</style>
```

## Start An Activity With An Animation

This animates the transition between Views.

Transitions:

- enter: Determins how views in an activity enter the scene. Explode transitions from the outside inward.
- exit: How view in an activity exit the scene. Explode transitions from the center outward.
- shared elements: How views shared between activities transition. Translates and scales the image smoothly between activities.

Enter and Exit Transitions:

- Explode: Move view in/out from center of the scene.
- Slide: Move views int/out from edges of the scene.
- Fade: Add/Remove View from the scene by changing opacity.

Transitions that support `Visibility` class can be used as enter or exit transitions.

Transition class [API](https://developer.android.com/reference/android/transition/Transition)

Shared Element Transitions:

- changeBounds: Animates changes in layout bounds of target views.
- changeClipBounds: Animate changes in clip bounds of target views.
- changeTransform: Animates changes in scale and rotation of target views.
- changeImageTransform: Animates changes in size and scale of target images.

### Check System Version

Requires Android 5.0 or higher.

```java
// Check if we're running on Android 5.0 or higher
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) {
    // Apply activity transition
} else {
    // Swap without transition
}
```

### Custom Transitions

1. Enable window content transitions with `android:windowActivityTransitions` attribute when defining a style that inherits from 'material theme'.
1. Specify enter or exit or shared element transitions in style definition.

See sample code in [Specify Custom Transitions](https://developer.android.com/training/transitions/start-activity#custom-trans) sub-section.

### Start An Activity With Transitions

This is covered in [Start An Activity Using Transitions](https://developer.android.com/training/transitions/start-activity#start-transition) sub-section.

## Footer

Back to [Root README](../README.html)
