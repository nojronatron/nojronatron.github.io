# Week Eight Discussions Log

## Tuesday 5-July

Monday was a holiday.

What full-stack things we've done in class so far:

- PostgresQL
- Spring Framework
- JPA
- Room
- AWS Amplify and DynamoDB

### Tech Interview Scoring Advice

Technical Interview scoring:

Interpreting the Question:

- Asking questions: Get free points by asking null, how many, already sorted, in-place or new questions.
- Question: If you are not told what to return, ask what needs to be returned, including type of structure.
- ID I/O: "Input is n, Output is n" and *must* be visually depicted on the whiteboard.
- Illustrate the problem domain: What is actually happening? What is going on and what is happening to the tree?
- ID Optimal Datastructure: This is usually discovered while asking questions and determining the input and output. What is the parent-child relationship in the data? Knowing this will help.

Solved the Technical Problem:

- You *must have finished code* to get points.
- You *must have a complete algorithm* to get points.
- Solution was the best possible? Full 2 pts for using the correct datastructure, but any solution should get you a single point.

Analyze the Proposed Solution:

- Step through the solution. Tell the interviewer what your code/algorithm is doing.
- Reason your way through BigO, but points could be up to the interviewer.
- Explain an approach to testing: Nothing will net zero points. JUnit, Espresso, null-testing, edge-value cases, and arrange-act-assert method.

Communicated Effectively Throughout:

- Verbalize the thought process.
- Use correct terminology: Traverse a datastructure. Iterate or Recurse a looping structure.
- Use time effectively: Get to writing the algorithm and the code as quickly as possible to get this full point.
- Over/underconfidence: Be confident despite not knowing what is going on. Alternatively, don't be over-confident if you *do* know what is going on.
- Readability of whiteboard: If it is difficult to separate different sections/boxed-in/illegible, clean it up for a free point.

Keep In Mind:

- You might be told to continue within a set of constraints - you must handle this situation gracefully and *go with it* as if a paying customer is telling you what they want.
- Interviewer *wants to see your process*, and learn about your personality such as friendliness, engaging, performance under pressure.
- If you use a built-in method, be prepared to talk about it - how it works, implications, etc.

### Deploying Your App To GooglePlay

Inclue images. Don't have to be exactly right but get the idea behind how the app operates.

Screenshots: Include screenshots of your app "in action".

Be aware that your app will get rated by users, bots, etc.

Updated On: Be realistic but keep it regular. A stale app might not look too good to some users.

Starting an App as "free" cannot easily be changed to "paid" later. Consider starting the app as "Paid" to make transition to "Free" easier.

Android App Bundle: AAB file extension. `app-debug.aab`: Drag this file into the App Bundles upload screen.

> MUST create a signing key and sign the bundle in order for GooglePlay to allow publishing to the store.

Generate a key in the "Generate Signed Bundle or APK" modal.

- Be sure to retain the signed key location.
- Generate a Release.

Multiple AAB files can be uploaded to the Release workflow.

Release Name will get updated when you upload your signed AAB.

Release Notes should be updated though.

Always update documentation when content in the App changes.

There is a Set Up Your App workflow that you should follow:

- App Access: Set restrictions for *user access* (AuthN, AuthZ) to your application.
- Set up Ads settings, if the App has Ads.
- Content Ratings: Add a spam-ready email and supply responses to categorization etc, of your app. Review the listed ratings for other countries.
- Target Audience and Content: Not much to note here.
- Privacy Policy: Need a privacy policy URL. Fill out the app-privacy-policy-generator.firebaseapp.com website to generate one.
- Enter target-age for the app.
- COVID Contact/Status Tracing App: Need to state yay/nay.
- Data Safety: Will walk you through required disclosures of how your app handles user data types. *Be sure to read this*!
- NewsApp? No, unless it is.
- App Category:
- Store Listing:
- Contact Details:
- Create new Release:
- Test/testing Actors and Groups:

Main Store Listing:

- Description
- app icon (creative commons license or similar *required*).
- Feature Graphic and App Icon sizing are included.
- App screenshots. Inclue at least 4 (to be considered for spotlighting).

Testing:

