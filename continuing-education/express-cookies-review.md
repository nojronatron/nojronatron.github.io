# Using Cookies with Express

## Overview of Cookies

Generally:

- Magic Coookies: Packet of data sent to another computer, expected to be returned, unchanged.
- Lou Montulli, a browser developer at Netscape Communications, is credited with coining the term 'cookie' as related to web-brower and serve features.
- Web-server created data stored on user's device by the web browser.
- Multiple cookies can be placed during a user's browsing session.
- Enable storage of stateful information.
- Can track browsing activity of the user including button clicks and other events.
- Data previously entered into forms.
- Authentication cookies used to make a logon 'sticky', identifying which authenticated account is being used.
- Tracking cookies compile long-term data about a browser's usage and traversal through the web.
- Non-essential cookie use and storage will require *consent* in some countries (example: EU requires *informed consent*).

Technically:

- A header field called 'set-cookie' is a name-value-pair with attributes storing expiration, domai, and flags.
- Older RFC created 'set-cookie2' field, but was soon deprecated and is no longer in use.
- Session-Cookie: In-memory cookie / Transient cookie. Only available while the user navigates a website and expire when the browser is closed. Do not have an expiration date identified in the header.
- Persistent Cookie: Has a specified  (`Expires` or `Max-Age`) in the header. Referred to as 'Tracking Cookies'. Used for ads, and for tracking Authentication / logon state, to reduce logon prompts at every visit.
- Secure Cookie: Only allowed over a secured connection. Enable the 'Secure' flag on the cookie to set it as secure only.
- HTTP-only Cookie: Cannot be accesses by client-side APIs (javascript). Thwarts XSS threats. Vulnerable to XST and CSRF attacks. Add 'HttpOnly' flag to enable it.
- Same-site Cookie: Attribute 'SameSite', values: 'Strict' | 'Lax' | 'None'. Strict mitigates XSRF attacks. Lax enables CORS allowed only for safe (GET) requests, and 3rd party cookies are rejected. None allows 3rd party cookies, and most browsers require the 'Secure' flag to be set too.
- Third-party Cookies: Another domain's server sets a cookie on the web browser through the actual server (for example: Images or other components stored in the third-party's domain).
- Cookies can be *any size* or length, there is no limit (see next point).
- Cookie Specifications require browsers to enforce limits: Up to 4 KB; 50 cookies per domain; 3k cookies total.
- Force-expiring a cookie server-side by sending 'Set-cookie' with an 'Expires' date in the past.
- Cookie *Attributes* are one-way: Server to Client. When the browser returns with set cookies, the Attributes are not included.

### Supercookies

- Most cookies are attached to a specific website or domain such as 'me.mydomain.com'.
- Supercookies are attached to the *top level domain* such as '.com' or '.net'.
- Present a security threat.
- Most browsers block by default.
- The 'Public Suffix List' mitigates Supercookie risks by providing list of domain name suffixes.
- Cookies that do not rely on HTTP, or instead rely on the browser cache mechanism.
- Not popular, usually blocked by default, and are not recommended.

### Zombie Cookie

- Placed on a browsing computer hidden outside of the web browser's cookie storage.
- Recreates an HTTP cookie as a 'regular cookie' after original cookie is deleted.
- Often stored in : Flash Local Shared Objects, HTML5 Web Storage, and sometimes server-side storage locations.
- Relies on javascript code stored in a long-term location that will automatically recreate deleted cookies, and re-launch itself in other areas of memory.

### Cookie Usage

Session Management:

- Shopping cart/basket (although today that is usually a database-provide feature).
- Requires a Session Identifier: Random unique string of characters. Browser will send-back that same cookie every time the user visits the website, and the server can then 'know' this is the same user and therefore session state might be associated with that user.
- User logon (more later).

### User Logon Process

1. User opens the Logon page and the server sends a unique Session ID to the client within a Cookie.
1. When user successfully logs in and cookie is sent back to the server.
1. Server processes the returned Session ID in the cookie and can now recall the user has authenticated successfully, grantin access to authorized resources.

### Personalization Cookies

- Used to store user preferences, encoded into a cookie and sent back to the browser.
- Page personalization can be applied whenever the browser returns with a request containing that cookie.

### Tracking Cookies

- Collect visitors browsing and buying habits.
- Multiple tracking cookies can be placed in a browser.
- Data is offect collected, processed, and sometimes sold to bidding corporations.

## Cookies and Authentication

Users need to authenticate themselves, via a logon page or functionality.

Authentication cookies are usually encrypted.

Risks of decrypting an Auth Cookie include:

- Exposing user's PII.
- Exposing user's login credentials.
- Allowing unauthorized access through stolen information.
- Enabling cross-site scripting.
- Enabling cross-site request forgery.

### JSON Web Tokens

- Self-contained data packaet.
- Used to store user ID and Authentication data.
- Used in place of Session-Cookies.
- Must be specifically sent with an HTTP request (wheras Cookies are sent automatically).

### HTTP Auth

- Basic Access Authentication and Digest Access Authentication protocols.
- Browser stores and sends the credentials with every subsequent page request.
- Can be used to track a user.

### URL aka Query String

- Java Servlet and PHP Session features use this mode if Cookies are not enabled.
- Query strings have a uuid appended by the server to all links in a web page. Following a link allows the server to ID the user and maintain logon state.
- Similar to cookies.
- Arbitrary data chosen by the server.
- Required on every request.
- Web URLs appended with Query Strings, when shared, could have unexpected, undesirable results.
- Unable to manage same-user coming from different computing end-devices. Cookies can handle this, URL strings cannot.

### Hidden Form Fields

- Similar to URL Query String.
- Information is held in hidden Form Fields.
- Similar advantages and drawbacks to URL Query String.
- Information is sent as part of a POST Request Body (not a Cookie, not a URL).
- Copied URLs do not have encoded information in them.
- Request Body payloads are not as obvious to view as URL Query String.

### Window.Name DOM Property

- Empty with every 1st request.
- Does not automatically send data with every request.
- Cannot be easily sniffed and intercepted.

## Other Means of Tracking

- IP Address: Server knows the IP of every computer running a browser (or the proxy). However, public IP's are not 1:1 with personal computing devices, think NAT and Shared Public PCs.
- ETag: Cached in the browser and returned with subsequent requests for same resource. Server can repeat the ETag received by browser to persist it (use caching). ETags can be cleared manually at the Browser.
- Browser Cache: Server can set a javascript to return a unique identifier. Subsequent visits will cause Browser to pull file from cache instead of from the server, persisting the ID.
- Browser Fingerprint: Version, Screen res, OS etc, used to ID the website visitor. A viable alternative to ID User or Computer when Cookies are turned off. Relatively good unique identifier storing about 18 bits of information.
- Web Storage: Local Storage and Session Storage. Similar to Persistent Cookies and Session Cookies, respectively. Session Storage is tied to a specific Browser Window and Tab.

## Important Cookie Considerations

- Privacy concerns, especially with non-secure sessions.
- Cookies are not guaranteed secure.
- Properly identifying a user should be more than an ID, rather: User ID, Computer ID, and Web Browser ID.
- Cookies are not 100% perfect at identifying a specific user (multiple accounts, multiple computers or browsers, multiple sets of cookies, etc).

## Cookie Parser


## Resources Used For These Notes

- Wikipedia: [HTTP_cookie](https://en.wikipedia.org/wiki/HTTP_cookie).
- Express [Cookie-Parser](https://github.com/expressjs/cookie-parser) on Github.com.

## Footer

Return to [Conted Index](./conted-index.html).

Return to [Root README](../README.html).
