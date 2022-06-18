# Reading Notes - Android Fundamentals

## Introduction

Kotlin, Java, and C++ can be used to write Android apps.

APK: Android App Bundle or Package file.

Android uses APK to install apps via the APK, and is required at runtime.

Android App Bundle: AAB file, `.aab` extension, contains Android Project files and metadata that the runtime does *not* depend on.

AAB files are the *publishing format* and are not installable.

Projects hosted on Google Play deploy optimized APK's that contain resources and code that an Android device will need when requesting App installation.

The Android OS:

- Is a Linex-based OS
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

Activities can interact if given permission to do so.

Activities:

- Track what is on screen / currently active
- Track previously used processes (that could be reactivated by the user)
- Manage App destruction by a user and return to previously active activity
- Provide user-flows between Apps e.g. Share

An activity can be implemented as a subclass of `Activity` class.

### Services

A general-purpose entry point.

Keeps App running in backround.

Performs long-running operations and remote process work.

No UI, but *can* manage media and streams e.g. music, network, etc.

An Activity can start and bind to a Service in order to interact with it.

Started Service: Stays running until work is completed. A UI-interactive App will be prioritized to keep running; Background Services are generally non-interactive, so could be killed if RAM is needed.


## The Manifest File


## App Resources


## Additional Resources


## References

Androide developers guide to [Android Fundamentals](https://developer.android.com/guide/components/fundamentals)

## Footer

Back to root [Readme](../README.md)
