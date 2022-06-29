# Serverless, Amplify and GraphQL

## Resources

What is Serverless Architecture? By [Hackernoon.com](https://hackernoon.com/what-is-serverless-architecture-what-are-its-pros-and-cons-cc4b804022e9)

Amazon AWS [Amplify](https://aws.amazon.com/amplify/)

Data Modeling at [Amplify Docs](https://docs.amplify.aws/cli/graphql/data-modeling/)

## Serverless Architecture

A buzzword!

It is:

- An execution model: Cloud CSPs manage server allocation and provisioning.
- Stateless.
- Event-triggered.
- Priced based on execution count (rather than compute capacity, etc).
- Oriented to service client-side logic.
- A provider of Functions-as-a-Service.
- Back-end logic + Security + Database functionality. Client-side logic is... in the client.

Sample of CSPs and their Serverless offerings:

- IBM OpenWhisk
- AWS Lambda
- Azure Functions
- Google Cloud Functions
- Auto0 Webtask
- Oracle's Fn Project
- Kubeless
- Others

Down-sides:

- Neworking: Only accessed as private APIs.
- REQUIRED: An API Gateway (which the CSP probably provides for you, maybe at a cost).
- Larger services that are dependency heavy are not well suited to be ported to a serveless environment.
- Long-running processes (e.g. 300+ seconds) will get killed, so avoid implementing sevices that are longer-term and/or access external sevices in order to perform.
- Scaling might not have the configuration and capability you need (but maybe it will).

Functions As A Service (FaaS):

- Deploy individual Functions as components of larger business logic.
- Process individual requests within a timeout period.
- Invokation-based billint.
- Event-driven.
- "Instantaneously" scalable.
- Independent, Logical functions.
- Stateless.
- Ephemeral: Spin-up, do work, shut-down.
- Optional: Can be invoked manually.
- Managed entirely by CSP.

Serverless Solution Example:

- Web Server: Amazon S3 simple web server service.
- Lambda Function(s): Logging and data access (DB, JSON...) functions can be built as Functions.
- Security Token Service (STS): Temporary AWS credentials (API Key + Secret) for App users. Enables invoking Lambdas.
- User Authentication DB: AWS Cognito provides sign-up, sign-in to mobile and web apps. Allows OAuth or custom Ident Systems.
- Client App: UI, client-side rendering w/ JS and/or static HTML.
- Databse: AWS DynamoDB (NoSQL DB). Optional for serverless.

Common Serverless Frameworks and Architectures:

- Javascript, Python, Golang
- Apex: JS
- ClaudiaJS
- Sparta (Golang)
- Gordon (JS)
- Zappa (Python)
- Up (JS, Python, Golang, Crystal)

### Links to Serverless Resource Materials

[Serverless Examples](https://github.com/serverless/examples?ref=hackernoon.com)

[Anaibol Awesome-serverless](https://github.com/anaibol/awesome-serverless?ref=hackernoon.com)

[Build serverless contact form for static websites](https://hackernoon.com/building-serverless-contact-form-for-static-websites-b0e622d5a035?ref=hackernoon.com)

## Amazon AWS Amplify

## Data Modeling

## Footer

Return to [Root README](../README.html)
