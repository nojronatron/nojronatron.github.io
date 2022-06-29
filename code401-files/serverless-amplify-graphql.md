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



## Amazon AWS Amplify

## Data Modeling

## Footer

Return to [Root README](../README.html)
