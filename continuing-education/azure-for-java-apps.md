# Azure For Java Applications

Summary of Azure Friday videos covering Java development within Microsoft and using Microsoft technologies.

## Part 1

Guest: Bruno Borges, MSFT Principal PM Manager for Java.

*Note*: There is not currently a Part n+1 listed (crossing fingers).

### Using Java at MSFT

- 500k JVMs at MSFT as of 2021. Many of these are from Linked, Yammer, Minecraft, and other assets.
- Another 500k JVMs for other, non-customer projects.
- MSFT is a Java Shop!
- Azure Services and internal systems are JVMs.
- Android App (over 50 of them) are Java-based and in the GooglePlay store.
- BigData Services like Bing and MSN utilize JVMs for infrastructure.

Community engagement through:

- Eclipse Foundation
- OpenJDK
- Adoptium
- Spring
- GitHub
- VSCode

### OpenJDK Build

Utilize JDK 11 and 17 LTS.

Platforms includ: Linux, Alpine, macOS, and Windows, all 64 bit.

ContainerImages built on OpenJDK.

Installers developed in OpenJDKs:

- MSI, PKG, DEB, and RPM
- TAR.GZ and ZIP
- Homebrew, WinGet, and SDKMan

MSFT has it's own Build of OpenJDK based on OpenJDK and Adoptium.

- Shipped MSFT Build of OpenJDK Java 17.
- Minecraft Java Edition is built on this.

### Modern Java

Internal partnerts and developers aligned using modern Java (17 LTS).

Azure Platform Services roll-out to Java 17 LTS:

- AppService
- Functions
- Spring Cloud

MSFT has published migration guides on Java 8 -> 11 and 17.

By moving to modern Java (17 LTS):

- Cleaner code.
- Smaller packages.
- Container awareness (kubernetes et al).
- Deduped Strings (shrinks XML, JSON apps size).
- Improved startup speed.
- Memory management improvements e.g. Garbage Collectors for large and small workloads.

### MSFT Tools for Java

Playwright: End to end testing for modern web apps.

GitHub Copilot: Coding suggestions provider.

Windows Subsystem for Linux.

VS Code: see aka.ms/java-vscode.

GitHub Actions: Automate workflows.

Maven and Gradle (and Ant): MSFT provides documentation for these.

### Building

IntelliJ, Eclipse, and VS Code: All include Azure Integration.

Maven and Gradle support.

GitHub, Jenkins, and Terraform automation for development workflows support.

### Build or Migrate Java Apps?

Common Azure tools for building and migrating Java apps (Java SE):

- IaaS: Virtual Machines and VMWare Tanzu.
- Containers: Azure Kubernetes Service and RedHat OpenShift.
- Platform as a Service (PaaS): JBoss EAP, Tomcat, Java SE, and Azure Spring Cloud.

*Note*: Some support for the above listed services is not there for Java EE flavors.

## Resources

- Azure Friday Episode: [Azure Is The Home For Your Java Applications Part 1](https://learn.microsoft.com/en-us/shows/azure-friday/azure-is-the-home-for-your-java-applications-part-1).
- Microsoft website [Java on Azure](https://azure.microsoft.com/en-us/resources/developers/java).
- MSFT Blog [Azure is the home for your enterprise Java apps](https://azure.microsoft.com/en-us/blog/azure-is-the-home-for-your-enterprise-java-applications).
- [MSFT Build of OpenJDK](https://www.microsoft.com/openjdk) home page.

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
