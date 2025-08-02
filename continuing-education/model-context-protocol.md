# Model Context Protocol (MCP) Learnings

## Let's Learn MCP: C-Sharp

Part of a series by the DotNET team and Microsoft Reactor.

Hosts:

- Katie Savage
- James Montemagno

## Requirements

- VS Code/Visual Studio
- Node.js
- Docker Desktop
- .NET 9 SDK
- C# Dev Kit Extension for VSCode

Note: Visual Studio does not leverage the C# Dev Kit, so some steps are slightly different, but concepts and result will be the same.

## Notes

Agentic Coding:

- Big change vs AI-assisted task execution
- Multi-step task execution
- More like a pair programmer than AI
- Needs a real-time context to be aware of external tools and capabilities
- Integration chaos starts, trying to add externalities to AI workflows!

MCP:

- Integrates external tools (external to Dev Environment) into Agentic workflow
- Provides a standardized protocol to connect LLM to real-time context
- "A universal adapter for AI Applications" -Katie Savage
- "A single interface for LLMS" -James Montemagno
- Created by Anthroipic and adopted by the AI community as a standard
- Can be used for many task types and purposes: _Not just for developers_

Parts of MCP:

- Hosts: Windows, VS, VSCode, Copilot Studio, etc. Tools that need access to data via the MCP protocol
- Clients: GH Copilots and AI/LLMS. The go-between.
- Servers: Lightweight programs that expose capabilities through MCP. GH, Azure, Playwright, etc

MCP JSON File:

- Sharable MCP config
- `mcp.json`
- Store in `root/.vscode` directory
- Names the server, sets startup command with defined arguments
- Optionally can provide environment variables `"env": { ... }`
- Can be used to start MCP server(s)

MCP Servers:

- Can be local or remote
- Custom (by you) or canned (templated) such as the GitHub MCP Server
- Add these MCP Server configs to `mcp.json` (supported in VSCode _and_ Visual Studio)
- Expose Tools, Resources, and Prompts

Authentication:

- Automatic OAuth Connect, OID, etc
- Authentication: Might pass-thru if already logged-in to your IDE

Best Practices:

- Add a custom CoPilot Instructions file: `copilot-instructions.md`

Generally:

- The GitHub MCP Server sits on top of the GH API, allowing access to a scoped list of endpoints
- The GitHub MCP Server provides endpoints that allow listing issues or commits, creating PRs, etc
- Any available GH CoPilot models can be used with your MCP Server(s)

MCP Clients:

- Invoke Tools
- Query for Resources
- Interpolate prompts

MCP Tools:

- An MCP Feature
- Functions an LLM can invoke to perform actions (function calling)
- EG: Send email, update todos, run tests, file GH Issues
- There are user controls like: Per-Chat and Mention
- There are also user-defineable Toolsets that can be created

MCP Resources:

- Expose data in a read-only fasion
- Exposed as URIs EG: `client/agent/user`
- Can be Files, Documents, DB Entries (and schemas), Images, etc

MCP Prompts:

- Pre-defined templates for AI tasks
- Invoked by the user
- Static presets
- Reusable with placeholders
- Dynamically generated
- Can be _returned by the MCP Server_

Use Cases:

- Onbolaring prompts to welcome users
- Common workflows with parameters
- Context ...

### Building an MCP Server

Official SDKs: C#, Java, Kotlin, Python, TS

C# SDK:

- Clients
- Servers
- Local (standard IO transport)
- Remote: Server-sent Events
- Remote_ Streamable HTTP

NuGet Packages:

- ModelContextProtocol
- ModelContextProtocol.Core
- ModelContextProtocol.AspNetCore (HTTP Server)

Get Started:

1. `dotnet new console -n {ProjectName}`
1. Add the NuGet packages
1. Update Program.cs with usings
1. Use `CreateEmptyApplicationBuilder(settings)`
1. Use HostBuilder to complete server config and add (for example) `.AddMcpServer()` and `.WithStdioServerTransport()`
1. Do `await builder.Build().RunAsync();` to startup at the end of Program.cs
1. Do `npm install --global mcp-inspector` (for runtime)

Start Creating Services:

- Add services to the project
- New file named by convention `{mcpName}Service.cs`
- Has data that it tries to load (a file for example)
- Could also have a SeedData method
- Also include methods that define the business logic: Endpoints for LLM's to call
- Also include specific Types and Classes to manage data transfer and state within methods

Create and Expose Tools:

- New file named by convention `{mcpName}Tools.cs`
- Define a tooltype using `[McpServerToolType]` attribute
- Inject necessary services from DI
- Integrate Tools into the Service(s)
- Att attribute to introduce methods exposed as a tool: `[McpServerTool, Description(string)]`

Build and Run:

- Build like usual
- Run the app and connect to VSCode and MCP Inspector
- `npx @modelcontextprotocol/inspeactor dotnet run`
- Update `mcp.json` to define the MCP Server
- Start using Copilot Chat to interact using your MCP Server!

MCP Inspector:

- Node.js application
- Install using `npm install --global mcp-inspector`
- UI is a webapp that MCP Server can connect to
- UI is a Mgmt display that helps to run defined custom tools
- Used as a dev and test utility!

## Other Stuff

- Create a new GitIgnore file for a current project: `dotnet new gitignore`
- CoPilot Instructions file can tell CoPilot where your repo is: `It is on GitHub at {url}` to provide more context
- Ask Copilot to brainstorm _for_ you (and _with_ your prompt inputs to steer it) when developing new projects!
- Copilot Agent Mode will often time write code directly from prompts. It's a good idea to tell Copilot to keep results in Chat so that code can be reviewed _before_ telling Copilot to write the code to a new (or existing) file
- MCP can be run to call local data sources, remote servers (Azure Functions, SQLAzure, WebAPIs, etc)
- MCP can be a Container App
- MCP SDKs are available for most common environments (DotNET, JS, Python, etc)

## Q&A

Q: Is GH Copilot required to utilize MCP Servers?

Q: How to add AuthN and AuthZ to MCP Endpoints?

> SDKs have a standardized way for clients to implement, supporting these.

Q: Why not just use Swagger to expose the API?

> There should be a standardized way to expose MCP to LLMs.

Q: Connect RAG with MCP?

> Use AI Extensions in VS Code to call into LLMs that are local or remote. "Sampling" package allows bi-directional (and experimental) to do this.

Q: What if host is running as a WebApp?

> That's where ASP.NET is, so use it to deploy MCP Tools and Services.

Q: Support for Azure Semantic Kernel?

> Yes, support is there (details not shared)

Q: What is MCP Server goes down?

> Error message if not able to connect (like ASP.NET and other HTTP services).

## Resources

- [Model Context Protocol](modelcontextprotocol.io) paper
- July 29th and 30th: [MCP Dev Days](https://aka.ms/mcpdevdays)
- [C# MCP SDK](https://aka.ms/csharp-sdk-mcp)
- Ideas and best practices for [Github Copilot Customizations](https://github.com/github/awesome-copilot)
- [James Montemagno's Lets Learn MCP CSharp repo](https://github.com/jamesmontemagno/letslearnmcp-csharp)
- [List of MCP templates](https://code.visualstudio.com) -> click the MCP navigation link

## Footer

- [Return to ContEd Index](./conted-index.md)
- [Return to Root README](../README.md)
