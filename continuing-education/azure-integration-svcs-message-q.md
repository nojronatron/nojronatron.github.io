# MSFT Reactor Azure Integration Services Message Queueing with Azure Service Bus

## Hosts

Source: MSFT Reactor, Toronto, Ontario, Canada

- Fernando Rocha Silva, MSFT Sr. Cloud Solution Architect
- /in/fernandorochas
- github/rochabr

## Overview

This is the 2nd Session in a 4-part-series on Azure Integration Services.

## About Message Broker

What?

- An intermediate layer, decouples sender and receiver apps, allowing communications asynchronously, without direct knowledge of each other.
- Managed enterprise message broker.
- Scalable, secure, globally available.
- Standards and protocols compliance.
- Developer friendly: Client libraries and dev tools for many languages.
- Multiple integration capabilities: Event Grid, Power Platform, MS365, Analytics, etc.

Why?

- Producers send data to Consumers.
- Data type(s) might not be known (?).
- Consumer might be offline, message cannot be sent successfully.
- Scalability, reliability, and durability can be issues.
- Error handling, ordering, and event handling might not exist or be difficult to implement/address.
- Cross-component communication might not be compatible.
- Tightly coupled solution makes it difficult to scale the solution.
- Lack of asynchronous handling within, between endpoints.
- Monitoring and tracking is difficult without a centralized management system.

What about Kafka?

- Kafka can be used as a message broker.
- Kafka is more of a streaming system event handler.
- Service Bus is more of a system-to-system communication system.
- Azure Event Hubs has similar eventing and capacity handling as Kafka, but not Message Broker.

When to use Azure Service Bus?

- An async process that requires polling.
- Reliable state transition management needed for business processes.
- Messages cannot be lost nor duplicated.
- Messages need to be consumed in a particular order.
- Consistent, enterprise messaging is necessary.

## Patterns

- Brokered transfer with Queues: Queue will hold messages until Consumer is back online. Messages can be batched.
- Competing Consumer/Load Balancing: Multiple Consumers are subscribed for queued messages.
- Fan-In: Multple Producers' messages queued to send to a single Consumer.
- Fan-Out with Topics: Producer sends Topics to Subscribers via Subscriptions, managed by the Queue.
- Fan-Out with Topics and Filters: Multiple Topic-based producers to multiple subscribing Consumers.
- Deduplication: Duplicate messages can appear as a result of application and/or communications errors.
- Message Deferral: Consumer can receive and process, or defer it until later (ordering, too busy, etc).

### Dead-letter Queue

- Safely despart messages from single Producer to single Consumer.
- Consumer might not be able to process the message.
- Dead-letter Queue is a "return process" Queue that receives the "bad message" from the Consumer, and Producer can process the dead-letter and try to fix/resend it.

### Many Others

- Scheduled Delivery
- Message Sessions
- Message Browsing
- Auto-forwarding
- Transaction Processing
- Auto-delete on Idle
- Geo-disaster Recovery
- More: https://aka.ms/Azureservicebusdocs

## Security Features

- Virtual Network integration w/ Network Security Group support.
- Azure Private Link.
- Azure AD authentication.
- Data encryption: In-transit and at rest. Uses Azure or customer-managed keys.
- Data leakage/loss prevention.
- Sensitive data discovery and classification.
- End-to-end tracing and diagnostics.

## Summary Comments

It is not clear to me how I would use this service at this time.

My current projects, while network and multi-system oriented, are intended for networks that are not Cloud-connected, when Service Bus wouldn't be available.

## Resources

- Demo on [GitHub](https://aka.ms/AzureIntegrationServicesGitHub)
- [Patterns](https://aka.ms/Azureservicebusdocs)

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
