# Components and React

## What Is A Component

Components are individual, functional bundles of code that contain methods, properties, and perhaps events.  

They specific a specific set of functionality or API that they export, and their prime directive is to simply perform on those APIs very well and that is it.

### Component Views

Object-oriented: Component is viewed as a set of well coordinated classes. Communication between classes are defined as an interface.  

Conventional: Components is viewed as a module or functional library with an interface allowing data to be passed between it and its dependants. All functionality and processing are fully encapsulated in the module.  

Process-related: Components are built on top of existing components, maintained as a Library.  

#### Process Related Examples

UI Components: Contain the controls and functions that can be used within other functions to manage aspects of the user interface.  
Resource Intensive: Components activated using a JIT approach.  
Invisible/Enterprise: Internet WebApps and other applications like EJB, DotNET, CORBA, etc.  

### Component Characteristics

Resuable: Some components are designed for very specific tasks, other are designed to be used in other scenarios. Either way, whenever a component can be used, it should.  

Replaceable: Substitution should be allowed and possible (with minimal or no code refactoring).  

Not Context Specific: Designed to operate in different environments.  

Extensible: New behavior can be added by building-on to the existing Component.  

Encapsulated: Details of "under the hood" processing and etc are hidden from the caller, as they are not necessary to meet the purpose of the Component nor the goals of the App that is using it.  

Independent: Components should rely on as few other Components or Libraries as possible.  

### Component Design Principles

Guidelines for Component Design and Creation:  

- Decompose software into reusable units.  
- Interfaces are unique to the component and details of operation are hidden from the caller.  
- Extensions to the component can be achieved without having to refactor the components code.  
- Do not depend on other 'concrete' components, use abstractions instead.  
- The interface defines the communication methods and properties with the component and other code or components.  
- Protocol-specific interactions can be used e.g. Method invokation, async calls, etc.  
- Specialized interfaces on Server-side components that handle a majority of clients, and the interface specifies the interactions.  
- Component extention is possible without blocking access to its own component functionality and interfaces e.g. "plug-in architecture".  

### Component Design Guidelines

- Use syntax and terminology that is in-scope for the problem domain the Component is used within or solves.  
- Encapsulate business-processes independently and without requiring other external entities.  
- Interprets other entities as new components.  
- Component naming scheme follows implementation meaning(s).  
- Follows concepts of derived classes and inheritance.  
- Other components are seen not only as components but interfaces.  

### How Does This Apply To React

React is a component-based Library *[itnext.io article (see link below)]*.  

## About Props

They:

- Are *objects*.  
- Act as parameters that can be passed into React components.  
- Are defined like `<MyComponent myAttrOne={foo} />` or `<AnotherComponent text={"Hello world!"} />`  
- Can have arguments passed to them like `let MyComponent = (props) => { return <p>Hello World!!!</p>; };`  
- Cannot have their value changed they are immutable.  

## Q and A

What is a Component? *Individual, functional bundles of code that contain methods, properties, and perhaps events*. The functionality is well-defined, and fully encapsulated into the software object. Components are tightly specified and guaranteed to provide the interface and functionality as it is described.  

What are the characteristics of a component? *Reusability, Replacability, Context-insensitive, Extensible, Encapsulated, and Independent*.  

What are the advantages of using component-based architecture?  

- Reusability.  
- Improved reliability given reusability.  
- Reduced development costs: Reuse components to build other components or Apps.  
- Simplified deployment: Only a small amount of work is necessary to deploy the component and it will operate as expected.  
- Reliability: Less code and very specific code is simpler to build, maintain, and debug.  
- System Maintenance and Evolution: Plug-in architecture enables simple updates and implementation w/o unbalancing the system.  
- Independance: Parallel development of many components can be done, and interactions can be designed based on the interface (contracts) of each component.  

What is "props" short for? *Props are how components pass data between each other. Props is a React keyword that stands for properties*.  

How are props used in React? *Props are used to pass data within a React application, from one component to another*.  

What is the flow of props? *Prop Data flows one-way, from Parent to Child*.  

## References

Component Based Architecture [webpage](https://www.tutorialspoint.com/software_architecture_design/component_based_architecture.htm)  
What Is Props and How To Use In React [webpage](https://itnext.io/what-is-props-and-how-to-use-it-in-react-da307f500da0)  

## Footer

[Back to readme.md](../README.md)  
