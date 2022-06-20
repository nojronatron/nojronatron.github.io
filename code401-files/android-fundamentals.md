# Reading Notes - Android Fundamentals

## Introduction

Kotlin, Java, and C++ can be used to write Android apps.

APK: Android App Bundle or Package file.

Android uses APK to install apps via the APK, and is required at runtime.

Android App Bundle: AAB file, `.aab` extension, contains Android Project files and metadata that the runtime does *not* depend on.

AAB files are the *publishing format* and are not installable.

Projects hosted on Google Play deploy optimized APK's that contain resources and code that an Android device will need when requesting App installation.

The Android OS:

- Is a Linux-based OS
- Treats Apps as other Users
- Sandboxes all installed Apps, running as virtual machines
- Assigns unique ID's to each user and App
- File permissions are set to only allow owning App to access its own files
- Constrains a running App to its own process, and manages process recovery (destruction?) when it is no longer needed or when memory is low

Principal of Least Priviledge: Only provide enough access rights for a user or process to do what it MUST do, and nothing more.

Apps can be allowed to share data with each other, and access system services.

Apps can share the same user ID, which will allow them same-file access.

Apps can be configured to share the same VM, but they must also have same ID and Certificate.

Apps that need/want access to the compass/location, bluetooth etc, must be provided permission to access those system services.

## App Components

Four different app components:

1. Activities
1. Services
1. Broadcast Receivers
1. Content Providers

Each component has a lifecycle defining creation and destruction of the component.

### Activities

Entry point for interacting with a user e.g. screen with user interface.

Together, multiple activities create a User Experience.

Activities can interact, if given permission to do so.

Activities:

- Track what is on screen / currently active
- Track previously used processes (that could be reactivated by the user)
- Manage App destruction by a user and return to previously active activity
- Provide user-flows between Apps e.g. Share

An activity can be implemented as a subclass of `Activity` class.

### Services

A general-purpose entry point, keeps App running in backround.

Performs long-running operations and remote process work.

No UI, but *can* manage media and streams e.g. music, network, etc.

An Activity can start and bind to a Service in order to interact with it.

#### Started Services

Stay running until work is completed.

A UI-interactive App will be prioritized to keep running; Background Services are generally non-interactive, so could be killed if RAM is needed.

#### Bound Services

Another App or Service has requested a service to start-up, so the spun-up service is Bound to the parent that started it.

Bound Services are maintained at the same priority level (interactive or background) as the App or Service it is bound to.

Good side effects include ability to set notification listeners, live wallpapers, and much more.

See the [Services Developers Guide](https://developer.android.com/guide/components/services) for more.

### Broadcast Receivers

Enables system to deliver events to App outside of user flow.

System-wide broadcast announcements are received by all Apps even if not currently running.

Apps can initiate broadcasts.

Status Bar notify area has Broadcast Receivers.

The BroadcastReceiver class delivers broadcasts as Intent objects.

### Content Providers

Manages shared app data sets, stored in many persistent-storage types.

A fine-grained security model allows controlling what Apps have access to the persistent data.

Temporary authorization grants (URI Grants) are made depending on these security permissions.

The `ContentProvider` class must implement APIs enabling other Apps to perform transactions.

See the [Conent Providers Developers Guide](https://developer.android.com/guide/topics/providers/content-providers)

Any App can start any other App Component. The example given was your app leveraging an existing Camera App, so your App doesn't have to implement the Camera function, just ask the existing Camera App to return a photo when done.

Android Apps do *not* have a single entry point e.g. `Main()` function.

### Activating Components

An `Intent` is used to activate Activities, Services, and Broadcast Receivers.

An Intent is asynchronous and binds components to each other at runtime.

Intent objects request an action from other compeonts, regardless of who owns the component.

Activities can return results as an Intent object, which could contain a URI pointing to a containing object/item.

ContentProvider is not activiated by Intent objects, rather when targeted by ContentResolver.

ContentResolver is the go-between for ContentProvider, adding abstraction.

Activating types of Components:

1. Pass an `Intent` to `startActivity()` or to `startActivityForResult()`
1. Use `JobScheduler` (API 21+) or pass an `Intent` to `startService()` and then to `bindService()`
1. Initiate a Broadcast with `sendBroadcast(intent)` or `sendOrderedBroadcast(intent)` or `sendStickyBroadcast(intent)`
1. Query a content provider with a `query()` "on a" `ContentResolver`

Using [Intents and Intent Filters](https://developer.android.com/guide/components/intents-filters)

## The Manifest File

Must be at the root of the app project directory: `AndroidManifest.xml`

- Declares all components, including Activities, within an App
- ID's user permissions required by the App
- Minimum API Level rqeuired by App
- Hardware and Software features used/required by App (Camera, BTLE, etc)
- List of other APIs the App needs to be linked against (meaning what?)

All App components must be declared using Elements (some examples):

- `<application android:icon...>` Icon ID'ing the app
- `<activity android:name_fqdn android:label...>` Class name of Activity subclass and user-visible label for it e.g. "Camera"
- `<receiver>` For Broadcast Receivers
- `<provider>` For content providers

### Component Capabilities

*Note*: When starting a service with an Intent, make sure it is an eplicite Intent. Starting with an implicit Intent is a security vulnerability. With API 21+, calling bindService() on an implicit intent throws an Exception.

Intent Filters: Include an `<intent-filter>` to set Activity Capabilities, which allows the App to respond to intents from other APps.

Declare intent filters as a child when declaring the Components.

Enables the App to start an Activity that creates a smooth user interaction like in the e.g. opening a new Email from the Email app.

### Declaring App Requirements

A profile for types of devices supported by the App.

Declared alongsite the software requirements in manifest file.

System does not use the info, but external services read them for filtering purposes.

Declares API Level necessary to support the App.

Build.Gradle contents:

```sh
android {
  ...
  defaultConfig {
    ...
    minSdkVersion 26
    targetSdkVersion 29
  }
}
```

When Gradle builds, entries in the build.gradle file override (and over write) these properties if they are in the Manifest File.

Attribute `required` can be set to true, or false if the dependency is optional.

Check out the [Device Compatibility](https://developer.android.com/guide/practices/compatibility) Document.

## App Resources

Code, images, audio files, UI components, and more are part of App Resources.

Enables updating at the component level instead of the entire App.

SDK Build Tools define unique IDs to ref Resources from App Code, etc, defined in XML.

Resource IDs are assigned names.

Alternate Resources can be defined, to support multiple device configurations.

File system location: `res/*` e.g. `res/values-fr/` for French String Values.

User's language settings are set this way.

There are qualifiers that are strings that enable capabilities like auto-rotation UI layout changes.

Device Configuration and [Providing Resources](https://developer.android.com/guide/topics/resources/providing-resources)

Product-Quality App [Guide to App Architecture](https://developer.android.com/topic/libraries/architecture/guide)

## Additional Resources

[Develop Apps with Kotlin](https://www.udacity.com/course/ud9012)

## Things I Want To Know More About

[ ] How to accept user input and gestures.
[ ] How to interact with externally connected devices.
[ ] How to leverage Bluetooth.

## References

Android developers guide to [Android Fundamentals](https://developer.android.com/guide/components/fundamentals)

*Note*: Additional Resources are witin the above referenced document.

## Footer

Back to root [Readme](../README.md)
