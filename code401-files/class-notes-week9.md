# My Notes From Class And Daily Work Week 9

## Goals For This Week

- [ ] Whiteboard interviews scheduling.
- [ ] Prep for final project week.
- [ ] Code Challenges will be whiteboard-interview practices.
- [ ] Instructor resume sign-off.
- [ ] Complete CEP entrance prerequisites. Interview can be scheduled for after finals week.
- [ ] Ethics in Tech reading *must* be done before Thursday morning.
- [ ] Finish up lingering assignments prior to Friday.
- [ ] Final Whiteboard Exam Review.
- [ ] Final Project Preps *must* be completed before working on the project.
- [ ] TODO: Complete the BusinessTrip tests with TODOs for future improvements, updates.

## Going Forward

Finals Week team reviews due Sunday following final presentations.

Review the core Java knowledge like:

- Name the 7 primitives.
- Object inheritance and polymorphism.
- Interfaces and abstractions.

## Tuesday 12 July

Tuesday is last day of code content.

Tuesday will be GooglePlay Location.

### S3 Review

Add Image Button => Image Picking Activity.

Convert to an input stream and publish to S3.

Geocoding: Referencing a place by it's name or street address, and translating that to geographical coordinates.

There are privacy concerns, both PII and App, Phone security implications.

### Final Project Prep

Teams need to work on project ideas and prepare, as a team, to pitch up to 2 ideas to Alex.

Teams need to agree on what they want to do before pitching it.

### Domain Modeling

It is in *everything*.

Relationships exist in databases, but also just about everything else!

### Lab - Location

GooglePlay Services: Location Provider Client - is a newer thing. The older service required the App to manage the connection to Google API Client service.

SocketIO

- Open sockets to communicate with another server.
- Logic exists to handle interruptions, but is essentially an open, tethered internet connection.
- Resulted in lots of callbacks in App implementation.

New:

- In onCreate lifecycle, implement FusedLocationProviderClient.
- LocationServices.getFusedLocationProviderClient enables requesting various types of location updates.

Last Location:

- Minimal battery usage.
- No active network connection.

Current Location:

- Much more battery usage.
- Active network connection.

Request Location Updates:

- Enables regular updates when the Device is moving.

Before Writing Code, permissions requests must be updated:

1. Go into `AndroidManifest.xml`. Multiple permissions can be edited here.
1. Add `<uses=permission>` tags for one or both of `ACCESS_FINE_LOCATION` and `ACCESS_COARSE_LOCATION`. Don't ask for high precision unless the App really needs it.
1. Run & Debug will reinstall app. Reinstalling App is required whenever permissions are changed.
1. Implement a completable future
1. Programmatically request permissions via requestPermissions as a new String[] that contains the `Manifest.permissions.PERMISSION_NAME_TAG` comma-delimited list.
1. Call fusedLocationClient to get application context via LocationServices.getFusedLocationProviderClient
1. Execute `fusedLocationClient.getLastLocation()` and chain-on `.addOnSuccessListener()`
1. Use an if statement to determine if ActivityCompat.checkSelfPermission() returns as expected.
1. Implement a listener that executes (sometime) depending on success or failure getting the location. Basically, checking what Allow Permission(s) the App has.
1. Within the listener assign results from object 'location' to get Lat, Lon, Speed, Altitude, Time, and many others. Lat and Lon are of type 'Long'.
1. `ActivityCompat.checkSelfPermission()` requires a context (this), and a `Manifest.permission.TAG_OF_PERMISSION_TO_QUERY`.

*Note*: The live demo coding session resulted in an error situation. Basic solution required:

- Opening GoogleMaps and allowing Location Access.
- Restarting the App with the new Permissions settings.

#### Location Resources

