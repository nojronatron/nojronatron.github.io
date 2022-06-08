# Class Notes Week 4 Jun 6 Through 10

## Monday Morning Discussion

STOP BEING A COMPLETIONIST

Spring MVC requires submit FORM DATA by default unless you specificy `application-type/json`.

### Code Challenge 13 Review

Big-O notation generally deals with TIME, and less so about space because memory is relatively cheap.

Recursive call? O(n)

Adding an Array (O(n) in Space)? Adding 2 arrays? Could be 2n, 3n etc, but it still boils down to 'n' because the increase is not significant.

Base Case: Required in recursive methods. Tells the recursive function *where to stop*.

Remember always check for null before calling a method and using Node.child as an argument.

### Lab 13 Review

This was our first full-stack application.

Spring Retro:

- spring mvc: Model-View-Controller => Design pattern; Frameworks
- repositories: An interface that extends JPA, providing connection to DB
- postgres: Hibernate is our ORM, postgres is the OpenSQL DB service
- thymeleaf: Front-end Template Engine => Manages connection to it, for displaying data. Mustache and React are similar in their ultimate jobs
- CRUD: Create, Read, Upate, Delete => For DB operations
- JPA: Java Persistence API gives us the CRUD operations via its overridden methods
- JDBC: Maintains connection to DB service
- Application.properties: Describes the JPA/postgres/JDBC environment
- Dependency Injection/AutoWired: An OOP design pattern => Fire-up a service (like connection to JDBC/DB) and it will be available for the life of the application (and auto-closes the service), guaranteeing it will only be a single instance
- GetMapping => HTTM Methods; Resource hosting; user interaction
- REST: No state/data stored between requests; ensures privacy, anonymity, and security

Trees Retro:

- Trees: Binary Trees => Each node can have only 2 children; 1-level relationship between parent and child nodes
- BST: Sorted Tree => Could be a Binary Tree, or some other Tree model
- DFS: Pre/In/Post Order searching; Always search left-to-right; Pre/In/Post refers to where the Data/Value is returned; Tip: Root node value appears in the resulting list: pre=first; in=middle; post=last
- BFS: Search by level, left-to-right; Levels start at zero; Use a Queue in a While loop

### Authentication

Authentication:

- Positively identify people, places, and things (users, services, service objects).
- You *are* who you *say you are*.

Authorization:

- Allow/disallowed to information, resources, or places.

Roles:

- Postgres uses this term
- Breaks down to what a user is able to do e.g. : CRUD operations!

Unauthentication/Anonymous Users

- Not all bad
- Leverage identifying these users by showing a login page
- Only show a homepage or simple data while they are anonymous

What are ways we can authenticate users/systems?

- Email
- Passwords
- 2FA and MFA
- Biometric: Face, fingerprint, retinal scan

Commonly used 2FA and MFA methodologies:

1. Something you have: A random number generator or Key
2. Something you know: PIN, Password
3. Something you are: Biometrics
4. Something you do: Dynamic biometrics e.g. Voice

### Hasing and Encryption

See Jun6 reading notes.

Hashing is NOT encryption in and of itself.

Salting: Merging a pre-configured variable/string with a plaintext. Salt must be kept secret. Does *not* make up for using a break-able cipher.

BCrypt is a hashing tool.

Hashing vs Encryption

- Hashing performs an irreversible function against the plaintext input.
- Hashing is one-way.
- Encryption/Decryption is a two-way function.

Hashing

- When you crate a passwd it is hashed to a unique value.
- Passwd has is stored on the server.
- Next time a user enters their password it is hashed, and the hash is checked against the has stored on the server to authenticate the user (or not if different).
- This limits password exposure across the network.

DO NOT add Spring Security to our existing Labs => Start a new lab instead.

### Lab Preview

Class 14 Lab due today.

Use the code (below) as a baseline to developing this lab.

Don't direct people to a route UNTIL THEY ARE LOGGED ON.

Do NOT use Spring Security today.

Use Thymeleaf w/ 'Model' and avoid using "User" as the name of your user object.

#### MVC

##### Views

- Login: Might require redirects with bad login event to put them back to Login route.
- Signup: Redirect users back to the Login page upon signing up.

##### Controllers and Routes

