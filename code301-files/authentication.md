# Authentication Authorization and Auth0

## What Is OAuth QandA

Give an example of what using OAuth would look like.

1. OAuth is used to enable computers to log on users on their behalf.  
2. User browses to a website and is presented with a logon screen that includes an open-authentication provider like Google.com.  
3. The user clicks that login provider to log-in, and that provider tells the website that the user is authenticated.
4. The website allows the user access, trusting the Google OAuth Provider's authorization.

How does OAuth work?  

As discussed on *[csoonline.com, accessed 30-Apr-2022]*

1. One website contacts a second website, on behalf of a website user, and uses OAuth framework, providing the user's identity.  
2. The second website generates a one-time token and one-time secret unique to the transaction and parties involved.  
3. The first site gives this token and secret to the initiating user's client software.  
4. The client's software presents the *request token* and secret to their authorization provider that could be on the second site (or not).  
5. If not already authenticated to the authorization provider, the client may be asked to authenticate. Afterwards, the client is asked to approve the authorization transaction to the second website.
6. The user (or the software they are use) approve a particular transaction type at the first website.  
What are the steps that it takes to authenticate the user?  
7. User is given an approved *access token*.  
8. The user gives the approved *access token* to the first website.  
9. The first website gives the access token to the second website as proof of authentication on behalf of the user.  
10. The second website lets the first website access their site on behalf of the user.  
11. The user sees a successfully completed transaction occurring.  

What is OpenID?  

> It is an open *Authentication* system (as opposed to OAuth *authorization* system).  
> OpenID is used to authenticate users to machines.  

## Authorization and Authentication Flows QandA

All responses were derived from reading the [Auth0 documentation on authentication and authorization flows](https://auth0.com/docs/get-started/authentication-and-authorization-flow)  

What is the difference between authorization and authentication?  

> Authentication (Auth-n) is the process of positively identifying a person or a thing.  
> Authorization (Auth-z) is a permission granted to an entity to allow an action or state of being.  

What is Authorization Code Flow?  

> For Auth0, it means authentication and authorization are handled in a single stream of activy that supports server-side, mobile, desktop, client-side, machine-to-machine, and devices.  

What is Authorization Code Flow with Proof Key for Code Exchange (PKCE)?  

> An added security layer for use on single-page apps and other instances where a client secret cannot be securely stored.  
> There is an excellent diagram on Auth-n Code Flow with PKCE at the [Auth0 website](https://auth0.com/docs/get-started/authentication-and-authorization-flow/authorization-code-flow-with-proof-key-for-code-exchange-pkce)  

What is Implicit Flow with Form Post?  

> Intended for *public clients* or applications that are insecure and cannot safely store client secrets.
> This flow offers a streamlined workflow if the application only needs an ID token to perform user authentication. 

What is Client Credentials Flow?  

> Used in machine-to-machine (M2M) applications (e.g.: daemons, services on the back end) authorizes an applicaton instead of a user.  

What is Device Authorization Flow?  

> Used for smartphones and other limited-input devices.  
> The device will ask the user to click a link or button on their smartphone to authorize the devices.  
> Used where entering text would be difficult or impossible.  
> An OAuth 2.0 draft implementation.  

What is Resource Owner Password Flow?  

> An alternative to Authorization Code Flow.  
> Uses an interactive form to capture username and password.  
> Should only be used when redirect-based flows cannot be used.  

## Resources and References

[What is OAuth](https://www.csoonline.com/article/3216404/what-is-oauth-how-the-open-authorization-framework-works.html)  
Authorization and Authentication [flows](https://auth0.com/docs/flows)  
[Auth0 for Single Page Apps](https://auth0.com/docs/libraries/auth0-react)  

## Footer

Go back to [Readme.md](../README.html)
