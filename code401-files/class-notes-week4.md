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

1. Project structure: Select the correct JDK version in Initializr *that you have on your dev machine*!
1. Make sure your IDE is starting up at the actual PROJECT ROOT.
1. build.gradle: starter jpa, starter typeleaf, starte we, boot devtoops, starter test, postgresql
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
1. Implement a repository, extending JpaRepository, and pass-in the Model and type of the ID property.
1. build-out '@PostMapping(/route)' entries to enable posting to the dynamic website. Use method return type 'RedirectView' so that on a 'login' route, and credential test returns true, the next-loaded page (redirect page) will be the splace page (e.g. User is "in" the application). Dont forget CTORs and getters+setters.
1. Back in the Repository class definition, set up the CRUD command and supply the Class property you are searching for: TYPE findByUser(username)
1. Update the Controller to test the password vs what is in the database and return the redirect view (to the page the user can access only if logged on).
1. Use .equals() to compare object.password with _password parameter.
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

## TODOs

-[ ] Keep hacking away at missing assignments *this week*
-[ ] Create a GH Gist with stuff like Application.properties template
-[ ] RETRO every day, and once per week: What can I regurgitate without looking up? What concepts do I have trouble with? Were there any blockers that I need help with?
-[ ] CodeChallenge 14: Do for bonus points! Pair-up to make it easier!

## Footer

Return to root [README.html]
