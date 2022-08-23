# Morning Discussion Notes

Assessment grading will be done on Saturday.  

## Project Week Preview

Plans need sign-off before beginning execution.  

## Code Review

Use an anonymous method when the method has a parameters list *and* the method should NOT fire immediately at runtime.  

```js
// inside of a React render method

// fires on render
<BookFormModal
  onClick={fireFormOnClick(item.property)}
  >
  // more code ...
</BookFormModal>

// will NOT fire on render
<OtherModal
  onClick={()=>fireFormOnClick(otherItem.property)}
  >
  // more code...
</OtherModal>
```

Required when performing a REST PUT Update operation:

1. url to the route
2. the fully-hydrated item that includes existing data AND the updated data

Use path parameters for data you KNOW exists i.e. the client *got* the data *from* the database or API server.  

Use Query Strings when you *do not* know whether the data is in the API/Database.  

## What Is Auth

Authentication :: Identification  
Authorization :: Allowance  

Within CRUD the breakdown of Auth operations is fairly fine-grained.  

### OAuth

One protocol that handles Authorization.  
Decouples Auth-n and Auth-z to allow authorization to a resource.  
Can leverage other authenticators and profile-holders to manage the auth-N portion.  

### Auth0

Requirement for final project: Implement Auth0  
Ideally, at least one person will figure out how to use it for the final.  
For Can-of-Books project: *just get it to log a Token on the FE* and console log it.  
Auth0 is a company that has implemented an OAuth solution.  

### Auth0 Auth Path

1. login request from client
2. OK received from Auth0
3. user token created and sent to my API server
4. API-server verifies token with Auth0 to validate it
5. Auth0 replies to server OK/NO
6. API server sends appropriate response to the client

### Auth0 Setup Info

Quick Reminder: Set localhost:port for most URLs during testing.

1. Select type of project. For us it will be React
1. Set an Auth0 badge (or use default)
1. Update Application Login URI
1. Set allowed Web origin URLs
1. Set allowed login URLs
1. Set allowed callback URLs (use 'localhost:port' but change to Netlify for deployment, comma-separated)
1. CORS: Leave blank to essentially 'allow all'. Updateing this field add *limitations*
1. JSON Web Key Set: Necessary to implement Auth0 on the back-end, to validate JWT tokens
1. Install the React Auth0 SDK
1. Wrap the `<Auth0Provider>` around your entire React App (index.js? or app.js? or ?)
1. Add attributes to Auth0Provider to define: domain, clientId, redirectUri => REACT_APP_AUTH_DOMAIN, REACT_APP_AUTH_CLIENT_ID, and REACT_APP_AUTH_REDIRECT)
1. Update '.env' *in the root of your project* file with details set above ()
1. Wrap App in export default statement with Auth0: `export default withAuth0(App)`
1. Add import from statement on pages where Auth0 is needed: `import {withAuth0} from '@auth0/auth0-react'`
1. Convert Auth0 into a Bootstrap method/component ???
1. Auth0 brings-in functionality like `this.props.auth0.isAuthenticated ? ifTrueCode : ifFalseCode;`
1. If user is logged-in then show a page, otherwise show a different screen e.g. please login
1. missing steps here!!
1. const res = await this.props.auth0.getIdTokenClaims();
1. const jwt = res.__raw to console.log the token
1. Axios allows sending a config object to make axios requests `const config = {...}`
1. To implement/use the JWT token, append the work 'Bearer ' to the front of the token.
1. Install jwks-rsa and jsonwebtoken modules and 'auth.js' will import them to handle both auth-n and auth-z, using jwksClient (see code in class repo)
1. Add jwks URL to the '.env' file
1. Use `jsonwebtoken.getKey()` and process it
1. Add functionality to verify the user on our route is authorized using a custom function and pass-in parameters 'request' and 'errorFirstOrUserCallbackFunction' => this is a try-catch for auth to return ErrorFirst if auth-n fails otherwise return the callback function to represent 'access allowed'

```js
// rough example but use of turnary is key
this.props.auth0.isAuthenticated ? (<>Your JSX page and components here</>)} : (<>JSX or component to show user when NOT logged on</>);
```

Recommendations:

- Copy the code from auth0.com to index.js, login.js, logout.js, and profile.js
- In fact, copy *as much code as you can* from the Auth0 website to save time and energy (no need to attribute it)
- Filenames suggested can be used as-are and in the end everything must be linked-up in the usual React way)
- HTTPS: *should* use it but not essential
- Allowed Callback URLs are necessary!
- All of the front-end ENV file entries relating to Auth0 *must be added to Netlify*
- *DO NOT* leave console.log of 'jawt' JWT Tokens in code usually, but do it for Lab15
- Sending a config{} object makes the Axios request simpler by wrapping everything needed: baseUrl, headers, method, and url  
- When dealing with auth.js be sure to have the headers sorted out properly otherwise it will break!  

### Auth0 Files

Profiles.js => Retains usernames (maybe more?)  

## Can Of Book Project Work

1. Implement Auth0 *client-side* request/response and assume an approved token is proxy for authentication and authorization?
1. Console log the JWT Token for credit

## Day Plan

1230 local: Partner Power Hour  
1330 local: Meet back at Zoom and discuss projects  
1400 local: Get minimal functionality going on Lab15 and submit it  
1600 local: Campus Virtual Mixer  

## Project Week Planning

- Review Project Guidelines in teh assignment  
- Review the Project Prep Assignments (1, 2, 3, and 4)  
- Timebox the cooperative agreement focusing on strength and weaknesses and remember Code Fellows Code of Conduct, applying those guidelines to the agreement  
- Complete Project Prep assignment 1, 2 within an hour each (timebox each to an hour) and turn them in together  
- Pick 2 ideas: A primary and a backup to pitch  
- Requirements: MERN + CRUD fully implemented  
- Project Prep #3: Set this up on Monday (GH, Trello, Heroku, other tools selections)  
- Project Prep #4: Wireframes of UI, JS logic flow, WRRC diagram, and optional control flow/user flow  
- Make sure 'how to build' steps are included in readme.md at a level that any Code 301 student could follow and successfully deploy  
- Project Reports: Retros, in QandA form, for the project, and they are fully confidential only to instructional staff  

## Jon TODOs

[ ] Read about passing "options" via `Mongoose.findByIdAndUpdate(id, body, options)`: This is what differentiates between a PUT and a PATCH.  
