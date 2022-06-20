# Read Class 27 Notes

## References

All these reading resources are available on Android Developers website.

[Save Key-Value Data](https://developer.android.com/training/data-storage/shared-preferences)

[Espresso Guide](https://developer.android.com/training/testing/espresso)

[Create UI Tests with Espresso Test Recorder](https://developer.android.com/studio/test/other-testing-tools/espresso-test-recorder)

[Tasks and the Back Stack](https://developer.android.com/guide/components/activities/tasks-and-back-stack)

## Save Key Value Data

SharedPreferences APIs: Good for persisting small collections of data.

SharedPreferences adds methods to use against storage file with the collection's KVPs.

SharedPreferences can be private or shared.

Should *not* be used to store system or user Preferences (there are other APIs for these).

### Get a Handle to Shared Preferences

Create new file or access existing one with either:

- 'getSharedPreferences(filename)' gets content in filename parameter, from any App Context.
- 'getPreferences()' should be called from an Activity if KVPs are needed for that Activity. No filename needed.

Good practice to name files with your 'application ID' e.g.: `com.example.myapp.PREFERENCE_<file-key>`

*Note*: Use a 'FileProvider' with 'FLAG_GRANT_READ_URI_PERMISSION' to share private files with other apps.

Use 'geDefaultSharedPreferences()' to get default shared pres file for your *App*.

### Write to Shared Preferences

Edit shared preferences using either:

- SharedPreferences.edit() returns a SharedPreferences.Editor
- EncyptedSharedPreferences.edit() securely returns a SharedPreferences.Editor

An example of something to store in a SharedPreferences file was a high score in a game.

File saves:

- Asynchronous using the 'apply()' method.
- Synchronous (immediate) when using 'commit()' method but it can pause the thread it is on so avoid using on main thread.

### Read from Shared Preferences

Call these methods, providing the KEY of the value you want:

- 'getInt()'
- 'getString()'

A 'default value' can be supplied (and returned) if no KEY exists.

## Espresso Guide

*Go over at least*: Overview, Basics, and Recipes.

## Create UI Tests with Espresso Test Recorder

## Tasks and the Back Stack

## Footer

Return to root [Readme](../README.html)
