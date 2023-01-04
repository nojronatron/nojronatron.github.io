# Working with Auth0 With Express

A collection of notes for future review about implementing Auth0 server-side for an Expressjs app.

## Required Reading

[Auth0 Docs - Authentication API](https://auth0.com/docs/api/authentication#introduction)
[Add Login to a React App](https://auth0.com/docs/quickstart/spa/react#add-login-to-your-application)
[Call an API from React/JS](https://auth0.com/docs/quickstart/spa/react/02-calling-an-api)
[Example of route protections using Auth0](https://github.com/auth0/auth0-react/blob/master/EXAMPLES.md#protect-a-route)

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

- [X] I need to look into how this works and how it can be leveraged for LingoBingo.

## Login and Logout

Three layers of authentication:

- Application Session: Requires the Application track users via Cookies in order to *log the user out of your application*.
- Auth0 Session: Auth0 has their own Session Layer SSO Cookie that they use to SSO re-authentication.
- Identity Providers Session (Google, Facebook, etc): It is not necessary to log a user out of their Identity Provider!

- [X] Implement cookies on the Express server to enable logout.

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
- Going this route will require acquiring an Auth Token from the Auth0 API Server and then a separate Token for the Express server to validate before authorizing access to a route.

Code Fellows suggested using:

- jsonwebtoken
- jwks-rsa
- Auth0 front-end App advanced setting `JSON Web Key Set` URI (avoids having to request authorization from the Auth0 API Server *but* limits authorization to allow/deny without fine-grained permissions control).

## Enabling API Authentication the Auth0 Way

1. Create an Auth0 API.
1. Decide whether to set any Permissions.
1. Follow the steps at Auth0 Dashboard, Quickstart tab, for your API.
1. Once configured, go to the Test tab and follow the steps to request an Authorization Token, and then GET authenticated.
1. Configure your Front-end with the API Server settings and an Audience setting (the URL to your back-end server).
1. Follow the Auth0 documentation to programmatically check for authorization on the Front end.
1. Follow the Auth0 documentation for your back-end to ensure it is registered as a nodejs/Express app, and that it has the Auth0 API settings for validating the user Authorization Token.
1. Be sure that the front-end acquires *the correct Auth Token from Auth0 API* before trying to get authorization from your custom backend server.

*Note*: You *MUST* include the following '/' in the 'issuer' entry. Not doing so will not authorize the jwt token and an error 'jwt issuer invalid' will be returned.

## Enabling Authentication to your Custom Backend the CodeFellows Way

Express Back End:

1. Install `cors`, `dotenv`, `jsonwebtoken`, and `jwks-rsa`. Redirects *will not work* without CORS installed.
1. Implement an Authorization module that uses `jsonwebtoken` and `jwks-rsa`. Implement a client by configuring jwksClient with the JSON Web Key Set URI of the front-end server. Implement getKey function that calls `client.getSigningKey()` and has a callback (supplying the signingKey) for `jwt.verify()` to use. Implement `verifyUser()` function that extracts a valid token from `req.headers.authorization` and supplies that token to `jwt.verify()` alogn with getKey, and empty object `{}`, and `errorFirstOrUserCallbackFunction`. Catch any errors. Export `verifyUser` from the module.
1. Require `verifyUser` (the custom module from previous step) and insert it (as a middleware) to each route that requires authorization to access.

React Front End:

1. Install `@auth0/auth0-react` and perhaps `axios` (else use `fetch`).
1. Import `{Auth0Provider}` from auth0-react and *wrap all child Components within the `render()`*. Remember to configure Auth0Provider with Auth_Domain, Auth_ClientID, and Auth_Redirect.
1. Optional: Create Login and Logout buttons (see info below).
1. Child components that need authorization: Import `{ withAuth0 }`. With this module comes `auth0.isAuthenticated` for free. Use isAuthenticated to show/hide components. The Module that uses 'withAuth0' *must* export like: `export default withAuth0(child);` where 'child' is the name of the component e.g. 'App'.
1. Child Components that require use of `useAuth0` functions or properties *must* import it. Functions include `user`, `isAuthenticated`, `isLoading`...

### Get a Token and Configure Axios to Call With Authorization

Within the front-end app, create a component that checks for authentication and if true, configures Axios with a valid Authorization Header with an Auth0 token.

1. Import `withAuth0` and `axios` (and perhaps React).
1. Check for authentication with `auth0.isAuthenticated`.
1. If authenticated, get claims with `auth0.getIdTokenClaims()`.
1. Define variable `jwt = res.__raw` *two underscores*.
1. Create an Axios configuration object with `method`, `baseURL` (server base address, optionally acquired from env vars), `url` (target path), `headers: { 'Authorization': 'Bearer ${jwt}'}`. *Note: Last part is a back-ticked template literal*!
1. Execute the Axios call a-la `const results = await axios(config);` and the authorization header will be included. If path requires token validation (authorization) that will happen automatically on the back end and the appropriate HTTP Status Code (and optional message) should be returned/expected.

*Note*: Much of this code will need to within asynchronous method(s), and could be executed within `componentDidMount()` or a `useEffect()`.

### Login and Logout Buttons

Login:

1. Import `useAuth0`.
1. Return a function that takes 0 parameters.
1. Within the function, deconstruct `loginWithRedirect` from `useAuth0()`.
1. Function returns a button with an onClick method that calls Auth0 `loginWithRedirect()`.

Logout:

1. Import `userAuth0`;
1. Return a function that takes 0 parameters.
1. Within the function, deconstruct `logout` from `useAuth0()`.
1. Function returns a button with an onClick handler that calls `window.location.origin` (this helps manage redirects from Auth0).

### User Details Available Upon Authorization

`useAuth()` provides a `user` object that has properties that can be used for a profile page:

```javascript
import { userAuth0 } from '@auth0/auth0-react';

const UserProfile = () = > {
  const { user, isLoading } = useAuth0();

  if (isLoading) {
    return <div>Loading . . .</div>;
  }

  return (
    isAuthenticated && (
      <div>
        <img src={user.picture} alt={user.name} />
        <h2>{user.name}</h2>
        <h4>{user.email}<h4>
      </div>
    )
  );
};

export default UserProfile;
```

## References

- React Tutorial: [Login](https://auth0.com/docs/quickstart/spa/react/01-login).
- React Tutorial: [Call an API](https://auth0.com/docs/quickstart/spa/react/02-calling-an-api).
- [Code Fellows](https://www.codefellows.org/courses/code-301/intermediate-software-development/).

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root Readme](../README.html)
