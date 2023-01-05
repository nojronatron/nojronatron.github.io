# Chosing a Coding Language

This is a collection of thoughts about what to use where, when, with a little bit of why.

No presumptions about who or how will be addressed.

## Languages

There are of course many programming languages to choose from - Java, C#, javascript, Rust, Go, Python (the list goes on).

Deciding what to use when can be a matter of necessity, order or expectation, available frameworks to help get the job done, or target environment requirements.

Some examples:

- C# relies heavily on Microsoft's .NET framework (little 'f', but includes 'DotNET Framework' too). You can't just write compiled code like C# in a browser, so environmentally it is limited.
- javascript has multiple interpreter environments (browser, nodejs, and others) and thus is fairly portable, but the performance and built-in capability might not be good enough to use for an underlying service (like a cloud service).
- Java has a specified environment that is tight, performant, and available on many OS platforms. Anywhere you can install the JVM will be ready to execute a `.jar` file.
- Python (similar to Java in this regard) also has an underlying platform (Python 3.x or 2.x) that are designed for many OS environments. Anywhere Python n.x can be installed will happily run a python script (term used loosely, please don't at me) and integrate well with the OS environment it is running in.
- PowerShell is an interpreted environment that does not compile in the usual sense. Instead it relies on .NET framework to interoperate with the OS and environment. Recently, .NET 7 has the ability to execute on *nix OS platforms so multi-platform is possible whereas just a few years ago it was locked-in to Microsoft OSes only.

## So What Should I Use For Project X?

Ask yourself some questions about the project goals and requirements, as well as your own comfort level with a language, prior to making a decision.

Does the project *require* a specific language?

- Did the project definition simply call for Python because that's what the team or group or organization uses?
- Was performance a prime driver for selecting Java for this solution?
- Is this a 'Microsoft shop' or is the project strictly targeting Microsoft Windows (it happens) so a concrete, ready-to-perform solution is necessary such as C#?
- Are there specific frameworks that provide functionality that otherwise would need to be created at great cost, therefore utilize Python to leverage those frameworks for savings on development costs and quick ramp-up to expected functionality/capability?
- Is the project developing a webapp or a web-based service that requires a definite capability to provide user-centric, responsive user interface and back-end functionality, so javascript was selected along with frameworks like React and Express?

Is the team already familiar and capable with a specific language (or set of languages)?

In advanced programming scenarios, it is possible to leverage multiple programming languages to develop a solution.

Is the client/customer expecting the solution to be developed on a certain platform or with a specific language?

- Perhaps the customer needs contract-based work complete, that the customer will then take-over, so a language is specified as a project requirement.
- Client asks specifically for Python knowing that existing Python Frameworks (and perhaps their own) will speed development and provide AI or ML capability to their application.

## Personal Projects

First off, do what you want! There is not a hard limitation on what language to use. However, there may be times when using a specific language will really help you out (or make the project unreasonably difficult).

When developing a website:

- For a simple, quick start just deploy React and Express and develop with javascript-like code to complete the requirements.
- Consider using Vue, Redux, Angular, etc to meet specific needs.
- Explore other languages along the way to learn more stuff!
- Using C# and ASP.NET should not be ruled out, although there is a learning curve to overcome if not already familiar.
- Java with Spring MVC also should not be ruled out, however this also has a relatively high learning curve.

*Note*: There are lots of resources available for ASP.NET and SpringMVC, however the strongly-typed languages require a level of OOP understanding that javascript (and arguably Python) do not.

When developing a service:

- Is the service simply providing a REST endpoing? Simple enough to stick with Express and js-like code along with compatible frameworks to implement features like authN, authZ, caching, etc.
- Does the service communicate with other services on a local LAN/WiFi, or in the public internet/Cloud? Consider whether Python, Java, or C# would be a good starting point based on: Comfort level with the language; requirements of the OS platform (for example: RaspberryPi supports Python and there is a lot of support for this setup).

When developing a Console App:

- Why bother with heavy UI frameworks at all? For Linux and Windows a good solution could be Java.
- Windows-based console apps could leverage C# or Java.
- Considerations could include: If console app needs to talk to an internet-based API, certain frameworks might be better than others.
- If Console App is local-only, most likely the default libraries will be enough to get lots accomplished in either Java or C#.

When developing a Desktop App:

- C# can get pretty heavy using WinForms, however WPF/XAML is arguably quite a bit better and includes lots of web-UI design concepts that enable creating a fairly nice interface, with some complexity and learning curve involved.
- Java Spring framework provides for developing desktop UI for applications, but again requires overcoming a bit of a learning curve.

Mobile App Development:

- Developing for Mobile is a little different than Web or Desktop. First of all, there are many restrictions to watch out for and requirements to meet when developing a native app. For example accessing phone device capabilities like GPS, phone calls, and file finding are a bit different than they are for desktop. Non-native development is an option but has it's own challenges and limitations, so research absolute device and UI requirements before selecting native development (probably Java or Swift).
- Build a Web App that has a 'small screen' mode or is responsive to smaller-screen devices and can serve web, mobile, and desktop users.
- Consider ReactNative as a candiate framework to help develop for Android (not sure about iOS).
- Obviously for iOS, short of creating a responsive Web App, leverage Apple's development tools and toolchains.
- I learned Android development using Java. Aside from the shock of Android Studio's quirky bits and some pain experienced using the Emulator, Java and various Android frameworks can create a handy, responsive, performant phone app. Prepare to spend lots of time working through Google Play Store requirements.
- Xamarin (Dot NET) is a Microsoft-based mobile-development platform enabling cross-platform app dev, test, and deployment. If you are already familiar with DotNET and Visual Studio, this could be a good way to go.

## References

- Oracle [Java SE 19 Documentation](https://docs.oracle.com/en/java/javase/19/docs/api/index.html).
- Baeldung [Java Language Basics](https://www.baeldung.com/get-started-with-java-series) with links to Spring Frameworks examples and tutorials.
- Python.org [Documentation and Community](https://www.python.org/).
- Javascript everything at [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript).
- Apple Developer [Swift Documentation and Resources](https://developer.apple.com/swift/).
- PowerShell 7.x [Documentation and Learning materials](https://learn.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.3).
- Cross-platform, Open Source, Any-App [.NET](https://dotnet.microsoft.com/en-us/).
- Cross-platform, OSS, mobile app development [Xamarin](https://dotnet.microsoft.com/en-us/apps/xamarin).

## Footer

Back to [ContEd Index](./conted-index.html).

Back to [Root Readme](../README.html).
