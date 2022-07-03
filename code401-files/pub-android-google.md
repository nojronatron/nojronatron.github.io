# Reading Notes: Class 34

Google's App Publishing Guide

Two primary tasks developer must take to publish an app:

1. Prepare Application for release.
1. Release Application to Users.

## Prepare for Release

Apps must be published with the *Android App Bundle* on Google Play.

Apps larger than 150MB now supported via specific delivery tools.

Configure and Prepare for Release:

- Remove Log calls from code.
- Remove `android:debuggable` attribute from manifest file.
- Provide values to `android:versionCode` attribute in `<manifest>` element.
- Provide values to `android:versionName` attribute in `<manifest>` element.
- Specify the API Level Requirement for your app's build.gradle file: 'minSdkVersion' and 'targetSdkVersion'.
- `./jni` location: Only Android NDK files.
- `./lib` location: Only 3rd party libraries.
- `./src` location: Your App Source files.
- Cleanup `./res`, `./lib`, and `./res/raw` directories of test libraries, private or proprietry data, and raw asset or static files.
- Update Gradle build to use 'release' build type and allow only permissions necessary for a published app.
- Thoroughly [test](https://developer.android.com/tools/testing/what_to_test) the release version on at least 1 target handset device and 1 tablet device [versioning your app](https://developer.android.com/tools/publishing/versioning).
- Address compatibility issues like screen size, multi-screen, tablets... use an Android Support Library to help esp with older devices.
- Update all App Resources e.g. multimedia and graphics files within, or staged on productiono (delivery?) servers.
- Prepare remote servers and services the app depends on, through security patches, configuration, and reliability and scalability configurations.
- Get a Private Signing Key/Crypo Keys for App (and any Bundle, if applicable). Will need upload Key and KeyStore, configure AppSigning in the GPStore, Sign the App with the key then *sign the UploadKey with your signing key*, and create an Upload Certificate (for versioning). Use Android App Bundle for [help](https://developer.android.com/studio/publish/app-signing).
- Create an App Icon.
- Create an EULA to protect your person, org, and intellectual property.
- Uploading requires checking the APK file, and possibly using [Google's Internal Test Stack](https://support.google.com/googleplay/android-developer/answer/3131213) to test the App before pulishing.
- Upload the app: Every upload requires revving the app, see [Manage App Updates](https://developer.android.com/guide/app-bundle/configure#manage_app_updates) for details.

A signed '.apk' file will be made available for distributing to users.

## Release App To Users

Usual: Release via an App Marketplace e.g. Google Play.

Alternate: Release via your own website or sending the app (APK?) direct to the intended user, or via another Marketplace.

## Release via Google Play

Pub, sell, and distribute your Android Apps, globally.

Developer Tools come with this release avenue.

Analysis tools provided via Google Play also.

Three Major Steps:

1. Prepare promo materials: Screenshots, videos, graphics, and promo text.
1. Configure options and upload assets: Countries, languages, price to charge, app type, category, content rating. Publication can be in *draft* while completing these substeps.
1. Publish Release Version: Click Publish, wait a few minutes, and done!

## Release Through a Website

Private or enterprise server-based release is supported.

Must still prepare app "the normal way" (see above or the "Publish Your App" reference link).

Hose the release-ready APK file on the website and provide a download link to users.

When the Android System receives an APK file it begins the installation process (depending on user settings, especially "unknown sources").

Down-side: Monetization requires building your own transaction-tracking mechanisms, whereas the Google Play Store method does this for you. Also, lack of enforcement of the "Licensing Service", which would prevent users from installing your app in an unauthorized way (or region, or other set of conditions).

## User Opt-in For Unknown Apps and Sources

API level 25 and 26 changed how this setting is made at the user device, and the terminology changed from "Unknown Sources > Allow Single Install of Unknown App" to "Install Unknown Apps > {source}".

In any case, the idea is to controll installation of applications from *non first-parties*.

## References

Android Studio User Guide [Publish Your App](https://developer.android.com/studio/publish)

More info on publishing to [Google Play](https://developer.android.com/distribute/googleplay)

## Footer

Back to [Root README](../README.html)
