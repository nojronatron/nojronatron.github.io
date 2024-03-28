# JDConf 2024 Notes

The Virtual Java Developer Conference

Weds March 27, 2024 (US/Americas)

## Intro and Keynote

Host: Bruno Borges, Prin PM Manager, Java Engineering Group, MSFT

- Memory enhancements
- SpringBoot 3

Julia Liuson, Pres MSFT Developer Division and GitHub:

Focus areas:

- Leverage MSFT tech and AI with Java.
- Improve Java development workflow.
- LinkedIn, Minecraft, Bing, and MSFT Azure all utilize Java, Kafka Clusters, and Java Frameworks.
- Playwright for Java!
- MSFT Dev Box and MSBuild + OpenJDK.
- GitHub Copilot (note: IntelliJ extension!) and Codespaces support.
- Spring Apps, Container Apps, Kubernetes, App Services, etc all support Java.
- Cloud support for Oracle, Tanzu, RedHat, IBM, Tomcat, GitHub, and Azure, all enable Spring Boot, IntelliJ, Maven, Gradle, and Eclipse build, test, and deploy support.

Josh Long Spring Developer Advocate - Tanzu by Broadcomm:

- Java 21 just released, includes virtual threads.
- Azure Spring Apps Enterprise.
- AI integrations into (Java or Spring?).
- SpringBoot 3.2 includes above bullet-points.

## Project Valhalla - Speed Up The JVM

Theresa Mammarella - IBM Software Engineer on Runtimes Team, Open J9:

- Memory-fetch now takes much longer than a simple addition operation (compared to when Java was initially released) due to multi-level memory caches, so a single cache-mis can cost 1000x cycles to grab the next-level cache.
- Not a dire situation but there is room for improvement (Java is already pretty effecient).
- Using pointers (refs) can actually slow down processing due to memory locations being "pushed down" to another level of cache.
- Garbage Collection: Does not know about all references (exactly) due to spread of pointers throughout multiple levels of cache. Note: Not all GCs are created equal and will behave differently.
- Header information increases Heap Size utilization, which might no longer fit within the cache.
- Equals() compares values, whereas `==` compares identifiers of objects, which is done for Field mutability and synchronization.
- By flattening Java Objects into more like a primitive, memory can be saved and is cache-efficient, without compromising abstraction.
- JEP 401 Value Classes: Not released. Introduces "Class without Identity", which causes initialized classes to become immutable ('Final'). This enables nullability (unlike primitives) and causes the equals operator `==` to behave the same as the Equals method `Equals()`.
- Implicit CTORs are required, along with some other syntax markup (`!`) for example, to encourage "flattening" in the JVM.

## Empower Quarkus APps with AI, Open Telemetry, Kubernetes

Daniel Oh - Dev Advocate, Java Champ, RedHat

Brian Benz - Cloud Advocate, Java Champ, MSFT

## Production AI Using Java Apps

Mark Heckler, MSFT

## VSCode Mastery With Java

Loiana Groner, Citibank

Using VSCode professionally to build Java-based products.