- Login Controller:  GET route to display the login page.
- Login Controller: POST route for accepting the user-submitted login credentials.
- Signup Controller: GET route to display the signup page.
- Signup Controller: POST route to accepts user-submitted signup information.
- Home Controller: GET route for simple splash/home page.

##### Models

UserModel:

- Unique ID
- Username
- Password

Repo with JPA:

AuthRepo: The interface that hosts the DB access methods:

- findByUsername()

*Note*: Do *not* use the class name or variable name "User". Instead, use a more-descriptive name i.e. "SiteUser" or "ChatUser" etc.

##### Database

postgres SQL type DB.

##### Live Coding Notes

Having git issues? How is your repository set up? Are you sharing projects within the same git repo?

Steps taken during live coding:

1. Set Project structure and configs using Initializer: Select the correct JDK version *that you have on your dev machine*
1. build.gradle: starter jpa, starter tymeleaf, spring web, spring boot devtools, starter test, postgresql
1. Make sure your IDE is starting up at the actual PROJECT ROOT.
1. Update Application.properties to include datasource.url, datasource.username, datasource.password, jpa.generate-dll, jpa.hibernate.dll, hiddenmetho.filter.enabled
1. PGAdmin4: Create the necessary Database (if using an existing one DROP EXISTING TABLES).
1. When building, make sure a 'build successful' actually results.
1. build a proof-of-life html template page: index.html (new file => html, or new file => ! [Tab])
1. add a signup.html file and write a Form action with the signup path
1. add a login.html file and write a Form action with login path
1. Build and check for errors: Missing datasource, etc
1. test the home route and verify your index.html page appears!
1. build an Auth Controller using '@Controller': '@GetMapping(/route)' with method returning the dynamic/template html page
1. Create a SiteUser class that includes '@Entity' and import javax.persistence.Entity. Add properties including a '@Id' (java persistence ID) and '@GeneratedValue' with a strategy to auto-generate and increment the ID.
1. Implement a repository, extending JpaRepository, and pass-in the Model and type of the ID property. Dont forget CTORs and getters+setters.
1. build-out '@PostMapping(/route)' entries to enable posting to the dynamic website. Use method return type 'RedirectView' so that on a 'login' route, and credential test returns true, the next-loaded page (redirect page) will be the splash page (e.g. User is "in" the application).
1. Back in the Repository class definition, set up the CRUD command and supply the Class property you are searching for: TYPE findByUser(username)
1. Update the Controller to test the password vs what is in the database and return the redirect view (to the page the user can access only if logged on).
1. Use .equals() to compare object.password with _password parameter.
1. Add BCrypt to the build.gradle file, dependencies section.
1. Implement hashed passwords using BCrypt: 'BCrypt.hashpw(password, BCrypt.gensalt(int: hash_rounds));' and then update the new site user password to be the hashed_password.
1. Back to login Controller route, update the if statement: 'if((userFromDB == null) || (!BCrypt.checkpw(_password, userFromDB.password)) return new RedirectView("/login");' otherwise user gets sent to home route "/". Use parenthesis to force the evaluations to be expressions so they operate in the correct order.
1. Verify your user and hashed-passwd logic for redirecting to Home or Login again.

Remember:

- Put html in STATIC folder only if you do not need a PATH for it but browser can go direct to the file.
- Dynamic web pages can only be accessed via paths (Controllers) will NOT render from the URL address bar.
- When defining Controller Route parameters, use underscore '_' prefixing.
- Spring MVC includes a class called Class that is the transport for '@Entity' annotated classes so that passing data between Controllers and the dynamic template pages.
- Use 'gradle refresh' after adding dependencies!

#### Code Challenge 16

Find maximum value within a binary tree.

Tip: Try to track the maximum value *within recursion*.

Can be partnered on one-your-own.

### Team Prep Work Today

Planning for all the usual Midterm/Final Presentation preparatory work.

## Tuesday 7Jun22

ALWAYS keep working within MVP and Features:

- MVP: The most basic functionality
- Features: Bolt-on capabilities to the MVP

Apply this thinking to Labs.

### Team Prep Comments

Try to get your MVP small enough that it is complete by EOD Tuesday.

