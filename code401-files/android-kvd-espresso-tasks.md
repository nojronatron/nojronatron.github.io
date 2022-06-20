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

Activities are stored in the Back Stack in LIFO order:

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

Changing Activities from LIFO to a custom reactivation or start-of-activity is possible:

- The `<activity>` manifest element with flags in the Intent to pass`startActivity()`

Activity element attributes:

- 'taskAffinity'
- 'launchMode'
- 'allowTaskReparenting'
- 'clearTaskOnLaunch'
- 'alwaysRetainTaskState'
- 'finishOnTaskLaunch'

Principal Intent Flags:

- FLAG_ACTIVITY_NEW_TASK: Start Activity in new Task.
- FLAG_ACTIVITY_CLEAR_TOP: Don't create a new Activity instance if current is at top of the Back Stack.
- FLAG_ACTIVITY_SINGLE_TOP: Destroy all other Activities on top, bringing this one to the top. Often used with FLAG_ACTIVITY_NEW_TASK to locate Activity and put in place where it can be leveraged/used.

*Note*: For the most part, Activity back-stack LIFO behavior should *not* be changed.

### Launch Modes

Use the Manifest file: Specify how Activity should associate with Tasks when it starts.

Use Intent Flags: Include in Intent that declares how/whether new Activity should associate with current task when calling 'startActivity()'.

A parent Activity that starts a child Activity has precedence over *how* the child Activity is associated with Tasks.

### Manifest File Launch Mode Keywords

Specify how Activity should associate with a Task via `launchMode` attrib in `<activity>` elements.

Launch Modes definable in `launchMode` attribute:

- standard: Default.
- singleTop: If 'TOP' then Intent routed through `onNewIntent()`, else new Activity is put on top of Back Stack.
- singleTask: (seems like it forces unique Activity affinities and could destroy existing Activities high in the Back Stack).
- singleInstance: Same as singleTask BUT no Activities are launched into the Task. Any Activities this one opens are done in a spearate task.
- singleInstancePerTask: Activity must be root Activity of the Task, so can be the only one. Multiple instances can be launched using various Flags.

### Define Launch Modes Using Intent Flags

Doing this modifies default association on an Activity to its Task.

See the section [Background and Foreground Tasks](#background-and-foreground-tasks) above for the Intent Flags to use.

### Handle Affinities

An *affinity* is synonymous with preference or owned-by.

Activities started by same App have affinity to each other.

Affinity can be changed for an Activity in element `<activity>` by using `taskAffinity(String)` attribute.

Affinities are set and altered by either of the following:

- FLAG_ACTIVITY_NEW_TASK
- Set attribute `allowTaskReparenting` to true

Use `taskAffinity(String)` to be sure a multi-App APK assigns the affinity in a logical way for your package.

### Clear the Back Stack

This is an automated process and all Tasks can be cleared except the Root Activity (assumes User abandonment).

Set attributes to alter the default behavior:

- `alwaysRetainTaskState`: True in root Activity to block default behavior.
- `clearTaskOnLaunch`: True clears down to the Root Activity when Task is NAV'd away then user returns to it, forcing initial state upon user return.
- `finishOnTaskLaunch`: Focused on single Activity (not entire Task), and causes Activity to finish (except Root Activity) when set to true. User NAV'd away then return, the Task is no longer present => disallows user to return to the launched Task.

### Start a Task

Use Intent Filter `android.intent.action.MAIN` to specify an entry point for a task, and include `android.intent.category.LAUNCHER` as the Category specification.

## Footer

Return to root [Readme](../README.html)