- Closed: Set up an App to be tested by specific users.
- Cannot select a 1.0 version number. App-level build.gradle must be edited prior to producing an AAB file for closed testing.
- Open: Select where users can be open testers of your App.

In Summary:

1. Set aside several hours to get this all organized.
1. Set up your app must be completed first.
1. Set up the App as free, or later on a Payments Profile can be added to monetize the App.
1. Release your app.

Google Play Store will tell you when things are wrong or not ready for publication.

### Using Deletes with GraphQL and Amplify

CUD: Create, Update, Delete. Part of CRUD.
Query: The READ part of CRUD.

Delete Process:

1. Send instance details using Intent Extras.
1. Get the ID of the item you want to delete.
1. Query the DB to get the instance by ID.
1. Within the response lambda: LOG, then `Amplify.API.mutate()` and see code below for inner detail.

```java
// setup a listener, create an Amplify API Query, get the data, then handle delete within a nested .response() lambda
deleteButton.setOnClickListener(view -> {
  Amplify.API.query(
    ModelQuery.get(TaskModel.class, finalTaskId),
    response -> {
      Log.i(TAG, "message");
      Amplify.API.mutate(
        ModelMutation.delete(response.getData()),
        success -> Log.i(TAG, "message"),
        error -> Log.e(TAG, "message")
      );
    },
    error -> Log.e(TAG, "message")
  );
  finish();
})
```

### Lab Goals Today

1. Register for GooglePlay Developer account.
1. Ensure the TaskMaster App can read & write to Amplify w/ GraphQL.

### Code Challenge Class 34

1. Find a peer and work through the whiteboard.
1. Work through the rubrik.

### Career Coaching Workshop: Presentation Prep

1. Begin working through the presentation workshop slides.
1. 7 slides + Title + Final side.

### Career Accellerator Update

Next Saturday will feature assignments that should be completed if interested in joining CAP.

- Schedule a qualifying interview with Dr.Robin: Soft-skills/behavioral interview.
- Discussion assignment (in Canvas) to ID what I will do to continue successful motivation and moving forward as a developer and attaining a job.

### Post-Interview Debrief

Areas where I need to improve:

- Review the problem domain while working through it.
- Once I have agreed to inputs, outputs, handling, etc, I need to stick with that agreement.
- In the problem depiction, separate input(s) and output(s) so they are clear.
- A Binary Search Tree *is* sorted, so verify this (with a question) and then utilize that knowledge to find what is being asked for.
- Write pseudocode in place of an algorithm.
- Casing: Don't mix snake, Pascal, and camelCase in the code. Stick with one throughout.
- Ensure the *best possible solution* is used.

Remember Big(O) in time:

- O(1) is constant time.
- O(n) is Linear Time (increases linearly with inputs).
- O(n log n) is logarithmic Time (increases more than linearly but less than exponentially).
- O(n^2) is exponential time (increases exponentially with inputs).

Trees:

- Breadth-first Traversal: Uses a Queue (breadth is horizontal, so is a Queue depiction).
- Depth-first Traversal: Uses a Stack (or the call stack using recursion) to walk down the left then up the right children of all nodes (Deptch is a vertical operation, Stacks are vertically aligned depictions).

## Weds 6-July

### Authentication Considerations In General

Going to need the following:

- A registration page where a user can add a username, email, and create their own custom password.
- A login page with username or email and password.
- Functionality to store a password securely (hashing, salt + hash, etc).
- A LOGOUT button.
- Conditional rendering to determine if/when to display either Login or Logout buttons.

Great functionality to have:

- Once a user has registered, the login page pre-populates the username/email address the user added.

### Amplify and Authentication

OAuth is only supported in JS (for "social sign-in"), not for AndroidStudio.

### Amazon Cognito

Identity Pools are free of charge: Sign-up, login, logout, and verification.

IAM Authenticates Developers that manage data, processes, etc.

Cognito Authenticates END USERS.

Cognito can also be used for Authorization.

User Pools:

- Managed service for all users within an app.
- Is essentially OAuth (?)

Cognito will be another AWS "Category: API".

Check out [my getting started with Cognito reading notes](./amplify-cognito.html)

### Steps

