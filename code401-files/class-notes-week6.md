# Class Notes Taken During Week 6 Java 401

## Monday 20 June

Class canceled.

### Lab Class 26

Wants Style, Color, and Fonts.

See paper notepad for list of Font and Color pallette options.

## Summer Solstice

Class will be held, run by David Souther.

### Data Structures

Arrays, LinkedLists, Stacks, Queues, and Trees.

Use Linked Lists when editing data mostly near the end of a list.

Use a Tree when you want to keep things sorted => They will make it faster to locate data or determine if the tree contains the data at all.

#### Maps

They are KVPs.

The notion of a map is tied to Keys (things to consider when going into the map to find values) and Values (the value).

Bracket notation and dot-notation are examples of KVPs.

ArrayLists: Index is the key; Value at that index location is the... value.

Array constraints: Indexes will be zero-based and less than the total length of the array values count.

For Maps, we want to find the value quickly.

TreeMap: Maintains a backing "Tree" to help find data.

Invariance: "The rules" under which a datastructure operations.

Map Invariant Rules:

- Keys are unique
- Keys have meaning (not random)

TreeMap Invariants:

- Keys must be sortable (have an ordering)
- O(log(n)) algorithmic time

*Note*: TreeMaps can be slow unless the data is unsorted, and HashMaps are more common.

Hash Invariants:

- Uses a hash to calculate indices of the data.
- Uses an Array that *holds* the data.
- Arrays are fixed size.
- Keys could be *infinite*.
- Needs to take a key, turn it into an index to store in the array.

Hash Functions

- Uses a calculation to determine index of value that is being searched
- Transforming/converting types to make them calculable
- Should be an O(1) search function
- Hash takes O(k) => depends on the key length

Hash Collision

- Multiple keys map to the same index
- Pidgeonholing: 4 pidgeons, 3 coupes => will multiple pidgeons be in a single coup? Yes. If n > k then at least 1 k will have n > 1 items in it.
- To avoid this use an Array, Linked List, or Balanced Tree to add data instances to the index.
- Resizing is an option, but "book keeping" under the covers is a somewhat expensive operation.
- A collision *could be useful* so consider whether you want to detect collisions explicitly and whether it should be handled in some special way (example: Finding duplicate entries => maybe exit with a return type? Throw something? Record the incident and continue?).

Hash Index Implementations

- There could be several.
- One implementation has the constraint of "the key MUST have a hashCode() method" - thankfully Java's Object allows .getHash() is inherited to all children.

What Is A "Good Hash Code"?

- Meets constraints and doesn't break assumptions.
- Statistically guarantee that the index values will be unique.
- Use prime numbers to return the hash.
- Use a power-of-2 size array to store the data.

Scaling:

- Ensure the total number of 'buckets' is a prime number (or a power of 2).
- Multiply the hash value by a large prime number to consume the entire index space that is avaialble.

Where would HashMaps be implemented?

- Proxy or cache for a slower file system: Use filename as key.
- Discover basketball player's score statistics.

When should I think about using a Map?

- When the keys in a KVP are strings instead of numbers.
- When using data structures that are not a tree or some sort of in/out stack or queue.
- When interacting with, storing, and querying unstructured data.

Random Accessing map items (for add or update):

- Example: `int value = map.contains(key) ? map.get(key) : default_value;`
- contains method could be different syntax.

Assignment:

- Implement a hashtable
- Implement the basic API functions (get, set, contains, keys, and hash)
- Collisions must be handled in get and set (could be sloppy or nice e.g. rehashing etc)
- Optionally: Track size of the hashtable
- Returning collection of keys will require some tips/hints searching
- Optionally: Create an interface to force implementation
- Single Responsibility
- Write Tests
- Document
- Catch errors

### Key Takeaways

Big-O Analysis is not the be-all, end-all:

