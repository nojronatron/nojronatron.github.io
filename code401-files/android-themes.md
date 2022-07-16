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

## Footer

Back to [Root README](../README.html)
