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

What is a good contribution?

- Small bug fix in a noteable OSS project.
- Fix/Add unit test in nateable OSS project.
- Fix an issue in a hobby project.
- Three separate small documentation contributions in separate projects OR 3 doc updates in a single LARGE project.

*Do not* write fluff documentation. Ever.


## TODOs

- [ ] Review Lambda methods in Java re: how 'context' is handled vs named methods.

## Footer

Return to [Root Readme](../README.html)
