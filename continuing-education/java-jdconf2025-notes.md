# JDConf 2025 Notes

Microsoft hosted a virtual Java Developer Conference on April 9, 2025 (its 5th year).

Host: Bruno Borges, Manager, MSFT

## Table of Contents

- [Keynote](#keynote)
- [Agentic Implementation Using Java and Spring Framework](#agentic-implementation-using-java-and-spring-framework)
- [Boost AI Dev Experience with Quarkus, LangChain4j, Azure OpenAI](#boost-ai-dev-experience-with-quarkus-langchain4j-azure-openai)
- [How to think about Building Agents in SpringAI](#how-to-think-about-building-agents-in-springai)
- [Discussion](#discussion)
- [What Comes After Jakarta EE 11](#what-comes-after-jakarta-ee-11)
- [Production Best Practices - Dev To Delivered](#production-best-practices---dev-to-delivered)
- [Performance InstantOn vs CRaC vs Native Image](#performance-instanton-vs-crac-vs-native-image)
- [AI-Driven Test Development](#ai-driven-test-development)
- [References](#references)
- [Footer](#footer)

## Keynote

Presenters:

- Amanda Silver, MSFT
- Josh Long, Broadcom
- Lize Raes, Naboo.ai

Topic briefs:

- Java is thriving
- MSFT supports Java:
  - VS Code, GitHub, and Azure
  - Github Copilot understands Java (VS Code, IntelliJ, and Eclipse support)
  - BTW: MSFT uses Java internally and also sponsors Open JDK and Adoptium
- MSFT offers services and platforms for Java development, test, deployment, and maintenance
  - Azure, AI tools (OpenAI, AI Search, AI Foundry), Copilot, IDE, PaaS, Container Services, DB services

Spring AI and LangChain4j Community Notes:

- Josh Long and Lize Raes present
- Demonstrated using Initizr to quickly init a SpringAI project
- Various integrations with Azure OpenAI, and many LLM's and local models (JLlama, OpenLlama, etc)
- Observability, guardRails, Audio, Advanced RAG, and Evaluation Framework
- LangChain4j v1.0 nearing release:
  - Few-Shot (model examples)
  - Caching
  - Agents
  - WOrkflow orchestration
  - Other new integrations coming
  - Support from MSFT

Demo: Java upgrade in VSCode with Github Copilot

- Github Copilot Upgrade Assistance for Java!
- Java 8 to Java 21
- Upgrade Project workflow analyzes and upgrades project (and code) for you
- Upgrade Project tool also runs unit tests
- Developer manages Copilots actions (just like dev time experience)

## Agentic Implementation Using Java and Spring Framework

Presenter: Josh Long, Spring Developer Advocate, Kotlin Dev (GDE)

Stream:

- Java releases are now on a 6-month cycle
- Initializr speeds up project ramp-up:
  - Now supports SpringBoot AI
- Anthropic MCP: Expose business logic to your model

## Boost AI Dev Experience with Quarkus, LangChain4j, Azure OpenAI

Presenter: Daniel Oh, Developer Advocate, Red Hat, and Java Champion among many other things!

Stream:

- AI Services can employ declarative approach to define LLM interactions: aka "Ambassador"
- Quarkus: Bootstrap the Java AI Model app dev using Azure OpenAI (others could be used instead of Azure OpenAI)
- API Keys must be in configuration
- "@Tool" describes when to use the tool
- "@RegisterAiService" registers the tool
- Embedding documents (RAG) using a doc store and an "Augmentation Interface"
- LangChain4j provides a simpler way to define RAG with a simple path to documents

## How to think about Building Agents in SpringAI

Speaker: Adib Saikali,

Stream:

- Shouldn't an Agent figure out the implicit requirements of a user's prompt?
- Adding AI to apps also adds complexity _but_ also adds proactive responses
- Agentic Systems: Leverage AI models to interact and fulfill user prompted tasks
- Agentic Loop: LLM (brain: reasoning, planning) -> (Interactions with its environment) Tools
- Workflow-based Agents improve interaction and results (perhaps in lieu of 100% automated Agent capability?)
- "Agentic Workflows": Definitions created ahead of time to enable routed or parallel decision making for an Agent

## Discussion

Participants:

- Bruno Borges
- Adib Saikali
- Emily Jiang
- Reza Rahman

Notes:

- Good to see AI benefits coming to fruition.
- Agentic AI will be taking over from non-Agentic in the coming months.

## What Comes After Jakarta EE 11

Speakers:

- Reza Rahman, Program Manager, Microsoft
- Emily Jiang, Cloud Architect and Java Champion, IBM

Stream:

- Formerly known as Java EE, now open-source platform for enterprise application development
- Jakarta is multi-vendor!
- No roadmap!
- Needs open-source contributors to move it forward
  - See [Jakarta EE Ambassadors contrib guide](https://aka.ms/ee12-contributor-guide)
  - High level overview of the program
- What is JakartaEE about?
  - CDI Alignment: Various JDK capabilities, better CDI support in REST, Concurrency, more...
  - Java SE Alignment: JSON Binding Records, Bootstrap API, Modernized TCKs, more...
  - Closing standardization gaps: HTTP/3, JWT, more...
  - Deprecation and removal items: SOAP, XML, CORBA, more...
  - Areas of Innovation: Data, NoSQL, MVC, Configuration, gRPC
  - Jakarta Messaging: Modernize MessageListener, bootstrap API, interop with AMQP, and a future "lite" version
- Security:
  - JWT alignment and spec for "MicroProfile JWT Bridge"
  - Modernize Roles based on CDI
  - "EL-enabled authorization annotation" (avoid using XML, in favor of Annotations)
- Configuration:
  - MicroProfile added to Jakarta Config
  - Programmatic lookup and CDI injection
  - "Layer config sources"
- There are other areas where efforts to improve for enterprise development

## Production Best Practices - Dev To Delivered

Presenter: Mark Heckler, Principal Cloud Advocate Java/JVM, MSFT

"How to go from dev to delivered and stay there"

Stream:

- Best practices: App dev, infra as code, CI/CD, monitoring, management, production patching, and security
- App best practices:
  - Configuration
  - Actuator: Foundation for tools to support config andn observability
  - Observability
  - Error handling & resilience: Circuit breakers, etc
- Containerization:
  - FYI: Docker uses "OCI Compliant" imaging technology
  - Minimal base images
  - Runtime vs. build deps
  - Multi-stage Dockerfile
  - IaC: Infrastructure as Code
- Minimal base images:
  - Smaller containers and configuration is _better_
  - Use a smaller base image such as "distroless": mcr.microsoft.com/openjdk/jdk:21-distroless
- Multi-stage Dockerfile:
  - Multi-stage containeraization
  - Stage 1: pul in larger JDK
  - Stage 2: Create the runtime image using minimal JDK image and actual app build and configure
  - Stage 3: CI/CD Pipelines
- SpringBOot Tools for Containerization
  - Existing Mvnw and Gradlew templates to build images
  - Maven: `./mvnw spring-boot:build-image`
  - Gradlew: `./gradlew bootBuildImage`
- IaC:
  - Azure: ARM templates (JSON), Bicep (declarative, less verbose than JSON), Terraform/OpenTofu (fully declarative syntax), etc
  - State management
  - Environment separattion capability
  - Repeatable
- IaC Principles:
  - Version control
  - Consistency
  - Documentation
  - Automated testing and validation
  - Idempotency
- CI/CD:
  - Define a refined, repeatable workflow
  - Manage secrets
  - Dev and Test, Deploy to Develpment, Deploy to Production, etc
  - Reusable, support multiple workflows with templates and linking workflow definitions
- Build and Test Workflows
  - Validate functionaligy
  - Ensure reliability
  - Verify security
- GH Action Workflows
  - Use exact action versions
  - Minimize secrets usage
  - Implement timeouts
  - Add concurrency controls
  - Create reusable workflows
  - Implement comprehensive testing
  - Use caching
  - Set up Notifications
- Monitoring:
  - Integate with Azure/Cloud monitoring
  - Application insights
  - Implement custom metrics
  - Add Log Analytics

An example of leveraging a Docker Container for a Java app:

```Dockerfile
FROM eclipse-termurin:latest
COPY project.jar /app.jar
EXPOSE port
CMD ["java", "-jar", "/app.jar"]
```

## Performance: InstantOn vs CRaC vs Native Image

Presenters:

- YK Chang, IBM
- Rich Hagarty, IBM

Stream:

- Java is:
  - _30 years old_
  - Critical to companies' core workloads and processes
- Upcoming:
  - Cloud-native "resurgence"
  - Lew infra to maintain an dmanage
  - Flexibility and scalability of Java
  - Easier to roll-out new releases
  - Security
- Re-architect monolithic Java app to Cloud:
  - Java-specific issues will be encountered (it wasn't designed for containerization, etc)
  - JVM, bytecode, machine language, JIT
  - JIT causes CPU spikes especially at start-up of Java app
  - JIT causes memory spikes as it loads methods during compilation at runtime
  - Steady-state not reached for some time after initial startup
- Java has:
  - JIT runtime compilation
  - Garbage collection ("great" GC)
  - Regular update pipelines (is OSS JDKs and paid EE JDKs)
- Wish List for JDK Cloud performance:
  - Fewer resources equaltes to lowered costs
  - Better performance in ramp-up, throughput, and horizontal scaling
- OSS:
  - Open JDK CRaC, Liberty InstantOn, GraalVM Native-image
  - Reduce startup time and/or minimize container image size
- CRaC:
  - Coordinated Restore and Checkpoint
  - Register 'resources' to get notifications before and after checkpointing
  - Interleave `beforeCheckpoint()` and `afterCheckpoint()` to manage CRaC during runtime
  - Linux-only, meant to be run in containers
  - Micronaut: OSS SDK for Java17 and up, Groovy, Kotlin, Maven, Gradle, JUnit, Spock, Kotest
- Open Liberty InstantOn
  - Full Stack solution: JVM, JDK, Java Framework
  - Speeds up start-up
  - Ideal for cloud function and scale-to-zero workloads
  - Leverages Linux CRIU for checkpoint/restore operations
  - Slightly larger image, but tradeoff favors overall performance and security
- NativeImage
  - Oracle GraalVM technology
  - No code loaded a run time
  - JIT and JVM affected capability
  - Focused on very fast startup
  - Long-running instances _will see degraded performance_ (because GraalVM is only focused on startup)
  - Compile-time is _much longer_ than without (due to specific startup enhancement calculations)
  - Lacks full Java API support
  - Me: THis sounds a bit like ahead-of-time compilation, but limited to only the start-up paths
- Overall:
  - Seems to be a trade-off between startup and runtime performance, and security
  - Pick what matters for the instance purpose and cloud deployment goals

## AI-Driven Test Development

Presenter: Loiane Groner, Dir Engineering, Bank of New York, Java Champion and MSFT MVP

"Test Smarter Not Harder"

Stream:

- There are still applications that don't have _any tests_ associated with it
- Often-times code is first, then tests are written, only to find the business logic fails
- Using AI, speed development of tests defining business logic, reducing time to actually code (and validate) business code
- Two Approaches to testing using AI: Rely entirely on the AI, or use AI to simplify code, reduce duplication, or other help while writing test code
- An additional approach is to write enough test code for a test case so that Copilot will "get the idea" and start writing more code and/or assertions
- Suggested code can be Accepted or Rejected
- AI uses input file(s) or a project (workspace) to get context to write tests:
  - Highlighting the class code page only provides that codepage as context
  - Drag-and-drop a file into the Chat window to leverage the dragged file as context
- Use `New` to create a fresh Chat Window from scratch, without previously introduced context
- Utilize `@workspace` to provide more context to Copilot:
  - Provides better results in many cases
  - Can take longer to generate results
- Copilot starts to incorporate the developer's _code style_ as it is used interactively

## References

- [Jakarta EE Ambassadors contrib guide](https://aka.ms/ee12-contributor-guide)
- [Daniels Quarkus repo on Github](https://github.com/danieloh30/quarkus-azure-ai.git)
- [Code.Quarkus.io](https://code.quarkus.io)
- [Java Learn](https://aka.ms/javalearn) resources from Mark Heckler
- Get on the [Jakarta EE Mailing List](jakarta.ee/connect/mailing-list)

## Footer

Return to [Conted INdex](./conted-index.html)

Return to [Root README](../README.html)
