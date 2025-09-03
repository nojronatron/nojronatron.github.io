# Generative AI Techniques

Notes from a Microsoft Reactor presentation on Generative AI.

## Generative AI For Beginners Java Edition

Rory Preddy

Core Techniques To Master:

- Completions
- RAG
- Functions
- Agents (which utilize Functions, RAG, and Completions)

### Completions and Chat

Completions:

1. System Persona and User Prompt
2. LLM: Controls max tokens and temperature
3. Single Reply

Multi-turn Conversation:

- Maintains a history
- Appends history into persona context for subsequent questions
- Context grows
- Token count increases

Interactive Chat:

- Looping through multi-turn conversation
- Trims contenxt and token usage

Trimming can actually be a problem due to loss of older context data

### RAG

Retreival Augmented Generation:

- Retrieve supporting data + prompt
- Data sources are injected into the Retrieve stage
- Augment prompt with supporting data
- Generate a response using LLM + Prompt + Supporting data

Useful for loading documents and other data so Completions and Chat can use it as part of the Context.

- Aka "Grounding" the AI with custom data (context)
- Can be configured to _only_ use target document(s) for its Context
- A temperature closer to 1 will allow the LLM to guess (hallucinate) it's way to a response
- Temperature closer to 0 will steer the LLM to not guess and return an unknown response if contextually relevant information is not found in the target document(s)

Functions and RAG use the same context concepts, as Functions followed RAG.

### Functions

Real-time calls:

1. User prompts
2. LLM processes the prompt to get contextually important data
3. Function (local or cloud) that finds a response
4. LLM-enhanced response given function result

Keywords within the prompt trigger the LLM to try calling a related function.

### Responsible AI

Limit harmful content, basic hate speech, and simple jailbreaks (GitHub Models do these).

### Azure AI Integration

Container-based (Kubernetes) application can be generated using the Azure Search OpenAI Demo (Java) repo.

### Q and A

GPT 5 removed Temperature?

> True.

Rate limiting issues?

> Stick with GPT 4o mini (and some others) to limit Token limit issues.

## Resources

[MSFT: Gen AI For Beginners (Java) repo](https://github.com/microsoft/Generative-AI-for-beginners-java)

[MSFT: Azure Search OpenAI Demo (Java) repo](https://github.com/Azure-Samples/azure-search-openai-demo-java)

[MSFT Learn: Quickstart Create a New Agent](https://learn.microsoft.com/en-us/azure/ai-foundry/agents/quickstart?pivots=programming-language-java)
