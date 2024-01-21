# MSFT Semantic Kernel and Vector Database

I recently watched a MSFT Reactor presentation on continous integration (CI) with LLMs and AI Models. There were two guests with the host. One of the guests mentioned Vector Databases and only briefly describe what they were, so I decided to do a little research.

Here are my notes on the topic.

## Introduction

A Vector DB is a component available for use with Semantic Kernel. It helps an AI 'remember things'.

- What is a vector database, exactly?
- What is vector encoding?
- What vector database tools are out there?

## Semantic Kernel Overview

It's an SDK:

- Open source
- Build agents using SDK to call your code
- Leverage OpenAI, Azure OpenAI, Hugging Face, and other AI models
- Supports C#, Python, and Java

It's an Orchestration Layer:

- Between Copilots and Plugin extensibility (above), and Foundation models and AI infrastructure (below).
- Allows combining AI models and plugins.
- Enables building custom Copilot experiences on top of AI plugins.
- Any AI service can be integrated via Semantic Kernel

Capabilities:

- Go beyond a simple chat bot.
- Automate processes using AI.
- Given a description of existing code, models can call the code via orchestration of Semantic Kernel.

Example Projects:

- Send email.
- Update databses.
- Switch a lamp on/off.
- Azure-Samples/miyagi [Project Miyagi - Envisioning sample for Copilot stack](https://github.com/Azure-Samples/miyagi)

### How to Use Semantic Kernel

Leverages attributes such as `[KernelFunction]` and `[Description]` to markup code for Semantic Kernel to process and orchestrate.

Describing code seems to mean: Hey Copilot & underlying AI models, here are the functions in my code and you are allow to use them.

Plugins/Code needs to be provided to the AI via the `Kernel` object. "Having the kernel" allows coding around the kernel instance to enable actions based on inputs (e.g. Chat-bot conversation that turns on/off a "lamp").

### Plugins

Plugins are _your custom code_.

- Markup your uplugin code with attributes that Semantic Kernel understands.
- Instantiate Kernel instance to leverage AI models and Copilot stacks.
- Call the Kernel instance to interface your code.

Semantic Kernel can be used as an "abstraction layer over OpenAI and Azure OpenAI services to run handcrafted prompts".

"Real power ... comes from combining ... components together."

## Vector DB

Vector DB stores data:

- As "high-dimensional vectors" aka "mathematical representations of features or attributes".
- Complexity and granularity of data contributes to the dimension depth of the data (100's to 1000's of dimensions).
- Vectors are transformed from images, documents, audio etc into raw data for storage.
- Machine Learning models, word embeddings, and feature extract algorithms are used to make vector transformations.

Advantages:

- Fast, accurate search of data.
- Bases similarity (hence search reliability) on 'vector distance'.
- Similar results are returned, rather than SQL-like 'exact matches'.
- Results based on semantic or contextual meaning (near-vector results).

What Are Vector DBs used for? _[MSFT Learn documentation]_

- Find images similar to a given image based on content and style.
- Find documents similar to given base on topic and sentiment.
- Find products similar to given based on features and ratings.

Querying Complexity:

- Can query a type-for-type: Supply an image to an image-based vector db.
- Can query a vector db across types: Supply text to describe an image to an image-based vector db.

Use Cases:

- Domains include Natural Language Processing (NLP), Computer Vision (CV), Recommendation Systems (RS), and others related to understanding matched data.
- Enabling Large Language Models (LLMs). This adds 'coherence' to LLM text-based responses.

### Vector Encoding

Vector encoding is the process of transforming an input type (such as an image or sound file) into raw data for storage in a vector database.

### Vector DB Tools

Azure has Vector DB Tools and Services:

- Azure Cosmos DB Vector Database Extension.
- Azure PostgreSQL Server pgvector Extension.
- Azure AI Search.

Other Connectors (partial list):

- Vector Database in Azure Cosmos DB for MongoDB vCore.
- Chroma.
- DuckDB.
- Milvus.
- MongoDB Atlas Vector Search.
- Pinecone.
- Postgres.
- Redis.
- Sqlite.

See more at [vector-db Available connectors to vector databases](https://learn.microsoft.com/en-us/semantic-kernel/memories/vector-db#available-connectors-to-vector-databases) at MSFT Learn.

## References and Related Topics

- MSFT Learn documentation on [Semantic Kernel](https://learn.microsoft.com/en-us/semantic-kernel/overview/).
- MSFT Learn topic 'Giving your AI memories' sub-topic [Store context in vector database](https://learn.microsoft.com/en-us/semantic-kernel/memories/vector-db).
- MSFT Learn Module [Machine Learning](https://learn.microsoft.com/en-us/training/modules/introduction-to-machine-learning/).
- My notes on [Machine Learning](./about-machine-learning.html).

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root README](../README.html)