- Memory is limited, but you can always buy more.
- Memory fragmentation in large data sets will cast lots of processing time (large linked lists).
- Processing time is essentially linear (it's not 1987 anymore -David Souther).

Dealing with Data Structures you *must consdier bit/byte sizes of the data*:

- CharCode is an int
- Primative int is 4 bytes aka 32 bits
- ASCII char codes are 7 bits

Pigeonholing Algo:

- Ceiling(n/b) aka round-up result of (num_pigeons / num_coops)

## Weds Class Notes

### Android Development Overview

- Android Studio (IntelliJ for Android dev)
- WYSIWIG editor built-in

Bring-forward learnings from Code 301 e.g. React and Components.

### Intro To Android Studio

We are going to build "Task Master" project that will build upon for the remainder of this course.

Do lots of exercising with UI Constraints to experience how they impact the UI in the emulator.

There will be times you will need to CLI-kill the emulator: Find PID, use kill command. Emulator has the PID.

Event Listeners: `onClick()` etc. They do not handle everything for you, but will be used a lot for Android development.

Vocabulary:

- Emulator: Virtual device, not a replacement for a physical device but is a handy stand-in.
- Activities: Analogous to an MVC View, but more closely related to MVVM (Model-View-ViewModel). Data can be passed between Activities.
- MPA/SPA: Multi-page Application (Thymeleaf/MVC) and Single-page Application (React).
- Fragments: SPA uses these reusable blocks of code to dynamically render a page to a single Activity.
- Intents: Routes Between Activities.
- Extra: Transient storage that is bound to the lifecycle of an Activity (between onCreate and onDestroy?) and perhaps changed a lot.
- Component Tree: Lists the elements and UI components and their IDs within an Activity. Espresso Tests *heavily depend* on this.
- Espresso: Integration Testing.
- Content Provider: Stretch goal in a later lab, otherwise AWS technologies will be used in most cases.
- Shared Preferences: Survive App close and re-open.
- Parseable: Storage capability for more complex data (but still not large) e.g. Collections.

Wednesday:

- Add 3 Activities.
- Homepage: Match the wireframe. Color scheme and exact layout is up to you but simply get this 1st round to look like the Lab.
- Add a Task: 2 inputs and 1 button. NO DATA PROCESSING, just UI and Event Handlers.
- All Tasks: ??
- Stretch Goal: Style the app!
- MUST build an APK and TEST IT (emulator to install and open).

### Android Project

Package Names MUST BE UNIQUE, and must start capitalized.

Select an "Empty Activity".

API Level: Check out apilevels.com to see API Level utilization.

Level 24 is a good balance between features and coverage.

No legacy Android.Support files/libraries will be necessary.

OnCreate method: Just launches the current Activity.

Directory 'res/layout': Create new Activities in here.

Directory 'res/values': Contains XML files. 'strings.xml' is the most important one and will get quite large.

Directory 'res/values/themes': Overall App look and feel, including all Activities.

Directory 'manifests': AndroidManifest.xml defines where resources can be found including online APK, theme selector, icon seelctor, etc.

AndroidManifest also defines Activities and intent-filter actions and categories. These are largely auto-generated.

Tests: Uses AndroidJUnit4.

Unittests: Test your methods internally to validate your logic.

Android Tests: Interactivity of Views (did it display?) and Buttons (did it display? Was it clicked?).

Build.Gradle: There are 2 of them:

- build.grade (Module): Usually the one that will get updated, very similar to the one we've been using with our Java apps.
- build.gradle (Project): Plugins and Task Clean are only defaults in this top-level 'default' config file.

In the Module build.gradle:

- Update 'compileOptions' from '{ sourceCompatibility JavaVersion.VERSION_1.8 }' to '{ sourceCompatibility JavaVersion.VERSION_11 }'

MainActivity.java: Where Main app logic is implemented in code.

activity_main.xml is where the UI is defined.

Use DeviceManager to create or select existing devices. Be sure to match your configured API Level here too!

System Images must be downloaded locally in order to run an emulator for specific devices (takes time to D/L and intsall).

Layout Constraints: Determine an item that will be an "anchor" element, and then drag *constraints* from other items to it. There are other ways to go about it, but this method is fairly simple and effective.

Use IDs! Set the 'id' in camelCase so that the UI elements will be properly addressable. Use semantic id naming.

Chains: Use these to chain-together elements to enable various layout spacings, horizontal/vertical constraints, etc.

Constraint Layout: Make sure you *stay* in this layout type, for the duration of this class.

Text View: For *displaying* text.

All other Text Palette items besides Text View are *input type* elements.

RecyclerView: A List.

FragmentContainerView: Frags go in here.

ScrollView: More view available below/beside your view.

Switch: Utilize Boolean type to manage/receive these settings.

Containers: Various collection view and interactive elements. Spinner is an up/down spin-view of a collection of data.

Most of the work in these Labs will deal with the UI.

Lifecycle of Android App UI elements: onCreate, onDestroy, onStart, onStop.

These Activity Lifecycle items will be discussed in more detail during the week.

Android Developers Documentation has details on [Activity Lifecycles (diagram)](https://developer.android.com/reference/android/app/Activity#activity-lifecycle)

#### Event Listeners

Review: How to create and adding an Event Listener:

1. Get a UI element by ID.
1. Anonymous function call/event listener.
1. Callback function OnClick.
1. Do stuff witin the Callback function.

Create your own callback method in Java to handle events:

1. For this example we will be working within the onCreate() method.
1. Button submitButton = MainActivity.this.findViewById(R.id.) (location of the XML defining the UI we are working with)

#### Developing Activities

In this example:

1. Create a button and give it an appropriate ID and name.
1. Create a new Activity and name it, and set it to not auto-launch.
1. Add items to the new activity for create a new page with element constraints.
1. Open the new Activity java code and build modular code just like we've been doing up to now.
1. Update Main Activity, onCreate method, implement an Event Listener and Handler per instructions above.
1. Set the EventHandler method using 'setOnClickListener'

Use an Arrow Function e.g.:

```java
orderFormButton.setOnClickListener(v -> {
  Intent intentItem = new Intent(MainActivity.this, DestinationActivity.class);
}); // this enables forward and backward navigation
```

Intents are a lot like HTML's Anchor tag => Take user to a different view or page.

Naming Convention (camelCase and descriptiveness) is important!

Event Listeners and Handlers need to be created at App start.

Note: The Activity that we routed to can route the user *back* to the previous activity using Event Handlers and Callbacks.

#### Various Errors Will Appear in the IDE

Click the Fix command on each Warning to set new Static Data into the XML.

Google Play Store *requires* that all of these are cleared.

#### Building an APK

Build Menu > Build Bundles and APKs > Build APK(s).

These are dumped into folder 

#### Kill Emulator

```sh
ps -ax | grep emulator
kill nnnn
```

```powershell
get-process emulator
stop-process -Name $name_from_above_command
```

### A Look Ahead

Week 1: Android basics.

Week 2: AWS Amplify, then try push to GooglePlay Store.

Week 3: File Storage, Location, and Mine? AWS? Launching other Apps from out App.

Week 4: Analytics and Lectures, as well as monetization of mobile apps, as well as OSS contributing.

Week 5: Final Presentations Week!

About 3 to 7 AWS technologies will be discussed throughout.

Consider getting AWS Certificates post-Code 401, but don't forget having completed school work to *prove* your knowledge.

Consider MOB PROGRAMMING and DEBUGGING to help get through various blockers/issues throughout these weeks.

### Hash Maps

Sets and Maps are like really big arrays.

Hash Maps are in best-case O(1), and lookup based on keys is very effecient even with very large data sets.

Do *not* just overwrite data, use collision handling (chaining etc) to deal with duplicate keys.

Handling collisions will be a *requirement* going forward.

## Thursday 24-June Notes

TODO: Fix the Neighborhood ZipCode Record type so that the GH tests stop failing!

### Android Dev Testing

MUST run emulator to do integration / UI testing.

Standard unittests can be run, but only against non-UI components and members.

### Android Dev Thursday

Intents: Routes between activities.

Preferences: Simple data storage for (settings?).

Espresso: Click-test testing in Android Studio.

Action Bar: The header bar the the Activities, located in the Theme definition, and can be shut-off/hidden.

#### Android Dev Thursday Talk

Activities: The Views and/or Forms that display information on the screen and provide interactive elements like buttons and textboxes and labels.

MainActivity (the first form you see).

Shared Preferences: Persistent, local storage, accessible from 2 fully-functional, separate Apps. Similar associative behavior is Facebook and the Messenger apps. User-info, configs (light/dark mode), etc are commonly stored here. Do NOT store large data items here.

Extras => Intents: Transitive Storage.

Rooms: The "database on your phone". Meant to store larger data sets.

AWS/Cloud Storage: Even larger datasets and complex information should be stored in the cloud.

Rename MainActivity to HomeActivity (refactor) so it is more semantically understandable.

Recommend creating an "activities" package to place all Activities into so they are well organized.

Text Elements are based on TWO DIFFERENT CLASSES and READONLY or READ-WRITE behaviors:

- Text display element: TextView.
- TextEdit elements: All the other "text" elements.

##### Shared Preferences Setup

1. Remember to set an id to every element added to the UI.
1. Declare a public static final TYPE property to create a KEY to associate with KVP to store in preferenceEditor.
1. Declare 'SharedPreferences preferences;' as a Class Property.
1. Create shared preferences instance 'PreferenceManager.getDefaultSharedPreferences(this);'
1. Get Save button 'Button userSaveButton = findViewById(R.id.BUTTON_ID);
1. Use onClick (see code detail below).
1. Get nickname (see code detail below).
1. Put nickname in the preference editor.

```java
public class ... {
  // set up the editor
  SharedPreferences.Editor preferenceEditor = preferences.edit();

  userSaveButton.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
      // grab the edit text for nickname
      EditText userNicknameText = findViewById(R.id.USER_NAME_INPUT_ID);
      String userNicknameString = userNicknameText.getText().toString();

      // userNicknameString will be the KEY in SharedStorage
      preferenceEditor.putString(USER_NICKNAME_TAG, userNicknameString); 
      preferenceEditor.apply(); // DO NOT FORGET THIS ELSE NOTHING SAVES!!
    }
  });
}
```

##### Shared Preferences Consumption

1. init shared prefs
1. get the value
1. set the returned value to a view Element

```java
// after the Class declaration
SharedPreferences preferences;

// within a method that needs to grab this data
preferences = PreferenceManager.getDefaultSharedPreferences(this);
String userNickname = preferences.getString(UserSettingsActivity.USER_NICKNAME_TAG, "No Nickname");
TextView userNicknameText = findViewById(R.id.ELEMENT_ID);

// the rest of the method and class code...
```

##### Toasts

```java
Toast.makeText(UserSEttingsActivity.this, "Settings saved!", Toast.LENGTH_SHORT).show();
```

##### Snackbars

```java
Snackbar.make(findViewById(R.id.ELEMENT_ID))
```

##### Device File Explorer

Check out 'data.com.yourthing.packagename' to view cached data including 'Shared Preferences'.

#### Android Activity Lifecycle

Check out [The Activity Lifecycle on Android Developers](https://developer.android.com/guide/components/activities/activity-lifecycle)

Check out the [diagram](https://developer.android.com/reference/android/app/Activity#activity-lifecycle)

Only run when the View first loads: 'onCreate()' => ONLY runs the very first time a View is loaded and launched.

Runs when the View is resumed: 'onResume()' => When going BACK to a View

#### Android Extras

These are used to send things along with Intents.

#### Android Values Strings

Use 'strings.xml' in res/values directory to store regularly used strings e.g. for UI element text.

### Espresso Testing Intro

1. Emulator MUST BE RUNNING.
1. Run > Record Espresso Test, do NOT force close it.
1. Click items (slowly) and watch the Record Your Test viewer load with the UI navigation commands.
1. Add an Assertion Statement e.g.: Does a text box have the correct text in it? Do the expected element(s) exist on-screen?
1. Save and allow installing the test dependencies.

The test is then written for you!

## References

Raul: logcat [Colors](https://stackoverflow.com/questions/39993867/android-studio-logcat-colors/39993868#39993868)

Raul: more logcat [Stuff](https://developer.android.com/studio/debug/am-logcat)

## Footer

Return to [root readme](../README.html)
