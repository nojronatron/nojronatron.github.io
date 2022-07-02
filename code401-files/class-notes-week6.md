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

## Friday 24 June

### Code Challenge Whiteboard Discussion

Using shortcuts in the whiteboard is okay so long as you are vocalizing what these shortcuts mean e.g. while in an interview.

The right-tree might have duplicate values within itself! Solution: Use a SET to force uniqueness, or otherwise implement a way to avoid duplicates in your output.

Use the heading Questions/Edge Cases:

- Do I already know already how to do what I'm about to ask?
- Make sure you have the ability to talk-through what built-in functions do before you use/ask about them.
- Always ask about value types including signed vs unsigned numbers.
- Always *go back to this section while whiteboarding to add items while working through the design process.

Question: When hashmapping Numbers, is a colliding value guaranteed to be a duplicate?

Tip: Arrays are usually a good go-to starting point for storage and/or returns, rather than creating a custom object, or dealing with Dicts, Sets, etc.

### Android Development Recycler Views and More

Android Studios [Recycler View](https://developer.android.com/guide/topics/ui/layout/recyclerview)

A Recycler View is similar to HTML tags UL and OL.

Only loads what it can display, rendered through fragments.

A View Holder encapsulates a Fragment.

A Fragment contains the actual data.

Actual data will be stored in an Array (or other Collection).

ScrollView: Loads ALL DATA AT ONCE, so it could heavy.

#### Set A TextView Into A Fragment

1. Add a RecyclerView to the Activity where you want it to belong in WYSIWYG, give it a good ID.
2. Create a method to grab a reference to the RecyclerView.
3. Set the Layout Manager of the RecyclerView to a LinearLayoutManager.
4. Set the Layout Manager horiz/vert scrolling behavior.

```java
// 2. Create a method to grab a reference to the RecyclerView
private void setUpProductListRecyclerView() {
  RecyclerView productListRecyclerView = findViewById(R.id.productListRecyclerView);
  // 3. Set the layout manager of the RecyclerView to a LinearLayoutManager
  //    REMEMBER TO ADD the Context, which is usually the Activity you are currently in.
  RecyclerView.LayoutManager layoutManager = new LinearLayoutManager(this);

  // 4. Set the Layout Manager horiz/vertical scrolling behavior
  productListRecyclerView.setLayoutManager(layoutManager);

  // 6. Bring in the ProductsListRecyclerViewApdater
  ProductListRecyclerViewAdapter adapter = new ProductListRecyclerViewAdapter();

  // 7. Set the adapter RecyclerView
  productListRecyclerView.setAdapter(adapter);

}
```

5. Create a new ProductListRecyclerView Class.

```java
public class ProductListRecyclerViewAdapter extends RecyclerView.adapter {
  // Implement all 3 methods required by the Interface/Abstract Class
  ...
}
```

6. Back to the setUpProductListRecyclerView method, bring-in the ProductListRecyclerViewApapter.
7. Set the adapter RecyclerView in setUpProductListRecyclerView method.
8. Make a FragmentClass called "fragment.ProductListFragment" using a "Blank Fragment template.
9. COMMENT-OUT any Params statements, and any code statements that rely on them.
10. Open the Fragment in the DesignView and name it appropriately, set up layout_width and layout_height, and supply it an ID that makes sense. There are no constraints like an Activity would have. Enter FrameLayout tool and CHANGE the Fragment from Frame Layout? to a "Constraint Layout".
11. Go back into the Adapter Class and edit the onCreateViewHolder() method to 'Inflate the Fragment'.

```java
// 11. Inflating a Fragment
public RecyclerView.ViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
  // Dealing with a Layout so R.layout instead of Id
  View productFragment = LayoutInflater.from(parent.getContext()).inflate(R.layout.fragment_product_list, parent, attachedToRoot=false);
  // 13. Attach Fragment to ViewHolder within the onCreateViewHolder() method in ProductListRecyclerViewAdapter.
  return new ProductListViewHolder(productFragment);
}
```

12. Create a ViewHolder class to hold a Fragment called ProductListViewHolder *inside* ProductListRecyclerViewAdapter. Include a default CTOR that accepts a View type param, and update the super() statement if you've changed the param name.
13. Attach Fragment to ViewHolder within the onCreateViewHolder() method in ProductListRecyclerViewAdapter.
14. Configure ProductListViewHolder.getItemCount() method to return hard-coded Integer 100 (for testing purposes).

Next Set of Steps:

1. Create a Data Class e.g. Product, and include a CTOR, Field(s), and GET/SETters.
2. Create Data Items and store them into a ListArray. These just represent data that would come from any data source e.g. a DB.
3. In ProductListRecyclerViewAdapter create a field as a Collection of e.g. Products, create a CTOR with the product param.
4. Bind data items to Fragments inside of ViewHolders within method onBindViewHolder(). (see Class Code Repo for the TextView holder code that goes in here). Include a codeblock that will call products.get(position).getName() and assign the output to String productName. 'productFragementTextView.setText(position + ". " + productName);'. Also include  in getItemCount() method 'return products.size()'.

Make Entries TAP-able:

1. In ProductListRecyclerViewAdpater class, clean up the RecyclerView.Adapter references to actually use ProductListRecyclerViewAdapter. Update remaining methods that need to use the ProductListViewHolder in Params etc.
2. Hand-in the Activity Context. In MainActivity, supply Context to the ProductListRecyclerViewAdapter, by adding 'this' to the params list (which causes red lines). Set a Field of type Context called 'callingActivity' and add Context to the CTOR so calling methods can include the Context with the method call.
3. OnClick event listeners must be set on the Bindings, not on the View Element.
4. Include a putExtra() method to store the productName (grabbed by its position, previously) and then call callingActivity.startActivity(goToOrderFormIntent).

## Dr. Robin Behavior, Interviews, and Strategies

### 7 Steps from grad to employment

Graduation => Employment

1. Finish 401
2. Look for work => When you start looking is up to you but *do not languish*. Take time off, but get back to the routine ASAP.
3. Send Stellar Resume to employers => Select *great* projects to showcase; describe who you are and what you know.
4. Leverage your network.
5. Technical Interviews.
6. Meet the team => Behavioral questions, learn about the org, pitch yourself. At this point *you are being seriously considered*. Will *I* fit in this space? Can I hit the ground running?
7. Receive an Offer =>
8. Negotiation => DO NOT SHY AWAY from this, speak up for yourself and counter at least once, then decide to continue with offer negotiations, or thank them and move on.

### GTM Strategy

- What is my value proposition? Sell myself, I am it.
- Tech is a creative space.
- Two primary concerns are Financial and Interpersonal.
- I have the skills to do the work that somebody else is willing to pay to get done.

### Behavioral Interviews

A series of questions and/or scenarios, that have you explain how you handle situations.

- challenges with co-workers
- disagreements with supervisor
- changed deadline
- working with someone who is difficult to work with (punctuality, different ideas/perspectives)

Considered to be the best predictor of future behavior.

It's really a conversation about past experiences.

- work related
- non-work experiences

Practice the STAR Method to *become ready* to handle these questions.

Remember that the Results part of the STAR method is an opportunity to elaborate on what was learned, takeaways, etc.

Common Questions:

- Tell me about yourself? This is your pitch!
- Strengths & weaknesses
- How I fit in a company
- Chance(s) to take the lead
- Went above and beyond
- Experience of failure, mistake, challenge

"Tell me about a time when you had the chance to take the lead."

Respond in the format: Situation, Task, Action, Results.

Advice:

- Keep yourself at the center of the story
- Avoid sensationalism which could take away from your Actions and Results
- Keep the story compelling, but short
- Allow the interviewer an opportunity to ask *more* about your response
- If you cannot share an exact experience, use "that has not been my experience, but here is what I would do..."
- Results should include something about what you learned from the experience
- Answer questions in a way that tells the interviewer about you and your strengths

## References

Raul: logcat [Colors](https://stackoverflow.com/questions/39993867/android-studio-logcat-colors/39993868#39993868)

Raul: more logcat [Stuff](https://developer.android.com/studio/debug/am-logcat)

How to answer behavioral questions [on YouTube](https://youtu.be/IV30jAw7dxA)

Behavioral interview dos and donts by [MyPerfectResume.com](https://www.myperfectresume.com/career-center/interviews/prep/11-crucial-behavioral-dos-and-donts)

[Smart Strategies](https://www.job-hunt.org/smart-behavioral-interview-answers/) for behavioral questions.

Glassdoor [How to prepare for the interview](https://www.glassdoor.com/blog/guide/how-to-prepare-for-a-behavioral-interview/)


## Footer

Return to [root readme](../README.html)
