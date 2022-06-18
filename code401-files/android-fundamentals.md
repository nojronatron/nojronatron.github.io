# Reading Notes - Android Fundamentals

## Overview

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



## References

Androide developers guide to [Android Fundamentals](https://developer.android.com/guide/components/fundamentals)

## Footer

Back to root [Readme](../README.md)