If Tuesday MVP is reached *then* bolt-on smaller feature add-ons and continue with documentation and testing.

Not all conflict involves emotions, so check yourself and your situation, and communicate concerns and bring solutions to the table.

There are 4 total preps.

Project Prep 2 is PROJECT IDEAS.

### Code Review

Tree Max

Review the very basics of [Unit Tests](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Challenge_Testing)

### Using Cookies in Spring

*Note*: Case sensitivity is in play!!

Use Developer Tools > Application > Storage > Cookies: To see set cookie details e.g. JSessionID (aka SessionID) and Value etc.

Need to add a Model for the AuthenticationController to be able to properly authenticate a user.

1. HttpServletRequest request must be added to the controller path `@PostMapping("loginWithSecretPage")`
1. SetAttribute on this session: Binds an object to a session using the specified name. `session.setAttribute("username", username)`
1. `HttpSession session = request.getsession()` comes from httpservletrequest?
1. `session.invalidate()` breaks the session cookie info so they cannot be replaced (logs out the user).
1. Hide cookie usage via `server.servlet.sesion.tracking-modes="cookie"` ??? (look for Alex's future update on this).

### Spring Security Demo

Create an authenticated server.

New gradle project, NOT MAVEN.

Setup using Spring Security:

1. Initializr with postgres, spring boot, spring security, etc.
1. Verify application.properties is set up.
1. Do a build to verify all is good. User-generated security password is provided. Use this default built-in form, but YOU need to update it by implementing the 'what to do' after form login.

#### Beans

Spring transforms @Service, @Entity, and @Controller into "Beans".

These are DI'd components that make up the Spring "Application Context".

Singleton: Only instantiate an object ONE TIME throughout the life of the application.

Beans exist for the life of the application, each Bean its own unique service/state, until the App shuts down.

Repositories *are also Beans*, so just use the '@Autowired' annotation to access it from other Classes!

*Note*: Variables MUST be named consistently!

Spring Beans: @Autowired, @Component, @Service, @ => All beans go away when the App is closed!

Steps:

1. Set up a user model and repo: 'model.AppUser' with properties: username, password, and add @Entity and @Id @GeneratedValue, and be sure to use private fields and getters/setters EXCEPT for Id. Also add constructors.
1. Create Repo: 'repository.AppRepository' and set it as an interface that 'extends JPARepository<AppUser, Long> { // custom query like findByUsername(String username);}'
1. Create a controller for that model: New Class controller.AppController, add four routes: get to login, get to signup, post to login, and post to login. Remember to use '@Controller' and '@AutoWired' and '@GetMapping' and '@PostMapping' decorators.
1. In the Post to Signup path, ensure the method grabs the username and password, then '@AutoWire' it (makes it a bean so it is a service available and DRY is followed).
1. Save the new user (with hashed passwd) to the repository.
1. UserDetailsServiceImpl implements UserDetailsService => Createa  new Package called 'config.UserDetailsServiceImpl' of type Class. Then *implement the method(s)*.
1. Implement UserDetails on the ApplicationUser class (there are 5 of them) and Booleans all return true.
1. Summary: WebSecurityConfig extends WebSecurityConfigurerAdapter. Create a new configs.WebSecuityConfig Class that extends WebSecurityConfigurerAdapter. Also add @Configuration and @EnableWebSecurity. Continues on next step...
1. Implement the @AutoWired annotation and set variable type UserDetailsServiceImp userDetailsService. NExt step...
1. Create public PasswordEncoder passwordEncoder method, takes no params. Enable BCryptPasswordEncoder as a variable (it already implemnets PasswordEncoder) so it can be returned within the method and returns bCryptPasswordEncoder. Continue...
1. Make this method a Bean with '@Bean', then add '@Autowired PasswordEncoder passwordEncoder' which *injects the singleton Bean into the class so it is usable within those methods*, THEN just use 'passwordEncoder' to .encode(passwd) or .decode(passwd).
1. Override configure(AuthenticationManagerBuilder) with 'auth.userDetailsService(userDetailsService).passwordEncoder(passwordEncoder());'
1. Configure security via HttpSecurity: Override configure(HttpSecurity http) and implement CORS, CSRF, URL Maters, Form Login, and Logout. Continue
1. CORS to configure access from outside your network: http.cors().disable() // were not sharing outside of our network
1. CSRF Cross Site Reference Forging: 'http.csrf().disable().authroizeRequests().antMatchers("/").permitAll()' // will not allow requests to come in as you unless they come from specific routes defined in out site but this specific config just allows anonymous access to root
1. CSRF for other routes: ... .antMatchers("/permitPath1", "/permitPath2", ...).permitAll()
1. Tie-together chained configuration with '.and()'
1. Form Login location config: ... .loginPath("/loginPath")
1. Logout page too: ... .and().logout()
1. On successful logout send user to login: ... .logoutSuccessUrl("/login")
1. Registration Page: We have createUser route "/signup". Create a template HTML for this page, add a Form with proper names and IDs so the username and password (and anything else) are captured for setup new user route.
1. Login Page: Similar to Registration Page but for login of an existing, valid user. This will override the built-in login page that Spring Security deployed when we initialized the project.
1. Auth with HttpServletRequest (later): Add this method to the AppController. Autowire the HttpServletRequest and name it 'request' so that it is available to the entire Controller. authWith

*Note*: There is no POST TO LOGIN because it is all in WebSecurityConfig.java => '.loginPath("/login")'

## Wednesday 8Jun22 Notes

### Morning Discussion

Mid-term Team Project chat.

Teams tell Alex when they want to stand-up meet, and this can be scheduled day-of.

Spring Security authz to content (conditional rendering).

Security software: Don't dev it yourself, use what exists, has been well tested, and what big corporations are using.

Bruce Schneier chit-chat.

Bug Bounties: Finding bugs can turn into cash! [bugcrowd](https://www.bugcrowd.com)

### Code Review Breadth First

Tips:

- Use a queue to track "where we are in the tree" while dealing with other nodes.
- Ensuring a tracking queue is loaded prior to entering the while loop is critical, otherwise while loop exits right away.
- Front node must ALWAYS be dequeued prior to grabbing its value so that it doesn't stay in the queue and get counted again.
- The Breadth Algorithm is a sub-tree logic loop, because it only deals with one parent, and however many children it has.

O(n) Stuff:

- Whenever there are lists, arrays, collections, etc, that is an O(n) operation.
- When there are multiple lists, queues, stacks, etc, that is an O(n+n+...) which boils down to O(n).

### Authorization

The [Spring Security Cheat Sheet](https://github.com/nojronatron/seattle-code-java-401d12/blob/main/SpringSecurityCheatSheet.md) can be followed to help get Spring Security set up and implemented.

Separate Controllers to manage specific tasks i.e. User Creation actions, Authenticated actions, Unauthenticated actions, specific paths, etc.

Principal: The authenticated user or object. A User Principal in this case.

Threading: One user per thread => Only that thread's user will be handled in the auth/action workflow.

When creating a Controller Mapping, take in args Principal p and Model m and test p != null before taking action on the args.

On a path HTML where a Controller Mapping has a principal params:

- Add thymeleaf to allow passing values between Controller and Template page using "TH:" attributes.
- Use 'm.addAttribute("name", name)' so that ThymeLeaf TH can utilize it e.g. `th:text="${name}"`
- When authenticated, only certain Paths have access (web security config file defines this and routes user to the specific Controller handler).
- Logout button calls '/logout' path that web security config file filters as a 'close this session and go to this un-auth path' workflow.

All of the above is *baked in to Spring Security* and is fairly basic.

-[ ] Today's Lab (Class 17) will build on yesterday's (CodeFellowship).
-[ ] TODO: Get my app up and running, commit and update yesterday's Lab submission THEN move-on to the rest of the app.
-[ ] TODO: Reference baeldung dates-in-thymeleaf page for help with managing Date objects in your Thymeleaf website including formatting.


## TODOs

-[ ] Keep hacking away at missing assignments *this week*
-[ ] Create a GH Gist with stuff like Application.properties template
-[ ] RETRO every day, and once per week: What can I regurgitate without looking up? What concepts do I have trouble with? Were there any blockers that I need help with?
-[ ] CodeChallenge 14: Do for bonus points! Pair-up to make it easier!

## Footer

Return to root [README.html]
