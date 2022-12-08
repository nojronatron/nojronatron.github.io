# Working with Auth0 With Express

A collection of notes for future review about implementing Auth0 server-side for an Expressjs app.

## Required Reading

[Auth0 Docs - Authentication API](https://auth0.com/docs/api/authentication#introduction)

## Requirements

1. Pick your technology. Client, Server, CLI, or other. Expressjs is listed among the options. Note: So is Java Spring Framework.
1. Allowed Callback URLs. Example: 'http://localhost:3000/callback'. Auth0 redirects the user after they have authenticated.
1. Allowed Logout URLs. Example: 'http://localhost:3000'. Auth0 redirects the user after they logout of Auth0.
1. Install 'express-openid-connect' module (maintained by Auth0).
1. Generate a 32-bit random hexadecimal secret using either `openssl rand -hex 32` or [GRC Password Generator](https://www.grc.com/passwords.htm).
1. Configuration of the OpenID Auth Router.

## Routing Considerations

- Should any static routes be protected by authentication?
- Will a '/profile' route bring-up a custom profile page for the logged-in user?

## Testing Considerations

- Thunderclient shows return data from Auth0 that can be used to start building a page or verifying output of routes.
- Using ThunderClient will show responses but does not have an interactive/rendering display so use the browser for interactive log-in activity.

## Application Settings

The most critical configuration items to set up:

- Name
- Domain nnnnnnn.us.auth0.com
- Client ID
- Client Secret
- Application Type: Determines what settings can be configured from dashboard. Code301 used "SPA".
- Token Endpoint Auth Method: None. POST enables the 'Client Credentials grant'.
- Allowed callback URLs. Should include dev, test, and deployed environment URL(s). Dev start => 'http://localhost:3000'
- Allowed logout URLs. Same as callback URLs but for expiring user's token.
- Allowed web origins. Defines allowed origins for cross-origin, device flow, and web message-response mode. Dev start => 'http://localhost:3000'
- Allowed Origins (CORS). Start with localhost for dev. Include *other* origins only if needed.

API Setting:

- Auth0 Management API: API Audience URL for System API (probably automatically configured).

Optional Settings:

- Description (this helps track your Apps).
- Application Logo. Default is Auth0 logo but can be redirected to an https page with your custom logo.
- Application Login URI: This is an unusual scenario. App must have a '/authorize' endpoint for Auth0 to call. Otherwise leave blank.
- Any other settings that were not already mentioned above should be left to them more secure setting option, or empty.

Always verify the Application's Advanced Settings, Endpoints has the correct entiries in them. If any are edited they will be pointing to a non-existing URL (or worse). Most of the time actual entries are already set by Auth0 during Application Setup:

- OAuth Authorization URL
- Device Authorization URL
- OAuth Token URL
- OAuth User Info URL
- OpenID Configuration
- JSON Web Key Set (WKS.json)
- SAML Protocol URL
- SAML Metadata URL
- WsFederation Metadata URL
- WsFederation Sign-in URL

## Client ID and Client Secret

Depending on the provider used for OAuth2, these may be named differently.

These are required to enable fully-features OAuth2 integration with your app.

## Keys

Custom Developer Keys:

- Unable to use custom logo in OAuth screen.
- Cannot use SSO properly because callback is not to the tenant callback url of the provider.
- User redirect from Rules will not work (/continue will fail).
- Federated logout will fail.
- Disabling (prompt=none) will not work.
- SAML Responses will miss critical properties.
- MFA will not work properly.

Provider Options:

- Google
- GitHub
- Facebook
- LinkedIn
- Twitter

Your Own Developer Keys:

- Check with each OAuth2 provider to acquire the keys.

## Auth0 Social Authenticators

This is related to Custom Developer Keys.

In the free tier, Auth0 allows up to 2 "social" authenticators.

- Google is there by default
- A second can be added

Auth0 Paid Tiers allow more.

## Auth0 Username Password Authenticator

In the free tier, Auth0 will support capture and use of end-users custom usernames and passwords.

-[ ] I need to look into how this works and how it can be leveraged for LingoBingo.

## Login and Logout

Three layers of authentication:

- Application Session: Requires the Application track users via Cookies in order to *log the user out of your application*.
- Auth0 Session: Auth0 has their own Session Layer SSO Cookie that they use to SSO re-authentication.
- Identity Providers Session (Google, Facebook, etc): It is not necessary to log a user out of their Identity Provider!

-[ ] Implement cookies on the Express server to enable logout.

Note: A Tenant-level 'Login URI' is available that can be used to all Applications within that Tenant.

### Setting and Forgetting Cookies

Set a cookie named 'auth0user_${useremail}': `req.cookie('auth0user_${useremail}', ${value}, { maxAge: ${30minutes} }`

Forget a cookie named 'auth0user_${useremail}': `res.clearCookie('auth0user_${useremail}')`

Cookie Options:

- domain: String => DN for the cookie.
- encode: Function() => Synchronous func for cookie value (default: encodeURIComponent).
- expires: Date => Expiry date in GMT. Session Cookies set to 0 (or not specified).
- httpOnly: Boolean => Accessibly only by the web SERVER.
- maxAge: Number => Expiry time, relative to current time in msec.
- path: String => Cookie path (default: '/');
- priority: String => Sets priority of Set-Cookie attribute.
- secure: Boolean => Only available with HTTPS protocol.
- signed: Boolean => Should the cookie by signed?
- sameSite: Boolean|String => Set value of 'SameSite' Set-Cookie attribute.

*Note*: res.clearCookie must match *all parameters and options* in order to clear the identified cookie.

See [ExpressJS 4x API](http://expressjs.com/en/4x/api.html#res.cookie) for details.

### Cookie-Session Middleware

Stores user session cookie data on the client.

- No DB or server-side resources required.
- Total session data limited to browser's max cookie size limits.
- Useful in load-balanced scenarios.
- Store light-weight session data including an identifier to lookup DB-backed data (reducing lookups).

### Redirect After Logout

Redirection post-logout can be done by registering the 'redirect url' in the Application Settings in Auth0.

Note: There is a Tenant-level 'redirect url' ("Allowed Logout URLs") which applies to all Applications within that Tenant that don't have 'redirect url' configured.

### Username Password Authentication

Auth0 provides a username-password-authentication database for free. It is possible to redirect Auth0 to your own DB.

- Require a username.
- Require a password of a certain range of length (e.g. 12-15).
- Import users to Auth0 for use with thie username-password DB.
- Enable/Disable 'sign-ups' to the application.

## User Management in Auth0

Creating a Role (RoleID) enables establishment of Permissions to Users that will access an Auth0 API.

- The Auth0 Management API is not included.
- TBD

## Enabling API Authentication

1. Create an Auth0 API.
1. Decide whether to set any Permissions.
1. Follow the steps at Auth0 Dashboard, Quickstart tab, for your API.
1. Once configured, go to the Test tab and follow the steps to request an Authorization Token, and then GET authenticated.

*Note*: You *MUST* include the following '/' in the 'issuer' entry. Not doing so will not authorize the jwt token and an error 'jwt issuer invalid' will be returned.

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root Readme](../README.html)