- Extensions, Spring suport, linting and vulnerabilities, testing and coverage, Docker and DB support.
- Java + Spring Extension Pack has stack of Extensions to support Java development, build, test, and deployment.
- Command Pallette: "Java" :arrow_right: Shows list of commands supported by the Extension pack.
- Can also download JDKs and configure JVMs directly in VSCode.
- Remember Spring Initializr? That is in the Command Pallette now to frame-in Maven or Gradle project types.
- Java Extensions supports MS-SQL, MySQL, and PostgreSQL, as well as Kotlin, JAR file output, etc.
- Dependencies can be selected while in the Command Pallette at the start, or during a project by right-click POM.xml and select the Dependency selection/adding tool.
- Run-Debug can be launched via a Dashboard, which also shows the included Beans.
- Rest Client extension: Build an 'http' file e.g. `api.http` with the REST calls (I've used this before and is obviously not platform-specific beyond recent VS Code versions).
- Extensions include a Java Test Runner that integrates into VS Code Test Explorer.
- Coverage Gutters Extension: Install 'jacoco' using `mvn` to get test coverage configured via Tasks e.g. `task.json`. See Coverage Gutters Extension for details. Coverage Gutters highlight code areas test-coverage by colorizing the 'gutter' area surrounding the code window.
- Microservices and Spring Framework: Use Spring Boot Dashboard (Extension) to view and configure components, including updating dependencies for security, features, and stability, with a single click-through.
- Extensions are available to enable Docker management and Database configuration and inspection.

## How To Eliminate Java Performance Warmup

Simon Ritter, Dep CTO Azul

- Java is compiled from source code to byte-codes to run on any platform (JVM - Write once, run anywhere).
- App startup tends to be slow, but increases over time due to JIT compiling of methods into runtime code - "Application Warmup".
- App Warmup applies _at every execution_. There is no 'memory' as to what was compiled last time.
- Goal: First run warmup might be the same, but subsequent warmups should ideally be (relatively) instantaneous.
- AOT: Ahead Of Time compilation. This causes full compilation specific to a platform. .NET 6+ enables this capability for C#. Bytecode intepretation and hotspot analysis is not executing during runtime while JIT compilation is happening.
- Graal Native Image: Compile 'native' executable to a platform everytime (like AOT)...with limitations.
- AOT is static: Code is compiled before application is run, so insights into what happens when the code runs. This can impact the ability to optimize the bytecode. Profiling helps but does not do the entire job.
- Speculative Optimization: Branch analysis evaluates methods, and compiles based on assumptions made during an initial analysis.
- Adding speculative optimizations at runtime is not compatible with AOT (at least, not without other major costs).
- JIT compilation: Reduces throughput during warmup.
- Azule Prime ReadyNow: Run app until 'warmed up', then profile the JIT data including any de-optimizations that occurred, and copy the compiled code. Restart the app, loading required classes and compiled methods, prior to hitting main entrypoint.
- ReadyNow optimization provides an n^3 level warm-up after a small zero-activity period, but then the warmup is largely completed, enhancing short-term full-performance.
- JIT Compilation has a cost: CPU-intensive, additional RAM, and tends to be a hazard for less-optimized (or lower horsepower) system environments e.g. little RAM.

Isn't using Azule just shifting the cost?

- Short: Yes.
- Long: Shift is to a more effecient place. JVM optimizations are carried to dedicated resources.
- More: Resources are shared and reused in a Cloud Native Compiled app/service.

CRUI - Coordinated Resume In Userspace:

- Linux-based service.
- Freezes a running App (sleep), creating a snapshot, and enables fast re-start.

CRaC - Coordinated Restore at Checkpoint:

- Makes App _aware_ it is being slept, checkpointed, and restored.
- Sockets, File IO, etc are not supported, so Checkpoint will be aborted if any of these are open.
- Within an API, utilize an Interface and implement `beforeCHeckpoint()` and `afterRestore()` methods to support sleep and wake operations. Registration via `register(resource)` tells the JVM the app is _aware_ of sleep and awake within (for example) SpringBoot.

Summary:

- No one solution fits every situation.
- AOT is good with small footprint services.
- ReadyNow provides JIT compilation 'memory'.
- Cloud Native Compiler decouples JIT workload from the Application and add cache.
- CRaC restarts App from a known point.
- New/upcoming; Project Leyden - Possibly a hybrid of some or all of the above approaches.

## Resources and Links

[JDConf 2024 Home Page](https://jdconf.com/)

[MSFT Java Developers Portal](https://learn.microsoft.com/en-us/java/?WT.mc_id=jdconf-56324-jemorg)

[MSFT Learn Java on Azure Training](https://learn.microsoft.com/en-us/training/paths/get-started-java-azure/)

## Footer

Return to [ContEd Index](./conted-index.html).

Return to [Root README](../README.html).
