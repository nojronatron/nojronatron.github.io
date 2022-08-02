# Class Reading Notes - Amplify and Cognito

Read the sections on Getting Started and Sign In.

## References

[AmplifyDocs on Authentication](https://docs.amplify.aws/lib/auth/getting-started/q/platform/android/)

## Amplify Auth Category

Android SDK API Level 16 or higher required.

Provision authentication resources in Amplify

1. Begin with: `amplify add auth`
1. Answer questions about security configuration (default), signing type (e.g. 'Username'), and Advanced Settings (not covered here, yet).
1. Finish with: `amplify push`
1. Add a dependency to app:build.gradle, dependencies section: `implementation 'com.amplifyframework:aws-auth-cognito:1.36.1;`
1. Get to coding!

## Coding With Amplify Auth

Add the auth plugin:

```java
Amplify.addPlugin(new AWSCognitoAuthPlugin());
Amplify.configure(getApplicationContext());
```

Check current Auth session (could be run from Main Activity 'onCreate()' method):

```java
Amplify.Auth.fetchAuthSession(
  result -> Log.i("AmplifyQuickstart", result.toString()),
  error -> Log.e("AmplifyQuickstart", error.toString())
);
// code snippet care of docs.amplify.aws
```

AuthSession has a property 'isSignedIn' that is used to determine if user is ...signed in... or not. In the above code example from docs.amplify.com, no user will be signed in.

## Sign In using Auth

Dev Prerequisites: Previous subsections must be completed.

User Requirements: Username, password, and email address for registration.

```java
AuthSignUpOptions options = AuthSignUpOptions.builder()
    .userAttribute(AuthUserAttributeKey.email(), "my@email.com")
    .build();
Amplify.Auth.signUp("username", "Password123", options,
    result -> Log.i("AuthQuickStart", "Result: " + result.toString()),
    error -> Log.e("AuthQuickStart", "Sign up failed", error)
);
// above code snippet from docs.amplify.aws
```

The above code invokes the API to do the registration work.

User Confirmation is required before signin is allowed.

Confirmation Code will be sent to user's email ID, and that confirmation code must be added to the `confirmSignUp` call in code.

```java
// console/terminal window will output result of this call.
Amplify.Auth.confirmSignUp(
    "username",
    "the code you received via email",
    result -> Log.i("AuthQuickstart", result.isSignUpComplete() ? "Confirm signUp succeeded" : "Confirm sign up not complete"),
    error -> Log.e("AuthQuickstart", error.toString())
);
// above code snippet from docs.amplify.aws
```

A UI is necessary to allow a user to login with a registered username and password.

Once username and password have been entered, call the `signIn()` flow to authenticate and 'log in' the user.

```java
Amplify.Auth.signIn(
    "username",
    "password",
    result -> Log.i("AuthQuickstart", result.isSignInComplete() ? "Sign in succeeded" : "Sign in not complete"),
    error -> Log.e("AuthQuickstart", error.toString())
);
// above code snippet from docs.amplify.aws
```

## Other Authenticators in Amplify

Multi-factor Auth.

More later, but this will require running `Amplify Add Auth` again and answering 'Manual Configuration' during initial Q&A.

Of course, follow-up with `Amplify Push`.

## Footer

Return to [Root README](../README.html)
