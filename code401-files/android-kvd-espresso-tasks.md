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

### Overview

Write concise Android UI tests.

```java
@Test
public void testName() {
  onView(withId($viewIdentifier)).perform($action($param[s]))
  onView(with($param[s])).check($assertion($assertedStatus()))
}
// $VARs are used to placehold actual commands
```

Calling 'onView()' waits synchronously:

- Message queue is empty
- No AsyncTask tasks running
- Idling Resources are idle

These ensure a single UI action will happen at any given time.

#### Packages

View matchers, actions and assertions: 'espresso-core'

Resoruces for 'WebView' support: 'espresso-web'

Synchronizing background jobs: 'espresso-idling-resource'

External contribs: 'espresso-contrib'

Validates sub intents (for hermetic testing): 'espresso-intents'

Where multi-process functionality is found: 'espresso-remote'

## Create UI Tests with Espresso Test Recorder

1. Turn off animations on test device.
1. Note: Do NOT manually set a dependency reference to Espresso Library (it is automatically done for you).
1. Record UI + Assertion interactions: Run > Record Espresso Test; Select Deployment Target: yourDevice; OK => Triggers build, install, and launch, then tests are executed.
1. Interact with the device in the "Record Your Test" window to start recording the test.
1. A list of actions will be recorded. Add Assertions to check: 'text is', 'exists', 'does not exist'. Save Assertions after configuring each one.
1. Click 'Complete Recording' when done, then name the test and Save it.
1. The Test Class file opens in the Project Window of the IDE.

*Note*: Instructation Test root determines where the tests are saved, and it will be in the 'src/*test' directory structure of your project.

### Run Espresso Test Locally

1. Open App Module Folder.
1. Nav to test to run.
1. rClick the test and select "Run 'testName'".
1. Choose your test device in 'Select Deployment Target' window (Create a new one if necessary).

### Run Espresso Test in Firebase Test Lab for Android

Free application with limited quota.

1. Create a FireBase project.
1. Follow steps to run Tests using Firebase Test Lab (in Android Studio).

Check out Firebase Test Lab => [Real Hardware Environments for Testing Your Android and iOS App](https://firebase.google.com/docs/test-lab/)

## Tasks and the Back Stack

Task: Collection of user-interactive activities.

Back Stack: Arrangement of activities, LIFO storage.

### Lifecycle of Task in Back Stack

Activities are store in the Back Stack in LIFO order:

1. Device HomeScreen.
1. App Alpha is launched (now foreground).
1. App Bravo is launched from App Alpha (now foreground).
1. User Nav 'back' so Bravo is popped/destroyed and Alpha is foregrounded.

Once all Activities are popped off the stack, the TASK no longer exists.

### Back Nav Special Cases

Root Launcher Activity can either be destroyed or backgrounded depending on Android/API Version:

- 11 and lower: Activity is finished.
- 12 and higher:Activity is moved to background (same as when using Home button or gesture). App remains in 'warm state' for faster restart.

*Note*: Instead of overriding 'onBackPressed()', use AndroidX Activity APIs to handle special cases.

### Background and Foreground Tasks

When a new App launches, Activities associated with other Apps are put into Background Activity level.

The Home Button causes current foreground Activity Alpha to go into background and a new Task is started with its own Stack of Activities.

When the user returns to the 'warm state' App, the Activity Stack with all Activities still in tact, is restored.

*Note*: Retaining an Activities in a Background State for long periods, or with many other Apps running, increases the likelihood it will be destroyed to recover RAM.

Multi-Window Environments are allowed and the system manages Tasks (or groups of Tasks) on a per-window bases.

## Footer

Return to root [Readme](../README.html)
