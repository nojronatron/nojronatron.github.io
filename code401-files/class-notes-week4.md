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

## TODOs

-[ ] Keep hacking away at missing assignments *this week*
-[ ] Create a GH Gist with stuff like Application.properties template
-[ ] RETRO every day, and once per week: What can I regurgitate without looking up? What concepts do I have trouble with? Were there any blockers that I need help with?

## Footer

Return to root [README.html]
