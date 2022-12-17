# Google Firebase Authentication

"Provides backend services, easy-to-use SDK's, and ready-made UI libraries to authenticate users to your app." *[Firebase Authentication Google Documentation]*

## Overview

- Integrates with other Firebase Services.
- Supports OAuth 2.0 and OpenID Connect for custom back-end integration.
- MFA available in Firebase Auth with Identity Platform.
- Username + Password, and Federated providers like Google and Facebook.
- Supports mobile (iOS and Android) and web apps, C++ and Unity.

## FirebaseUI Auth

- Recommended for complete sign-in system.
- Handles UI flows for sign-in.
- UN+PW, Phone Number, Federated ID/Social.
- Mobile and Web drop-in solution.
- Account recovery and account linking supported.
- Customizable to app's visual style.
- OSS.

## Firebase SDK Auth

- Email + Password: Create and manage users, and handles pw reset emails.
- Federated ID Provider Integration: "Social auth" including Google, FB, Twitter, and GH.
- Phone Number: SMS-message based authentication.
- Custom Auth: Integrate existing system with Firebase Auth SDK.
- Anonymous Auth: Trail-based auth, helps convert lookers to users through simple conversion.

## Firebase Auth with ID Platform

- Optional.
- Adds new features to Firebase Auth.
- No migration necessary.
- Includes SAML and OpenID Connect providers support.
- Enterprise-level.

## Usage Limits

- Spark Plan: No cost. 3k daily active (unique) users for Email, Social, Anonymous, and Custom auth types.
- Blaze: Pay as you go.

## Sign-in User To An App

1. Get auth credetnials from user (UN+PW or OAuth Token).
1. Pass credentials to Firebase Authentication SDK.
1. Firebase backend services verify credentials and return response to client.

### User Profiles

After authentication:

- App has access to user's basic profile data.
- Access controls can be applied to app and other Firebase products.
- Auth Token can be used to authenticate to your app's backend services.

## Implementation - FirebaseUI Auth

1. Setup sign-in method(s): Firebase console configuration; setup OAuth redirect URL.
1. Customize sign-in UI: Set FirebaseUI options (or fork OSS and customize from there).
1. Perform Sign-in Flow: FirebaseUI Library configures sign-in methods support and flow.

## Firebase JS SDK 9 Setup

### Overview Video Notes

For dev/test, a local Auth Emulator must be running on the correct port else an error will be returned.

Users that are not already registered must be added manual, or to use Email validation flows (provided by FireBase or can be customized).

User UUID is guaranteed to be unique regardless of login method, and is provided as a User field that your App will have access to.

To programmatically create a user account:

- Create a new user leveraging createUserWithEmailAndPassword(auth, email, password).
- createUserWithEmailAndPassword will not only register a new user, but also log them in.
- UI *must* be updated according to 'authentication state' using 'onAuthStateChange' function.
- Logout is done using async function 'signOut'.

Best Practice: Use a Login State Monitor function that will return correct feedback to users on the login screen.

### Walk-thru with Code Samples

1. Add and Init Auth SDK.
1. Prototype and test with Firebase Local Emulator Suite (optional).
1. Sign-up new users.
1. Sign-in existing users.
1. Set an authentication state observer and get user data.

Source: [Firebase Docs Auth Web Start](https://firebase.google.com/docs/auth/web/start)

## Dev Setup and Management

Firebase Tools and Firebase-CLI are needed for enabling the firebase emulator environment.

- `npm install -g firebase-tools`
- `firebase login`: Launches a web-browser to authenticate to Google and allow Firebase-CLI access to Firebase project(s).
- `firebase init`: Asks a bunch of questions about the features to use, connecting the local project to an existing Firebase Project, what language to use (TS or js), and which emulator(s) to install. For authentication select the 'auth emulator'.
- Emulator install: `firebase init emulators`.

Documentation for [install and configure](https://firebase.google.com/docs/emulator-suite/install_and_configure).

### Local Auth Emul Config

- Auth Emulator Port: 9099
- Emulator UI enabled
- Emulator UI Port: (can allow app to choose any available)
- Edit the Firebase Configuration module (or at the top of your webapp code) to include 'connectAuthEmulator' function from 'firebase/auth'.

Note: Admin SDKs can be automatically connected using a ENV file. See [firebase docs emulator connect authentication web version 9](https://firebase.google.com/docs/emulator-suite/connect_auth#web-version-9) for details.

Final step to start the emulator processes:

- `firebase emulators:start`.

### File System Changes After Dev Setup and Emulator Install

Added:

- .firebaserc
- database.rules.json
- firebase.json
- functions/

Changed:

- package.json

### Emulator Startup Info

When starting the emulator(s) (firebase emulators:start):

- The latest code is auto-downloaded.
- A listing of enabled Emulators, ports, and links to their UIs: http://ip:port.

*Note*: Left off here.

## Resources

- [Firebase Authentication Google Docs](https://firebase.google.com/docs/auth)

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root README](../README.html)
