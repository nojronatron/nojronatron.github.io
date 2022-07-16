# Read Class 38

Intent Filters, and Implicit and Explicit Intents

## Resources

[Intent Filters](https://developer.android.com/training/basics/intents/filters)

[Implicit vs Explicit Intents](https://developer.android.com/guide/components/intents-filters#Types)

## Intent Filters

Action requests can be set up so that your App appears as a handler for an Action.

E.g.: When tapping 'share' a list of apps appears to select from (Facebook, Twitter, Messenger, etc) - your App can be on that list by supporting `ACTION_SEND`.

Allowing other Apps to do this requires adding `<intent-filter>` to the `<activity>` element in the manifest file.

Ensure your implemented Intent Filters are *specific*.

Intent Filter Criteria are:

- Action: ACTION_SEND or ACTION_VIEW. Use the full-name of these in the action element.
- Data: Use 1 or more attributes in the element. E.g. MIME type or URI prefix, URI Scheme, or combination.
- Category: Characterizes the activty handling on the Intent. Not often used. Most Implicit Intents are defined with CATEGORY_DEFAULT.

See the code in [this doc](https://developer.android.com/training/basics/intents/filters) for simple examples of the above implementations.

Incoming Intents specify:

- 1 Action
- 1 Data type

Multiple instances of action, category, and data elements can be declared within each intent-filter.

Separate mutually exclusive action:data pairs with separate intent filters.

Read-in the properties of the incoming Intent to determine an action to take:

Call getIntent() within onCreate() or onStart() lifecycle methods.

Use 'setResult()' to return a result to the activity that invoked this Activity.

- Call finish() when done.
- Set a result code (required when using setResult) such as an integer e.g. something greater than 0.

## Implicit vs Explicit Intents

Explicit: Specify which App will satisfy an Intent.

- Can supply the target App's package name, or fully-qualified component class name.
- Typically used to start a component in this App.

Implicit: No specific component is named.

- Declares genera action to perform.
- Allows component for another App to handle it.
- E.g.: Can be used to request some other App handles a request from within your own App.

The System is responsible for managing Implicit and Explicit Intent operations.

Compares Intent content to Intent Filters in the Manifest File of the 'other App' on the device.

- When more than one Intent Filter matches, System displays a dialog so a user can select one.
- When another App has NO Intent Filters within the Manifest File, then the Activity *must* be launched from *within* that App.

When using a Service: *Always* use an *explicit* Intent, for security reasons.

## Footer

Return to [Root README](../README.html)
