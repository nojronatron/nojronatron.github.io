# Using Cookies with Express

## Table of Contents

- [Overview of Cookies](#overview-of-cookies)
- [Cookie KVP and Attributes](#cookie-kvp-and-attributes)
- [Cookies and Authentication](#cookies-and-authentication)
- [Other Means of Tracking](#other-means-of-tracking)
- [SameSite Key](#samesite-key)
- [Important Cookie Considerations](#important-cookie-considerations)
- [Cookie Parser](#cookie-parser)
- [Cookie Gotchas](#cookie-gotchas)
- [Resources Used For These Notes](#resources-used-for-these-notes)
- [Footer](#footer)

## Overview of Cookies

Cookies are just Key-Value Pairs with some additional Attributes that define when and where the cookie can be used.

When a server sets a cookie with a reply to a client (user agent) request, the user agent stores that Cookie and sends it back to the server on its next request. The idea is to store state information between user agent and server, enabling session-tracking capability.

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
- Non-essential cookie use and storage will require _consent_ in some countries (example: EU requires _informed consent_).
- User Agent (Browser's) privacy settings could block cookies.

Technically:

- A header field called 'set-cookie' is a name-value-pair with attributes storing expiration, domai, and flags.
- Older RFC created 'set-cookie2' field, but was soon deprecated and is no longer in use.
- Session-Cookie: In-memory cookie / Transient cookie. Only available while the user navigates a website and expire when the browser is closed. Do not have an expiration date identified in the header.
- Persistent Cookie: Has a specified (`Expires` or `Max-Age`) in the header. Referred to as 'Tracking Cookies'. Used for ads, and for tracking Authentication / logon state, to reduce logon prompts at every visit.
- Secure Cookie: Only allowed over a secured (https) connection. Enable the 'Secure' flag on the cookie to set it as secure only.
- HTTP-only Cookie: Cannot be accessed by client-side APIs (javascript). Thwarts XSS threats. Vulnerable to XST and CSRF attacks. Add 'HttpOnly' flag to enable it.
- Same-site Cookie: Defines if cookie should be restricted to 1st-party or same-site context.
- Third-party Cookies: Another domain's server sets a cookie on the web browser through the actual server (for example: Images or other components stored in the third-party's domain).
- Cookies can be _any size_ or length, there is no limit (see next point).
- Cookie Specifications require browsers to enforce limits: Up to 4 KB; 50 cookies per domain; 3k cookies total.
- Force-expiring a cookie server-side by sending 'Set-cookie' with an 'Expires' date in the past.
- Cookie _Attributes_ are one-way: Server to Client. When the browser returns with set cookies, the Attributes are not included.

## Cookie KVP and Attributes

When using Set-Cookie the primary article is a Key-Value pair. There are also attributes that could (should) be set:

- `cookie-name = String`
- `Expires = Date`
- `Max-Age = Number`
- `Domain = String: domainName.com`
- `Path = String`
- `Secure` (Sets the flag, otherwise not set)
- `HttpOnly` (Sets the flag...)
- `SameSite = String: Strict | Lax | None`

As mentioned elsewhere `SameSite=None` must be followed by `Secure` otherwise the Cookie will not get set by the User Agent.

### Supercookies

- Most cookies are attached to a specific website or domain such as 'me.mydomain.com'.
- Supercookies are attached to the _top level domain_ such as '.com' or '.net'.
- Present a security threat.
- Most browsers block by default.
- The 'Public Suffix List' mitigates Supercookie risks by providing list of domain name suffixes.
- Cookies that do not rely on HTTP, or instead rely on the browser cache mechanism.
- Not popular, usually blocked by default, and are not recommended.

### Zombie Cookie

- Placed on a browsing computer hidden outside of the web browser's cookie storage.
- Recreates an HTTP cookie as a 'regular cookie' after original cookie is deleted.
- Often stored in Flash Local Shared Objects, HTML5 Web Storage, and sometimes server-side storage locations.
- Relies on javascript code stored in a long-term location that will automatically recreate deleted cookies, and re-launch itself in other areas of memory.

### Cookie Usage

Session Management:

- Shopping cart/basket (although today that is usually a database-provide feature).
- Requires a Session Identifier: Random unique string of characters. Browser will send-back that same cookie every time the user visits the website, and the server can then 'know' this is the same user and therefore session state might be associated with that user.
- User logon (authentication) and/or authorization.

### User Logon Process

1. User opens the Logon page (Server-side rendered: The server also sends a unique Session ID to the user agent within a Cookie).
1. When user successfully logs in and cookie is sent back to the server by the user-agent.
1. Server processes the returned Session ID via the cookie.
1. The user agent supplies an Authorization header and, if validated, the server sets a new cookie granting access to authorized resources.

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
- Must be specifically sent with an HTTP request (wheras Cookies are sent automatically by the User Agent).

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

## SameSite Key

'SameSite' is an Attribute.

Possible values:

- Strict: Mitigates XSRF attacks,.
- Lax: Enables CORS allowed only for safe (GET) requests and 3rd party cookies are rejected.
- None: Allows 3rd party cookies, and most browsers require the 'Secure' flag to be set too.

### Lax

- Cookies NOT sent on normal cross-site subrequests.
- Cookies ARE sent when user navigates to the origin site (e.g.: following a link).
- Is default value if SameSite not specified at all.
- Browser compatibility varies - None might be default which requires `Secure=true` else Cookie is ignored.

_Note_: Browsers might implement 'Lax-Allowing-Unsafe' to enable cross-site unsafe requests within a short timeframe, therefore a value _should_ be set by the developer.

### Strict

- Cookies _only_ sent in 1st-party context.
- Any 3rd party requests will not include Strict cookies.

### None

- Cookies sent in ALL contexts including 1st-party, and cross-site.
- _Requires_ `Secure` attribute to be set else cookie will be blocked.

## Important Cookie Considerations

- Privacy concerns, especially with non-secure sessions.
- Cookies are not guaranteed secure.
- Properly identifying a user should be more than an ID, rather: User ID, Computer ID, and Web Browser ID.
- Cookies are not 100% perfect at identifying a specific user (multiple accounts, multiple computers or browsers, multiple sets of cookies, etc).
- SameSite should be explicitly set with a value to avoid browsers applying some `SameSite=Lax` or `SameSite=None` without `Secure` flag, which will break things.

## Cookie Parser

1. Install Cookie-parser: `npm install cookie-parser`
1. Load in Express (JS): `const cookieParser = require('cookie-parser')`
1. Initialize as middleware function: `app.use(cookieParser())`
1. Acquire a specific cookie from a user agent request: `const receivedCookie = req.cookies["key"]`
1. Set a cookie in user agent browser via a Response: `res.cookie('keyString', 'valueString', { options })`
1. Set options as a destructured object (see below).

```javascript
const options = {
  maxAge = 1000 * 60 * 15, // 1 sec * 60 sec * 5 => 5 minutes
  httpOnly: true, // only useable by the server
  signed: true // only include if the cookie is signed
};
res.cookie('name', 'value', options);
res.send('');
```

### Signed Cookies

1. Prefixed with `s:`.
1. Include a secure string to sign them.
1. Set `signed: true` property on the cookie options.

### JSON Cookies

1. Prefixed with `j:`. Parsed using JSON.parse.
1. Return parsed JSON value: `cookieParser.JSONCookie(String)`.
1. Iterate over the keys to return an object: `cookieParser.JSONCookies(Array[cookies])`.
1. Signed JSON cookies can also be parsed: `cookieParser.signedCookie(String, Secret)`. Signature must be valid, if not, returns `false`.
1. Iterate over the keys to check for signed values: `cookieParser.signedCookies(cookies, Secret)`. Secret can be an array of Secrets or a single Secret String. In either case, all Secret(s) will be used to 'unsign' each cookie in signedCookies.

Review the expressjs cookie-parser documentation for a few more details about JSON Cookies.

## Cookie Gotchas

See StackOverflow [set cookie using express framework](https://stackoverflow.com/questions/16209145/how-can-i-set-cookie-in-node-js-using-express-framework), where a user noted that Fetch didn't seem to respect cookie setting. Fetch options must be set in order to work around the problem.

You will not see a SecureCookie, this is on purpose. Be sure to use a valid secret to sign cookies, and utilize `req.signedCookies` to retrieve them.

## Resources Used For These Notes

- Wikipedia's entry on [HTTP cookies](https://en.wikipedia.org/wiki/HTTP_cookie).
- Express [Cookie-Parser](https://github.com/expressjs/cookie-parser) on Github.com.
- StackOverflow [set cookie using express framework](https://stackoverflow.com/questions/16209145/how-can-i-set-cookie-in-node-js-using-express-framework).
- Web.dev blog [Same Site Cookies Explained](https://web.dev/samesite-cookies-explained/).
- Mozilla.org [MDN Web HTTP Headers Cookies](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cookie).
- Mozilla.org [MDN Web HTTP Headers Set-Cookie](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie).

## Footer

More [about cookies](./about-cookies.html) notes I've written while researching.

Return to [Conted Index](./conted-index.html).

Return to [Root README](../README.html).
