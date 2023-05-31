# Integrate ChatGPT Into Apps

Microsoft Reactor held an online presentation on this topic.

I expect this notes page to grow as new and updated information is discovered.

## MS Reactor Integrating ChatGPT into Apps

Host: Korey Stegared-Pace

Guest: Henri Shulte, Cloud Solution Architect, MSFT

- Located in Denmark.
- AI focused job.

### ChatGPT API Basics

OpenAI is open for professional use.

ChatGPT UI is a Q&A based 'chatbot' style interface.

ChatGPT can be extended to operate on your own data.

Use Case:

- Don't want the user to ask any questions (unlike ChatGPT).
- Rules and Roles should be utilized to scope behavior to the specific application.
- Integrate responses within the app (vs using a chat UI).
- Model must retrieve from specified sources.

System Message:

- Controls and limiting responses through Roles.
- System Role: The overarching controller.
- Assistant Role: OpenAI.
- User Role: The human chatting with the Assistant.
- Define these roles in the openai framework setup. Multiple arrays of profiles, limitations, and capabilities of the Assistant agent.

Korey showed Jupyter Notebook code showing that 'openai' must be imported.

- API Keys are required.
- An organization partition definition is optional.

Chat History:

- Must be stored and tracked so the Assistant contextualized responses properly.
- Follow-on questions and responses require history.

Prompt Injection:

- Delimiters and Instructions: Help put guidance around what the user could say.
- Define a prompt and capture an object that represents the customers prompt responses.
- Should include knowledge of who the entity is, the entity's relationship to the user, other context like date, time, season, etc.

Formatted Responses:

- Backend receives requests from FE/UI and manages API Calls to OpenAI/Chat GPT.
- Backend can do additional processing in between.
- Formatting can be accomplished using JSON, HTML, Markdown, etc.

In the end:

- Setup and pre-processing includes history, prompt injection, and system message info.
- Payload might include: Model, messages, temperature, maximum tokens, etc.
- Just make an HTTP POST request and process the response.
- Validation of the AI responses might be necessary. Henri built a custom private method that accepts the API response and parses it to ensure various tokens exists or otherwise normalizes the response data, appropriate for an end user.
- If the API response payload just needs to be processed and not returned to a user, then JSON responses can be used for processing. Simply validate the JSON and then parse and process it.

Going Forward:

- Consider using Azure Cognitive Services to implement speech response on top of the GPT response.

## Prompt Injection Explained

[YouTube Video](https://www.youtube.com/watch?v=FgxwCaL6UTA&ab_channel=SimonWillison)

## References

[Learn how to work with the ChatGPT and GPT-4 Models](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/how-to/chatgpt?pivots=programming-language-chat-completions).

[Azure OpenAI Service Documentation](https://learn.microsoft.com/en-us/azure/cognitive-services/openai).

[Module: Introduction to Azure OpenAI Service](https://learn.microsoft.com/en-us/training/modules/explore-azure-openai).

[System message framework and template recommendations for LLMs](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/concepts/system-message).

## Footer

Return to [ConteEd index](./conted-index.html)

Return to [Root README](../README.html)
