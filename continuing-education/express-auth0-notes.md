# Working with Auth0 With Express

A collection of notes for future review about implementing Auth0 server-side for an Expressjs app.

## Required Reading

- Auth0 Docs [Authentication API](https://auth0.com/docs/api/authentication#introduction).
- Auth0 Docs [Client Credentials Flow](https://auth0.com/docs/get-started/authentication-and-authorization-flow/client-credentials-flow).
- Auth0 Docs [Call Your API Using Client Credentials Flow](https://auth0.com/docs/get-started/authentication-and-authorization-flow/call-your-api-using-the-client-credentials-flow).
- Auth0 Docs [Token Best Practices](https://auth0.com/docs/secure/tokens/token-best-practices).

## Quick Summaries

Auth0 Service and Configuration:

- An Auth0 Tenant will have the same Auth0 Domain e.g. dev-domain.us.auth0.com.
- An Auth0 Application will rely on the Auth0 Domain for endpoints like '/Authorize', '/.well-known/jwks.json' etc.
- The Auth0 Management API exists to supply Auth Tokens for Auth0 management endpoint access - basically do many admin and management tasks at the Tenant Level programmatically.
- Custom Auth0 API's is for: Acquiring Tokens for Auth Tokens scoped to specific 'audience' (protected service), and for applying permissions during authorization at the 'audience' end-point.
- Single-Page App configuration: Domain will be Tenant domain. ClientID and ClientSecret will be individual to each Application. App, Login, Logout, Origins/CORS, and Web Origins are Application-level settings.
- Token expiration and refresh lifetime are configured at each Application configuration level.
- Metadata: Can be assigned at the Application level (for identifying Tokens within the App).
- OAuth Endpoints: All of these hang off of the Auth0 Tenant Domain and support: User and Device Auth, OpenID Config, and a public JSON Web Key Set endpoint.
- SAML and WS-Federation: These hand off of the Auth0 Tenant Domain as well. I have not used these yet.

Auth0 Authentication and Token Validation using JWKS:

1. An application must be configured to find the Auth0 Domain and must have the Auth0 ClientID for the Application configuration in Auth0. An audience and Scope are not required but can be used for fine-grain control during authorization.
2. The front-end will also need to know (progorammatically or by user input) the URL to the API Server they want authorization to access.
3. When a user needs to login to the application, a redirect to Auth0's Universal Login provided by the configured in Auth0 Application will display, showing configured authentication types.
4. When a user authenticates, the Tenant (?) supplies an Auth Token to return to the web app, which can be stored securely.
5. When a user tries to access a protected API that requires a valid Auth Token, the web app must send the token (hopefully via https) to the custom API server (or if using device-2-device authentication, it is sent to the Auth0 API Management Service with a request to access an audience, but this is beyond the scope of these steps).
6. The custom API server must know the Auth0 Domain and Auth0 Issuer BaseURL, and the Auth0 JWKS URI. For Device-2-device authentication, an Audience must also be configured (out of scope).
7. The custom API server processes the client token using `jwks-rsa` and `jsonwebtoken`, validating it using the JWKS URI.
8. This is the point where the token is authenticated or not. If it is authenticated, then Cookies can be used to "keep the user authenticated through several API calls", rather than forcing the API server to digest the Auth Token for every single call. Either way would work though.
9. Timeouts: There should be timeouts on Application Session logins though, so the custom API server must be configured accordingly. Refresh Tokens eventually expire and Token Lifetimes too, so that scenario should trigger a re-authentication cycle on the client-side (not the custom API server side).
10. Logouts: Application session logout is just a matter or expiring the Cookies. Auth0 Logout requires the web app to call the `logout()` method in the Auth0 SDK. Any configured 'logout redirect' will be sent back from Auth0 so the web app redirects to the correct page.

## Terminology

### Machine-to-Machine (M2M) Application

Applications that need to authenticate without user credentials. Examples:

- CLIs, Daemons, or Services on back-end.
- Non-user scoped authentication scenarios.
- Authentication scenarios that are not 'Social Login'.

Instead of a username + password, a ClientID and Client Secret ae used for authentication, and in return are supplied with an Auth Token.

The flow is:

1. M2M App sends ClientID and ClientSecret to Auth0 Tenant.
1. Auth0 Tenant validates ClientID and ClientSecret and sends back an Auth Token (or an error).
1. M2M App sends a request with Auth Token in headers to the API Server endpoint.
1. API Server endpoint sends a response with data (or access denied).

### Java Web Tokens, Signatures, and Keys

JWT: Java Web Token. Check out [JWT.io](https://jwt.io/introduction) and [Auth0 Docs on JWT](https://auth0.com/docs/secure/tokens/json-web-tokens).

- JWT are similar to SAML Tokens but SAML are much larger (XML based). JWT are JSON objects and are easily used in HTTP and at scale.
- Use for Authentication, Authorization, and secure (signed) information exchange.
- JWT are *plain text* and therefore can be sniffed over an unencrypted connection. Always use HTTPS when exchanging JWT.
- JWT can contain claims, which can be used for fine-grained Authorization logic by the Application.

Security Algorithms:

- RS256: Provides asymmetric keys (X.509 Certificates) for Token signing and signature validation. Secure.
- HS256: Symmetric secret key to produce and validate signatures. Risky due to single, shared key structure.

Auth0 SDKs:

- Can perform JWT Validation for you, securely.
- Can perform JWT Parsing for you, properly.

In-code:

If a JWT Parser or Validator returns an error message 'jwt malformed' your code *must reject the request* to remain secure.

JWT Aud and Scope Fields:

- After validation and parsing, the JWT will have Aud and Scope fields, known as *Claims*.
- These are determined and set at Token creation time. Configure your Auth0 App settings to configure these fields.
- Aud: Audience. This has the URI of the intended resource that the Token was designed for.
- Scope: A space-separated list of permissions that can be applied to API endpoints or routes.

Scope Examples:

- `create:users`: Provides access to a specified endpoint like `/create`.
- `read:data`: Provides GET access to an endpoing like `/data`.
- OpenID (OID) example: `scope=openid name email family_name`.

Auth0 uses `scope=openid ...` to limit token size.

An API should enumerate Scope to ensure the API Endpoint rejects access when a Token does not include the correct Permission.

JWT Makeup:

- Segements separated by dots.
- 1st Segment is Token Metadata including crypto used to secure the Token.
- 2nd Segment is "payload". Contains claims and the ID of the user and their permissions.
- 3rd Segment is "signature". Use this to validate Token trustworthiness and integrity. Validation is a *required step* prior to storing and using the Token.

### Refresh Tookens

Auth0 only allows obtaining a Refresh Token if one of the following flows is used:

- Authorization Code Flow (with or without PKCE).
- Resource Owner Password Flow.
- Device Authorization Flow.

There are rate-limits set on Refresh Token requests (200 per Application). Manage this in the Auth0 dashboard.

When testing, follow Auth0's instructions in [Token Best Practices](https://auth0.com/docs/secure/tokens/token-best-practices) to avoid rate limit issues.

## React Auth0 Requirements

1. Pick your technology. Client, Server, CLI, or other. Expressjs is listed among the options. Note: So is Java Spring Framework.
1. Allowed Callback URLs. Example: 'http://localhost:3000/callback'. Auth0 redirects the user after they have authenticated.
1. Allowed Logout URLs. Example: 'http://localhost:3000'. Auth0 redirects the user after they logout of Auth0.
1. Install 'express-openid-connect' module (maintained by Auth0).
1. Generate a 32-bit random hexadecimal secret using either `openssl rand -hex 32` or [GRC Password Generator](https://www.grc.com/passwords.htm).
1. Configuration of the OpenID Auth Router.

### Routing Considerations

- Should any static routes be protected by authentication?
- Will a '/profile' route bring-up a custom profile page for the logged-in user?

In these cases, use a wrapper around those protected routes that calls Auth0, enabling use of 'isAuthenticated' (and possibly other members).

### Testing Considerations

- Thunderclient shows return data from Auth0 that can be used to start building a page or verifying output of routes.
- Using ThunderClient will show responses but does not have an interactive/rendering display so use the browser for interactive log-in activity.

### Application Settings

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

### Client ID and Client Secret

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

- [X] Implement cookies on an Express server to enable Application Logout.

Note: An Auth0 Tenant-level 'Login URI' is available that can be used to effect all Applications within that Tenant.

## Cookies for Application Login and Logout

### Setting and Forgetting Cookies in Express

Request Cookies: There could be multiple cookies within a Request object.

Response Cookie: When setting properties of the Response object, each Cookie is set individually.

Setting a Cookie in Response:

- Set a cookie named 'auth0user_${useremail}': `res.cookie('auth0user_${useremail}', ${value}, { maxAge: ${30minutes} }`
- Forget a cookie named 'auth0user_${useremail}': `res.clearCookie('auth0user_${useremail}' , ${value}, { maxAge: ${30minutes} )`

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

## Redirect After Logout

Redirection post-logout can be done by registering the 'redirect url' in the Application Settings in Auth0.

Note: There is a Tenant-level 'redirect url' ("Allowed Logout URLs") which applies to all Applications within that Tenant that don't have 'redirect url' configured.

## Username Password Authentication

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
1. Follow the Auth0 documentation for your back-end to ensure it is registered as an M2M App with Auth0, and that it has the Auth0 API settings for validating the user Authorization Token.
1. Be sure that the front-end acquires *the correct Auth Token from Auth0 API* before trying to get authorization from your custom backend server.

*Note*: You *MUST* include the following '/' in the 'issuer' entry. Not doing so will not authorize the jwt token and an error 'jwt issuer invalid' will be returned.

## Enabling Authentication to your Custom Backend the CodeFellows Way

This method relies on using the Asymmetric Keys available in the Single Page Application advanced settings, JSON Web Tokens, and auth0-react.

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

## Auth0 Tenants

Separate configuration boundaries within an Auth0 account.

Support dev, test, and production phases. Often company-dev and company-qa and another company-prod.

Separate user communities.

Sandboxes: Use to test different deployment scripts or implementation without impacting an existing deployment/production tenant.

If deleted, a Tenant Name *can never by used again*.

Enter a name, logo, and support email so customers can confirm they are in the right place, and get support if necessary.

Vanity Domain URL:

- More difficult to fish your domain.
- Some browsers limit iFrame cross-domain support - using a vanity Domain will cure this.

Enable MFA for your Admins.

Tenants support multiple Admins (recommended).

SSO Cookie Timeout (login session lifetime) is per-Tenant. Default is 7 days.

Sandboxing: Ensure tenants are associated with your account so that the sandboxes are within your account scope.

## References

- Auth0 React Tutorial: [Login](https://auth0.com/docs/quickstart/spa/react/01-login).
- Auth0 React Tutorial: [Call an API](https://auth0.com/docs/quickstart/spa/react/02-calling-an-api).
- Auth0 [Add Login to a React App](https://auth0.com/docs/quickstart/spa/react#add-login-to-your-application)
- Auth0 Github code [Example of route protections using Auth0](https://github.com/auth0/auth0-react/blob/master/EXAMPLES.md#protect-a-route)
- [Code Fellows](https://www.codefellows.org/courses/code-301/intermediate-software-development/) course materials.

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root Readme](../README.html)
