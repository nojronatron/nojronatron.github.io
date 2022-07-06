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

## TODOs

- [ ] Practice traversing data structures to prep for interviews.

## Footer

Return to [Root README](../README.html)
