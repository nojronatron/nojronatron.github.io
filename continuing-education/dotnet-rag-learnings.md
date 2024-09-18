# DotNET Retreival Augmented Generation Notes and Learnings

Microsoft Reactor has been hosting online Meetups focused on Retreival Augmented Generation and related AI and Copilot topics. Other Microsoft events also cover similar topics. This page contains notes taken while attending or reviewing these events, with the goals of expanding my understanding and building a basis upon which to use Generative AI and RAG in my own applications.

## Building RAG Apps in .NET

Presenters:

- Jordan Matthiesen, Sr. Program Manager
- Luis Quinanilla, Sr. Product Manager
- Bruno Capuano, Principal Cloud Advocate

RAG (very succinctly):

- LLMs are trained with a specific set of data.
- To add specific knowledge or your own data, several techniques are available, RAG is one.
- Provide more up-to-date public knowledge to a Model.
- Enables access to internal knowledge through RAG.
- RAG is comprised of: Retreiver, LLM, Glue, and Features.
- Retreiver: A knowledge base that can be used to retreive sources matching a query. Example: Azure AI Search.
- Langchain, Llamaindex, and Semantic Kernel are examples of the "Glue" that bind a "Retriever" and LLMs, enabling chat history, feedback buttons, text-to-speech, user login, file upload, access controls, etc.

Note: Small Language Models could be used (RAG is not tied to a specific model, SLM, LLM, or otherwise).

### Common Tools To Spin Up a RAG App

- Azure Developer CLI
- .net 8
- git
- Docker
- PowerShell

## Resources and Links

- [Python "RAG Chat" solution](https://aka.ms/ragchat) shows examples on how to interact with LLM's in Q&A mode.
- Another [RAG Chat Example App](https://aka.ms/ragchatnet).

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