1. `amplify add auth`
1. Use Email to signing.
1. Advanced settings? No (for now).
1. `amplify push`: Builds local backend resources and provisions in the cloud.
1. `amplify publish`: Builds local backedn and frontend resources and prvosions.
1. Implement Amplify addplugin statements to your code (entrypoint? HomeActivity?) onCreate() to get ref on AWSCognito.
1. Implement Cognito registration statement(s) to your code (right after the previous step code).

Remember: Intents are used to move user to a new Activity (see [my notes on Component Activation](./android-fundamentals.md#activating-components)).

Note: Amplify.Auth has a bunch of built-in methods. EXPLORE THESE, as some of them allow 3rd party auth methods like facebook, etc.

Remember: When dealing with Amplify *you must use a builder* e.g. `AuthSignUpOptions.builder()`, and builders use chained-methods to configure e.g. `AuthUserAttributeKey.email()`. End with `.build()`, a comma, then `success -> {log}, failure -> {log}` sub-block.

### Cognito AWS Web UI

Go here to see the users that have registered.

Displays details about registered users.

Password details, hashes, etc, is not easily available.

Login experience can be configured here as well.

### How To Get Nickname To Display

Use Fetch User Attributes.

Can add this to onResume lifecycle method.

```java
public void fetchUserDetails() {
  // remember: this is running in a single thread so UI update requires special handling
  String nickname = ""; // this could be a global variable
  Amplify.Auth.fetchUserAttributes( // note: .fetchAuthSession could be used in similar way but not for this
    success -> {
      // log result of fetching user attribs
      for (AuthUserAttribute authAttrib: success) {
        if (authAttrib.getKey().getKeyString().equals("nickname")) {
          String userNickname = authAttrib.getValue();
            runOnUiThread(() -> {
              ((TextView)findViewById(R.id.id_of_view)).setText(userNickname); // casting required if not grabbed earlier
            });
        }
      }
    },
    failure -> { // log this failure state with info }
  )
}
```

Functionality: If email address is 'verified' is a good place to implement authorization within the App.

### Implementing Login and Logout Buttons

1. Create method called something like handleSignIn.
1. Implement Amplify.AUTH code in it.
1. Call handleSignIn from onCreate.

Handle Conditional Rendering

1. Create a new method called setupLoginLogoutButtons or something similar.
1. Consider whether to call setupLoginLogoutButtons at onCreate and/or onResume lifecycle method(s).
1. Instantiate a new authUser using Amplify.Auth.getCurrentUser();
1. If authUser is null get a ref to the Login Button and set its visibility to visible e.g. View.VISIBLE.
1. Same for the logout button BUT View.INVISIBLE.
1. If authUser is NOT null, get a ref to the Login Button and make it View.INVISIBLE.
1. Same for the logout button BUT VIew.VISIBLE.

Conditional Rendering Activities

1. Perhaps implement a specific Registration and Login Activity(ies).
1. Do an authentication check before executing `setContentView(R.layout.activity_name)`.

### Testing

Espresso Tests are optional but *encouraged*.

Unittests are not required, but *encouraged*.

Do manual testing though, to verify authentication is operational.

### Logging

Check System logging files in `/var/log`!

App logs will probably be in the installation directory of the App itself.

Advice:

- [ ] Always find out where file-based logs are stored for the app (service, etc) you are working on.
- [ ] Review the logs to see what they look like.
- [ ] Understand the types of error logging: Info, Warn, Error, Debug, Verbose... others.
- [ ] Get a grasp on how to utilize the Logging utility so you can add to the logs in your custom methods.

## Thursday 7July Notes

### S3 Storage

Simple Storage Service.

Buckets of snakes (objects representing data).

DynamoDB: AWS's noSQL DB with relational capabilities overlayed.

- Relationships can be mapped.
- Max size 400kiB for data pages.
- Able to CRUD data, especially UPDATE.
- Designed for low-latency, sustained performance.

S3 By Comparison:

- CanNOT update, only replace.
- Max size 5 TB.
- No indexing, no search/queries, no transactions, etc.
- More like a hashmap: Need to send a Key to retreive stored Objects.
- Can throttle your network transactions.
- Is "bursty" meaning performance is not tuned for low-latency.

Three out of Four steps to show an image are ASYNCHRONOUS:

1. Select an image.
1. Upload to S3.
1. Link to Data.
1. Display Image.

JS uses Promises and async/await.

Java uses CompletableFuture which is a more complete solution that Promises.

Uses `.complete()` a CompletableFuture otherwise an async call will remain incomplete in the Stack.

There is a *lot* of boilerplate code to write to get this working so modularize a lot.

### LL and Tree Traversals Review

#### Linked List

Single LL Traversal:

- Use a while loop to iterate through the LLNodes.
- Loop condition should be `Current != null`.
- Problem Domain logic goes within this iterating code block.
- Next node is found through assigning: `current = current.next`.

#### Trees

Binary Tree vs. Binary Search Tree

BST:

- Is sorted.
- Everything to the left of the parent is LESS THAN value of Root.
- Everything to the right of the parent is MORE THAN value of Root.
- Be sure to depict it properly when drawing.

### Technical Interviewing Advice

It is okay to talk about an iteration / traversal without addressing the problem domain logic when depicting how the solution will work.

However, the logic that occurs inside the looping structure ("under the while" in the depiction model) must also be visualized.

It is okay to ask the interviewer if you can use a library object to utilize Queue or Stack. If they ask what you need then tell them the specific methods and functionality you are looking for.

If unable to use a Library-based Queue or Stack, then use recursion.

Ask the interviewer how the data is coming in to the algorithm to determine whether balancing is necessary.

Consider initialize the value of Root/Head as the comparison value.

Find a root by thinking about Preorder, Inorder, and Postorder: Beginning, Middle, or End of an array (in the end).

#### DFS vs BFS

DFS: Depth First Search

Preorder: Logic FIRST, children LAST.

Inorder: Left child FIRST, Logic SECOND, Right child LAST.

Postorder: Children FIRST, Logic LAST.

#### Recusion

Types:

- Single or Multiple Recursion: One or more calls to the method itself.
- Implicit Recursion: Recursive method calls another method that calls the recursive method.

While whiteboarding, whenever a recursive function calls itself, put the calling method on the Stack (represent with a value if possible).

### Android Image Picking Actvity

Intents can be used to do more than just navigate between Activities.

An ImageSelector can be launched using an Intent.

Android ImagePicker has an onTap functionality.

Develop an impagePickerResultLauncher that is triggered by onActivityResult event handler lambda.

OnActivityResult should:

- Open local image as an input stream.
- Call custom method uploadInputStreamtoS3(InputStream).

uploadInputStreamToS3(InputStream) should:

1. Upload the image to S3 AND capture the S3 Bucket Key.
1. Store the S3 Bucket Key by calling another custom method saveProductKey(String s3Key).

saveProductKey(String) should:

1. Store key to DynamoDB.

Flow Summary:

- Use intents to get to the image picker.
- Use lambda callbacks to chain-together functions.
- Open the file and prep for streaming.
- Upload stream to S3 and capture the Key.
- Store the S3 Key to DynamoDB.

*PRoject Goal*: Grab the image, stream it to S3, then display it on the local device.

### Android Intents

When using Intents to select an item and launch a new Activity:

1. Get the KEY of the item that was selected. This could require a completable future call to a distant DB.
1. Set up the Activity to be called to collect and use the Key via Intent Extra. A CompletableFuture call might be necessary to call a distant DB to hydrate the object instance using the Key.
1. Just pass-in the Key as an Intent Extra when setting up and calling the Intent to load the next Activity.

Use Intent.ACTION_GET_CONTENT: ??

Using `ActivityResultLauncher<Intent>`:

- Ensure to make this a `CompletableFuture<T>` at the global Class level.
- MUST be initialized within `onCreate()` method *with a value* otherwise will *always be null*.

Using `Intent.EXTRA_MIME_TYPES`:

- MIME types must match for web servers to understand how to handle data.
- AndroidStudiod uses this to only allow JPG or PNG files.

Activity Result:

- Must register for one using `registerForActivityResult()`
- Must add ActivityResultContracts as a Contract.
- Must include a Callback method for the method to call when it is done doing its work.

### A Quick Note About GraphQL Schema To Support S3

For the Labs a change will be made that will associate an S3 Bucket storage file with a Task. In order to support this in the TaskMaster app, a GraphQL Schema change is required.

In my case, I added `imagepath: String` to the Task Entity.

This requires an update to the GraphQL schema on the back-end:

```sh
amplify push
# continue? Yes
# update code for your updated GraphQL API? Yes
# Generate GraphQL statements (Queries, Mutations, Subscriptions) based on schema types (this will overwrite existing)? Yes
```

*Note*: Schema changes might not be immediately visible in the console and could require adding a new item (or edit an existing one) before the column shows.

### Applying S3 Storage to Android Apps

`amplify status`

`amplify add storage`

Respond:

- Content type
- Write a friendly name for the resource
- bucket name should be left at default UUID
- Auth users only (guests should be selected for special situations only)
- Create/update read delete
- no Lambda Triggers

`amplify push`

Insert S3 dependencies ABOVE AuthCongnito in App:build.gradle.

Sync Gradle files.

Add the AWSS3StoragePlugin() into your Entrypoint Activity.

#### Upload A File To Bucket

Create a new method to perform a file upload.

Utilize:

Init a test filename using String filename and File Type.

Try-Catch: Buffered Writer to append strings to a new file and be sure to `.close()` the buffer.

S3 expects a key aka the file reference:

- Must store that key ourselves so that we can get to the file later.
- S3 does NOT have any Query or Search functionality, nor does it return a Key for you.

Implement Amplify.Storage:

Amplify.Storage.uploadFile arguments are: String key, File local, `Consumer<StorageUploadFileResult> onSuccess, Consumer<StorageException> onError`

```java
Amplify.Storage.uploadFile(
// no NULLs are allowed
  testFileS3Key,
  testFile,
  success -> Log.i(TAG, SUCCESS_MESSAGE),
  failure -> Log.e(TAG. FAILURE_MESSAGE)
);
```

#### S3 Amplify Security

Amplify will be allowed to do the things that are configured when implementing it in your project.

This means the "Amplify App" has S3 access, whether or not Cognito has authenticated a user of your App.

It is *up to the developer* to implement user-properties and access logic along with IAM and the S3 File Key to enforce access permissions / authorization.

#### Download A File From Bucket

*Note*: Lab37 preview and work will be on Monday the 11th (appended below).

### Mondy 11 July Continuation Notes

Overview of methods:

1. Activity Result Launcher opens local file as an InputStream, calls UploadInputStream method.
2. UploadInputStreamToS3 using InputStream filedata then calls SaveProduct using String S3Key.
3. SaveProduct using String S3Key.

In Alex's demo, method 1 called method 2, method 2 called method 3.

Remember: Android Activity Lifecycle must be utilize properly to get S3 interoperation working properly. For example, OnResume is most commonly used, but OnCreate and OnClear? are also used to initialize/set and clean-up before and after using the App.

CompletableFuture must be:

- Set up as a global variable set to null.
- Initialized within OnCreate lifecycle method and NOT onResume and NOT a click handler or else it will fail.
- Supplied with a value when used to avoid NULL exception.
- Completed! If this is forgetten, the CompletableFuture will *never complete* and no value.

ImagePicker:

- Is a built-in Activity.
- Must use Intents to move between Activities, includuing accessing ImagePicker.
- Extras: Additional information sent to an Activity along with an Intent.

Allow/Deny Lists:

- Always easier to set requirements on an AllowList.
- Utilize an AllowList to select the correct MIME types.

ActivityResultLauncher:

- Instantiate a new variable globally.
- In onCreate supply it with a value.
- Later on it will be called (?completed?)??

Intents:

- Have Launch method.
- Have other Methods.
- There was a bunch of stuff going on here regarding the FilePicker module that involved Intents and some weird method-ish code that I'll need to review.

Success:

- There are data Fields within the Success Callback Handler.
- TODO: Figure out how to acquire the necessary Field(s) (could be a collection) and use those variable(s) in a Log.i method call.

S3 Storage Key:

- For purposes of this Lab, go ahead and create a global variable to initialize an S3Key for temporary storage within the Activity where it will be acquired.

Whenever calling on AWS Storage Services:

- Need a Key.
- Need an Input Stream
- Need a Success Callback
- Need a Failure Callback
- In the case of Amplify: `Amplify.Storage.uploadInputStream(filename, filestream, success -> {}, failure -> {});`
- Always log the Success Callback

File Access Advice Within a Success Callback Function:

- Wrap the call to reading/writing a file within a Try-Catch structure.
- Prior to the try block, set the file variable to null so it can be compared (null vs has value).
- The Catch block could catch any Exception, but FileNotFoundException is a good bet.
- Log.e (for Errors) should be called in the Catch block.
- When using an InputSteam: It *cannot be reused* inside of the Success Callback so a new one must be instantiated (probably with Null).
- A Stream can be considered a type of Queue: Once you pop the next "chunk" off the Stream, it is no longer in the Stream (it is Dequeued).

Image Viewer:

- Just another UI element.
- Set content to its display the same way as done with TextView and other Elements.

If your Amplify Key expires (these steps need validation):

- amplify api update: change API key to have longer expiration dates
- amplify push

## Friday Notes

### Storage Access Framework Reading Notes

Open files using storage access framework [android developers documentation](https://developer.android.com/guide/topics/providers/document-provider)

SAF (Storage Access Framework) introduced in Android 4.4 (API Level 19).

Browse and open documents, images, other file types, across storage providers.

Standardized file browsing UI.

Implement 'DocumentsProvider' to gain storage access functionality.

SAF includes:

- DocumentsProvider: Implement a Document Provider as a subclass to DocumentsProvider. Built-in document providers include Downloads, Images, and Videos.
- Client app: Custom app invokes ACTION_CREATE_DOCUMENT, ACTION_OPEN_DOCUMENT, and ACTION_OPEN_DOCUMENT_TREE *Intent* actions. Receives files returned by document providers.
- Picker: UI allows access to files from all document providers (filtered by client apps search parameters).

SAF Features:

- Browse content from all document providers.
- Enables long-term, persistent access to docs managed by document provider, including Add, Edit, Save, and Delete operations.
- Multi-user support and USB/transient storage provider support.

Within DocumentsProvider files paths follow traditional file hierarchy.

COLUMN_ROOT_ID: Points to a doc/directory representing contents under that root.

Root of path is a single document, which can point to N other documents, in a cascading 1:N relationship hierarchy.

COLUMN_DOCUMENT_ID: Must be unique. This ID represents a single file or directory. This is used as part of the persistent URI "grant".

Document Properties: Openable with specific MIME type; Traversable (directory, MIME_TYPE_DIR) with additional documents list.

Document Capabilities: Described by COLUMN_FLAGS:

- FLAG_SUPPORTS_WRITE
- FLAG_SUPPORTS_DELETE
- FLAG_SUPPORTS_THUMBNAIL

COLUMN_DOCUMENT_ID can be included in multiple directories.

Control Flow:

`App => OPEN_DOC || CREATE_DOC => System UI (picker) => DriveDocProvider || UsbDocProvider || CloudDocProvider`

System Picker: Asks registered providers for matching content roots when an Intent fires that includes filters e.g. "openable files of MIME type 'image'".

System Picker: Provides a standard UI regardless of which register provider (or providers) and responding to the Intent, including Cloud, USB, or local storage types.

### Storage Access Framework Write a Client App

Invoke an Intent to retreive a file from another app:

Android 4.3 and earlier: ACTION_PICK, ACTION_GET_CONTENT

Android 4.4 API 19 and up: ACTION_OPEN_DOCUMENT, and the above Intents.

Android 5.0 API 21 and up: ACTION_OPEN_DOCUMENT_TREE, and the above Intents.

ACTION_GET_CONTENT: Read or import data, such as a single image file.

ACTION_OPEN_DOCUMENT: Long-term, persistent access, such as a photo-editing app.

Checkout [android/storage-samples Github](https://github.com/android/storage-samples/tree/main/StorageProvider) for code samples.

## TODOs

- [ ] Practice traversing data structures to prep for interviews.

## Footer

Return to [Root README](../README.html)