Android Developers Blog [New Location APIs](https://android-developers.googleblog.com/2017/06/reduce-friction-with-new-location-apis.html)

Android Developers [Last Known Location](https://developer.android.com/training/location/retrieve-current#BestEstimate)

Android Developers [Network Connections](https://developer.android.com/training/basics/network-ops/connecting)

Android Developers [Declare Dependencies](https://developers.google.com/android/guides/setup#declare-dependencies)

Android Developers [Retrieve Current Location From Play Services](https://developer.android.com/training/location/retrieve-current#play-services)

Android Develoeprs [Location Requests](https://developers.google.com/android/reference/com/google/android/gms/location/LocationRequest)

## Wednesday 13Jul22

### About OSS and Contributing

Transparency is very important in development.

OSS isn't just about free, it can be licensed and sold.

Many eyes on OSS can make it better.

Proprietary software can be constricted/restrictive in ways that do not support the community.

OSS contributions can (and should) be highlighted on your resume, and definitely in your GitHub/repositories.

Some OSS repos will have guidance for new contributors. Look for a "want to contribute?" button or link, or a search filter.

Check GitHub Issue labels:

- "good first issue"
- "backlog" - indicates not enough time to work on these
- "docs" - help improve documentation
- "feature requests" - look for discussions around these to help get started

GitHub "Trending" repos: Could be a good resource, but sometimes the trend is all the possible "good first issue" items are already solved.

#### For the OSS Lab

Go to the FirstContributions repo - a directory of OSS projects that have potentially good first issues for new OSS contributors.

What is a good contribution?

- Small bug fix in a noteable OSS project.
- Fix/Add unit test in nateable OSS project.
- Fix an issue in a hobby project.
- Three separate small documentation contributions in separate projects OR 3 doc updates in a single LARGE project.

*Do not* write fluff documentation. Ever.

### Root Cause Analysis

RCA -> Scientific method to analyse WHY something happened, external causal factors, and the timeline in which the problem occurs.

Troublshooting

- Documenting the problem: Log
- When did the problem occur? At what point are things fine vs when they are no longer *fine*. Breakpoints are a good tool in this regard.
- Distinguish between the root cause, and other external factors.

There are 5 Why's of RCA:

- WHY is this thing dead?
- WHY is what it depends on not functioning?
- WHY is what that thing depends on broken?
- WHY was the part allowed to stay in place beyond its useful life?
- WHY was the maintenance schedule not followed? This is the root cause, but cascades to the 1st WHY.

RCA Reference by [Wikipedia](https://en.wikipedia.org/wiki/Five_whys)

### Final Project

Re-teaming to a single, 6+ person team.

- Not everyone needs to talk but everyone needs to contribute to the presentation (in addition to the project as a whole).
- My goal will be to step-back from *doing* project managing activities and instead *guide others* in this regard.
- We need to be prepared to talk about what we did in detail.

Everyone needs to ask themselves:

- Am I doing too little?
- Is imposter syndrome playing a part in sense of too-little or too-much?
- Look at what I *have done* and use that as a bar for determining what my participation level *actually is*.
- Be prepared to speak up, promote ideas, AND inclusively promote ideas and feedback of others.

TODOs:

-[ ] Determine what my areas of improvement are and *be prepared to talk about it* during the final presentation.

### Whiteboard Review

Node Logic:

- What the problem domain is asking.

Advice:

- When using recusion, use a helper method!

Avoid Assumptions, instead:

- ASK the question before doing what you plan to do.
- STATE what it is you are going to do and react appropriately if the interviewer has feedback/guidance.

Breaking Down The Problem Domain

- Difficult to break it down completely on the first pass.
- Verify what needs to be returned by asking questions and making statements while jotting notes.
- Write-out method-like pseudo code in chunks that address the small components of the problem domain.

Recursive Functions:

- You cannot just "break out of the loop" when you are done, the stack must unwind itself.
- Returning values is difficult because it must percolate *up the stack*.
- Use global variables to manage capturing and/or updating value(s) from a recursive method.
- When a function pops-off the stack, the previous function call *state* will be as it was when it called the now-popped method.
- Passing items by Value might be better than passing by Reference might be necessary in recursive functions.

Suggested Execution Pattern (subject to everything, and ask questions as needed in-flight):

1. Pick a traversal mode and sketch it out.
1. Break down the Problem Domain to determine what processing mechanics are needed to address all of its components.
1. Refactor the drawings and any problem domain brake-down jottings and write them up as plain-english Algorithm segments. Reference the Problem Domain by talking through this refactoring and algorithm writing.
1. Update my questions, test cases, and edge cases. Test Approach should include JUnit, Debugging Breakpoints, happy path, null-input, failure path, and so on.
1. Write pseudocode.
1. Once pseudocode is done, BigO can be written. Be sure to analyze the pseudocode to justify the BigO analysis conclusions.
1. Refactor any and all representations to ensure they are legible, make sense, and represent your solution.
1. Write actual code.
1. If there is still time clean things up and ask questions about the solution to discover if more work or additional cleanup is necessary.

## TODOs

- [ ] Review Lambda methods in Java re: how 'context' is handled vs named methods.

## Footer

Return to [Root Readme](../README.html)
