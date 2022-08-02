# AWS Amplify

What is it? Pros? Cons?

## References

AWS Amplify on [Be A Better Dev.com](https://beabetterdev.com/2021/09/22/what-is-aws-amplify/)

## Overview

Full-stack devepment toolkit.

Relies on Amazon AWS and integrates with Amazon Cloud.

Designed for full-scale setup, test, launch, and scale of production-ready apps.

"Minimal time focusing on the details."

## What Is AWS Amplify

Born November 2017.

Google Firebase and Netlify are direct competitors.

Amplify offers direct feature integration with AWS' backend services.

Is a: Toolchain => build and deploy entire apps.

Can be used for backend only, but aimed at full-stack deployments.

Supports JS, React, and Angular.

Mobile-support is there: React Native, Android, and iOS.

Has a CLI, and a limited-feature UI for day-to-day administrative tasks.

Supports:

- Storage => Amazon S3
- Authentication => Also Authorization: Amazon Cognito
- Monitoring
- PubSub functions
- Managed Hosting
- Manage Users
- GraphQL, REST, API => AWS Appsync or API Gateway
- Functions
- CI/CD
- Content Management
- Analytics
- Code/Pull Request Reviews
- Interactions
- AI/ML and Predictions
- Monitoring
- Push Notifications
- Custom Domains
- Simple Notification Service (SNS)
- Simple Queue Service (SQS)
- Serverless Compute: AWS Lambda
- DataStore => Amazon DynamoDB

## CLI

Install as a library.

Setup Commands:

- amplify configure
- amplify init

API Setup:

- amplify add api

CLI will generate code to place in your API, which can be modified to suit your app requirements.

## Admin UI

Data Model Studio: Add DataModels w/ Fields and Type settings, configure data relationships and DB schema. Will generate indices of relational data too.

Can think of Admin UI as a physical view of components.

## Pros of Amplify

1. Get Started Quickly: Run a few CLI commands to get going for prototyping or production deployments.
1. Fast Dev Cycles: App moves between dev, test, A/B or Blue/Gree stages very rapidly.
1. Simplified Cloud: Functions and features of the Cloud are available as Components to add to your App.

## Cons of Amplify

1. Don't *learn* the AWS services.
1. Collaboration issues, perhaps oriented to solo-engineers.
1. Boxed-in to currently available feature set.
1. Surprise Bills. Azure has tackled this problem fairly well after several years. Adding functionality will deploy Services that have cost implications. Also, serverless functions are pay-per-use and can help mitigate 'surprise bill' events.

## AWS CloudFormation

Define templates for complonents.

Deploy resources to the cloud.

More details on CloudFormation [here](https://www.beabetterdev.com/2020/12/06/aws-cloudformation-tutorial/?_gl=1*1e2oi00*_ga*MTA3MTMwNTU4MS4xNjU2Mzk3MTcx*_ga_9YXSREER7T*MTY1NjM5NzE3MC4xLjAuMTY1NjM5NzE3MC4w&_ga=2.160987389.171189771.1656397171-1071305581.1656397171)

## Footer

Return to [Root Readme](../README.html)
