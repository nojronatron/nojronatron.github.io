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
- Anonymous Auth: Trial-based auth helps convert lookers to users through simple conversion.

## Firebase Auth with ID Platform

- Optional.
- Adds new features to Firebase Auth.
- No migration necessary.
- Includes SAML and OpenID Connect providers support.
- Enterprise-level.

## Usage Limits

- Spark Plan: No cost. 3k daily active (unique) users for Email, Social, Anonymous, and Custom auth types.
- Blaze: Pay as you go.

## WebDev Simplified Setup Overview

Source: [WebDev Simplified: Crash Course with Firebase and Routing](https://www.youtube.com/watch?v=PKwu15ldZ7k&ab_channel=WebDevSimplified).

1. Create Firebase Auth Projects: One for Dev, one for Production (if needed).
1. Create your Firebase Auth App within the Project to get the 'firebaseConfig' data.
1. Create ReactApp.
1. Setup an ENV file and add all 'firebaseConfig' data there. Prefix all Env keys with 'REACT_'.
1. Install 'firebase' using NPM.
1. Add a firebase.js file, import firebase/app and firebase/auth.
1. Add a const firebase.initializeApp and use process.env.REACT_NAME_OF_EACH_ENV_ENTRY to load the settings. Export as default.
1. Create a Signup.js React functional component. This page should include the ability to Register using a link or Login using an on-screen Form. Include a password confirmation input too! Don't forget a Submit button with value 'Sign up'. One way to grab data from Forms is to `import {useRef} from 'react'` and assign Refs variable names so React can use them. useRef variables can be referenced using `refName.current.value`.
1. Create a folder called 'context' to store Context so the authentication can be used anywhere within the ReactApp.
1. Create an AuthContent.js React Functional Component. Assign `const AuthContext = React.createContext()` to allow wrapping the function export 'children' within an AuthCotext.Provider tag. (16:46 minutes into video). There is more setup here where useState is utilized to store the AuthProvider is set up.
1. Import firebase/auth into AuthContent.js. Add a signup function using auth.createUserWithEmailAndPassword(). The function will now return currentUser and signup functions.
1. Import contexts/AuthContext into the Signup React Functional Component.
1. Ensure the entire App (inside App.js return() statement) is wrapped with `<AuthProvider>`.
1. Validate user inputs! Exit out of a handleSubmit function if the input validation fails, and return a helpful error message (`return setError('Passwords do not match')`).
1. Ensure rendering doesn't happen until Firebase can return with the user info. There is a lot to this, including use of useEffect and useState.
1. Import BrowserRouter (a react-router-dom component) to App.js, and include 'Switch' and 'Route'. Router component will live inside the App rendered Container, and AuthProvider will live inside of the parent Router component.
1. Enable routes by adding `<Route path='/path' component={component} />` and wrapping them all with `<Switch>`.
1. Create a Login component that is A LOT like the Signup Component, except will leverage wrapped Login function from Firebase Auth component.
1. Use ReactRouter's `<Link>` component to enable linking text from one page (e.g. Login) to another (e.g. Signup).
1. Leverage 'useHistory' from React Router to 'push' to a specific page (or '/') as a way to redirect after registration, login, or logout.
1. Create a profile (dashboard) with a new React Functional Component. Replicate the work done in the login/register pages but only include a Logout button, and instead of displaying a Form for user to enter data, use elements to display data about the currently logged on user (`const { currentUser } = useAuth()`).
1. Optionally configure a link to update the user profile that `<Link to='/update-profile'>Update Profile</Link>` using React Router's 'Link' component.
1. Create a custom component called 'PrivateRoute.js'. It's a new React Functional Component. Export a function `PrivateRouter({ component: Component, ...rest })` that just returns `<Route {...rest}></Route>` and a `render=` that captures the arrow function that checks for 'currentUser' to render component that got us here, otherwise redirect (via React Router) to the Login page.
1. At the bottom of the Log In page, add a div to contain a link to 'forgot password' page.
1. Create a Route for Forgot Password in the Route list in App.js.
1. Create a new React Functional Component `ForgotPassword.js` and copy 'Login' component code (except the password expressions and variables), update text to set 'Forgot Password' context for the user, and implement a wrapper function `resetPassword(email){}` that just returns `auth.sendPasswordResetEmail(email)`.
1. Complete the Profile/Dashboard page, and utilize `useAuth()` hook to allow Email and Password changes.

## Sign-in User To An App

1. Get auth credentials from user (UN+PW or OAuth Token).
1. Pass credentials to Firebase Authentication SDK.
1. Firebase backend services verify credentials and return response to client.

### User Profiles

After authentication:

- App has access to user's basic profile data.
- Access controls can be applied to app and other Firebase products.
- Auth Token can be used to authenticate to your app's backend services.

## Verify ID Tokens

A custom backend server can verify a user's Firebase Auth Token:

1. Front-end app verifies user and logs them in.
1. Front-end app opens a connection to the back-end using HTTPS.
1. Back-end server receives the user's ID token and verifies its authenticity to get the user's UID.
1. Back-end server uses the UID to securely ID the currently signed-in user.

[Verify ID Tokens](https://firebase.google.com/docs/auth/admin/verify-id-tokens) in Firebase Authentication.

### On the Back End (More Info)

1. Setup Firebase with a Google Application Credential (json file) and Firebase Project ID. Use DotEnv for example.
1. Install firebase-admin (I used ^11.4.1).
1. Implement middleware that imports firebase-admin, dotenv (for example) and setup a 'serviceAccount' variable that requires the Google App Creds.
1. Middleware: `admin.initializeApp({ credential: admin.credential.cert(serviceAccount)});`
1. Middleware: Implement a 'getAuthToken(req, res, next)' function that gets the 'Bearer token', and calls 'next();` at the end (as middleware does).
1. Middleware: Implement a 'checkAuthentication(req, res, next)' function that calls 'getAuthToken' then within a try-catch uses `admin.auth().verifyIdToken(authToken)` to validate the token then return 'next()' or an error (if 'catch(error)' is executed, then setting status code 401 and an error message i.e. 'unauthorized') else set 200 like status code.
1. On each path that requires authentication, insert 'checkIfAuthenticated' exported module function in the middleware, so Express will disallow or authorize access to the code next in the middleware chain.

Optional: Use and refresh session cookies when 'checkIfAuthenticated' passes, otherwise expire the cookie.

## Implementation - FirebaseUI Auth

1. Setup sign-in method(s): Firebase console configuration; setup OAuth redirect URL.
1. Customize sign-in UI: Set FirebaseUI options (or fork OSS and customize from there).
1. Perform Sign-in Flow: FirebaseUI Library configures sign-in methods support and flow.

## Firebase JS SDK 9 Setup

### Overview Video Notes

Generally:

- For dev/test, if using a local Auth Emulator, it must be running on the correct port else an error will be returned.
- Users that are not already registered must be added manually or via use of Email validation flows (provided by FireBase or can be customized).
- User UUID is guaranteed to be unique regardless of login method, and is provided as a User field that your App will have access to.

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

Running a local emulator is optional, but can serve as a local dev & test platform without relying on a 'production' Firebase Auth App instance or setting up a second app.

When starting the emulator(s) (firebase emulators:start):

- The latest code is auto-downloaded.
- A listing of enabled Emulators, ports, and links to their UIs: http://ip:port.

*Note*: Left off here.

## Authorized Domains

In the Firebase Auth project, defaults will be entered for you.

For development, localhost will be allowed.

For production, localhost should be deleted!

## Using Google Auth

1. Add Firebase to the JS project if not already.
1. Enable Google as sign-in provider to Firebase Project (a new public-facing project name will be added and a Project Support Email will be required).
1. Implement [Google Sign-in Flow](https://firebase.google.com/docs/auth/web/google-signin) using Firebase SDK into the project.

### Implement Google Sign In Flow

1. Create a Google Provider object that imports GoogleAuthProvider from firebase/auth, and calls 'new GoogleAuthProvider()'.
1. Optional: Add OAuth 2.0 scopes using `provider.addScope(googleapis.com/my_scope)`.
1. Optional: Localize OAuth flow to user's preferred language.
1. Optional: Specify custom OAuth provider params to send with OAuth Request: `provider.setCustomParameters({ 'key': 'value' })`.
1. Use the Google Provider Object to authenticate the user with Firebase. A Pop-up can be used or a redirect to the sign-in page (redirect preferred on mobile).
1. Call `getRedirectResult(auth)` to acquire the provider's OAuth token when the page loads.

### Google ID OAuth 2.0 Scopes

Check out [OAuth 2.0 Scopes for Google APIs](https://developers.google.com/identity/protocols/oauth2/scopes)

### Notes About Google Sign In Flow using Nodejs

Firebase documentation states this sign-in flow must be handled manually:

1. Implement sign-in flow to get user's Google ID token.
1. Build a Credential Object using Google ID Token.
1. Call `signInWithCredential(auth, credential)`... (more code here so see the web link) to perform login and handle any error.

Overall:

- Integrate the Google OAuth and call signInWithRedirect() which could return a promise.
- Leverage getRedirectResult either in the custom authentication context (leveraging firebase-auth) or at the login button handler.
- When calling 'signInWithRedirect(auth, provider)', return the result from 'getRedirectResult(auth)' to get a 'credential' and/or a 'token' in return.
- Acquire Bearer Token elsewhere in the front-end app by calling `currentUser.getIdToken()` where 'currentUser' is imported from Firebase Auth.
- When assembling a Bearer Token, concatenate 'Bearer ' with the result of currentUser.getIdToken() (template literal works).
- Add a Headers field `{ Authorization: Bearer {token} }` and server will parse it, validate with Firebase Auth, then return an Authorized response.

*Note*: Bearer token appears to be stored in local browser's firebaseLocalStorage (browser LocalStorage) at: value > stsTokenManager > accessToken.

## Resources

- [Firebase Authentication Google Docs](https://firebase.google.com/docs/auth).
- [OAuth 2.0 Scopes for Google APIs](https://developers.google.com/identity/protocols/oauth2/scopes).
- [Google Sign-in Flow](https://firebase.google.com/docs/auth/web/google-signin).
- [firebase docs emulator connect authentication web version 9](https://firebase.google.com/docs/emulator-suite/connect_auth#web-version-9).
- [install and configure](https://firebase.google.com/docs/emulator-suite/install_and_configure) Firebase Auth Emulator.
- [Firebase Docs Auth Web Start](https://firebase.google.com/docs/auth/web/start).
- [Verify ID Tokens](https://firebase.google.com/docs/auth/admin/verify-id-tokens) in Firebase Authentication.
- [WebDev Simplified: Crash Course with Firebase and Routing](https://www.youtube.com/watch?v=PKwu15ldZ7k&ab_channel=WebDevSimplified).

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root README](../README.html)
