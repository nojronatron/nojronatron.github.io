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

Purpose-built tools and features.

FE Web and Mobile full-stack apps on AWS.

Configure web, mobile, backend for your app, visually, with content management.

Tools:

- Amplify Studio: Build full-stack App FE+BE visually.
- Amplify Libraries: Conenct App to existing services (Cognito, S3, etc)
- Amplify CLI: Manage Amplify from your local terminal.
- Amplify Hosting: Host website or content.

Use Cases:

- User Authentication: Plug-in your app to gain AuthN and user controls.
- Build Backend Data Model.
- Visually build App UI and Backend.
- Host progressive webapp or static website.

AWS Amplify [Docs](https://docs.amplify.aws/)

## Data Modeling With GraphQL

There are a bunch of code snippets throughout this article.

AWS Amplify automatically creates:

- Dynamo DB
- GraphQL types (@model directive in schema => @hasOne, @hasMany, @belongsTo, @manyToMany)

Setup Tables:

1. `type Name @model { content: Type }`
1. `amplify push`

Queries:

Queries look like a JSON-related plain text file with a heierarchy.

Example query:

```sh
query QueryAllThings {
  listThings() {
    things {
      items {
        id
        content
        createdAt
        updatedAt
      }
    }
  }
}
# Lists all 'things' (and their fields/properties?)
```

Primary Key:

Configure by using `@model` directive and id will be automatic and primary.

Mark a 2nd field with `@primaryKey` to specify *it* as the actual primary key.

*Cannot change* primary key without deleting/recreating DB table.

Sort Keys:

Use `ID!` without `@primaryKey()` directive.

Secondary Index:

Underlying datasource is DynamoDB, a KVP type NoSQL DB.

Model access patterns with secondary indices with `@index` directive.

Hash Key: Strict equality tester.

Sort Key: Comparisons including GT, LT, non-strict-equals, starts/ends with, and between operations.

`sortKeyFields: ["fieldName"],` is used within the `@index` directive.

Relationships Between Models:

Uni-directional 1:1 releationship between 2 models: `@hasOne`

One-direction 1:N relationship between 2 models: `@hasMany`

Has One or Has Many bi-directionsl relationship: `@belongsTo`

Join-Tables between 2 models for N:N relationships: `@manyToMany`

*Note*: Avoid circular relationships between uni-directional relationship tables, or uni- and many- relationship tables.

Bi-directional HasOne and HasMany relationships can be configured.

Default Field Values:

Use `@default` directive for scalar type fields e.g. int, string, etc.

An example from *[Amplify Docs]*:

```sh
type Todo @model {
  content: String @default(value: "My new Todo")
}
```

Rename and Disable:

Can be done to GraphQL queries, mutations, and supscriptions with name overrides, and nulling a value.

Other Comments:

- Custom queries can be created.
- Lambda functions can be used for queries.
- Edit timestamp fields 'updatedAt' and 'createdAt' to custom names like 'createdOn' and 'updatedOn'.

### How It Works

See the bottom section of the site labeled [How It Works](https://docs.amplify.aws/cli/graphql/data-modeling/#create-multiple-relationships-between-two-models) for details on:

- Using the '@model' directive.
- TypeDefinition of '@model' directive.

## Footer

Return to [Root README](../README.html)
