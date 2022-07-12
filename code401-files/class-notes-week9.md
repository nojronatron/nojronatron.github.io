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

## Final Project

## Footer

Return to [Root Readme](../README.html)
