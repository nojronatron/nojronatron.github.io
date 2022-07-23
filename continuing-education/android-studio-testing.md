# Testing Android Studio Applications

## Overview

Unit testing your code implementations that are dependent on Android platform libraries requires one or more of the following:

- Publicly available APIs for each class that is implemented
- Mocking
- Faking
- Test Doubles

## What To Unit Test

- ViewModels or presenters
- The Data Layer especially repositories (use Test Doubles to assist with this)
- Platform-independent layers e.g. Domain layer
- Utility Classes
- Edge cases including: boundary conditions; network connection errors; corrupt data e.g. malformed JSON; disk/repository states e.g. 'full storage' when saving to file; Object re-creation e.g. when device is rotated.

## UI Tests

- Screen UI Tests: Speicfic user interactions in a single screen
- User Flow Tests E.g. Navigation Tests: Cover the most common paths at bare minimum

## Specialized Tests

- Screenshot tests
- Tests categorized by purpose e.g. regression, accessibility, and compatibility

## What To AVOID Testing

Avoid testing frameworks your code depends on (these should already be fully tested with accessible results, etc).

Avoid unit-testing Framework Entry Points such as Activities, Fragments, or Services.

- None of these should have business logic in them anyway (if they do, the logic needs to be refactored out into a separate custom library or class).
- If testing is required, use Espresso to test them.

## References

Developer Android [Build Local Tests](https://developer.android.com/training/testing/local-tests)

Stack Overflow [Writing Instrumentation Tests](https://stackoverflow.com/questions/28960898/getting-context-in-androidtestcase-or-instrumentationtestcase-in-android-studio/29063736#29063736)

Android Studio Project [Site](https://sites.google.com/a/android.com/tools/tech-docs/unit-testing-support)

Android Developer [What To Test in Android](https://developer.android.com/training/testing/fundamentals/what-to-test)

Android Developer [Using Test Doubles in Android](https://developer.android.com/training/testing/fundamentals/test-doubles)

Android Developer [Testing Codelabs](https://developer.android.com/codelabs/advanced-android-kotlin-training-testing-basics)

## Footer

Back to [Index](./readme.html)
