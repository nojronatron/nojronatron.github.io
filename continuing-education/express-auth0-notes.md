# Working with Auth0 With Express

A collection of notes for future review about implementing Auth0 server-side for an Expressjs app.

## Requirements

TBD

## Application Settings

The most critical configuration items to set up:

- Name
- Domain nnnnnnn.us.auth0.com
- Client ID?
- Client Secret?
- Application Type: Determines what settings can be configured from dashboard. Code301 used "SPA".
- Token Endpoint Auth Method: None.
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

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root Readme](../README.html)
