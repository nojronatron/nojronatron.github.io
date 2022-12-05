# Using Cookies with Express

## Overview of Cookies

- Web-server created data stored on user's device by the web browser.
- Multiple cookies can be placed during a user's browsing session.
- Enable storage of stateful information.
- Can track browsing activity of the user including button clicks and other events.
- Data previously entered into forms.
- Authentication cookies used to make a logon 'sticky', identifying which authenticated account is being used.
- Tracking cookies compile long-term data about a browser's usage and traversal through the web.
- Non-essential cookie use and storage will require *consent* in some countries (example: EU requires *informed consent*).

## Cookie Parser

## Cookies and Authentication

Users need to authenticate themselves, via a logon page or functionality.

Authentication cookies are usually encrypted.

Risks of decrypting an Auth Cookie include:

- Exposing user's PII.
- Exposing user's login credentials.
- Allowing unauthorized access through stolen information.
- Enabling cross-site scripting.
- Enabling cross-site request forgery.

