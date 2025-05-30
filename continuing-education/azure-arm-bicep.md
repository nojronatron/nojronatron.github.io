# Azure ARM and Bicep

ARM Templates are fairly complex, and Bicep helps to define templates for you (and with you).

## Table of Contents

- [About Bicep](#about-bicep)
- [Bicep Basics](#bicep-basics)
- [Syntax Structure](#syntax-structure)
- [Keywords](#keywords)
- [Parameters and Variables](#parameters-and-variables)
- [Expressions](#expressions)
- [Functions](#functions)
- [Combining Strings](#combining-strings)
- [Conditionals, Ternary Operator](#conditionals-ternary-operator)
- [Generate an ARM Template](#generate-an-arm-template)
- [Compose Bicep Modules](#compose-bicep-modules)
- [Deployment Using Bicep](#deployment-using-bicep)
- [Set Scope to Bicep Script](#set-scope-to-bicep-script)
- [Things To Be Aware Of](#things-to-be-aware-of)
- [Bicep Commands (Not Comprehensive)](#bicep-commands-not-comprehensive)
- [Learning Q and A](#learning-q-and-a)
- [Resources](#resources)

## About Bicep

Targets Azure (not other cloud platforms).

Declaritive.

Uses Domain Specific Language (DSL).

Describe the shape of your Azure deployment as a "final state" and Bicep takes care of the hard work.

Bicep can be interactive to notify the Admin that issues might result using a current Bicep file declaration.

Bicep describes Azure infrastructure without having to sort through lots of JSON file metadata.

Scott Hanselman: Bicep transpiles down to Arm Template(s).

Bicep is the layer above ARM whereas Terraform and other engines are the defining and execution components.

Automated deployments using Bicep are available through GitHub Actions, Azure DevOps, or through scripts.

Bicep scales better than ARM templates.

Modular:

- Reuseable components
- Compose multiple files into an Azure infrastructure definition

## Bicep Basics

Bicep language files end with `.bicep`

Bicep support:

- VS Code Extension "Bicep" has a Bicep language service.
- Visual Studio: 1st-class support.

Azure API versions have Swagger endpoints that Bicep then knows how to use (Azure Typed resources).

Bicep knows how to fetch Keys for deployment requirements such as Azure Key Vault.

Azure CLI `az` is used:

- Install and update Bicep
- Create Azure Resources based on a bicep file
- Remove Azure Resources based on bicep definitions

Basic Usage:

1. Define how Azure resources should be configured in a Bicep Template (file)
2. Submit the template to Azure Resource Manager
3. Watch the resources get deployed to Azure on your behalf

## Syntax Structure

Similar to a coding language, syntax includes:

- Parameters
- Properties
- Keywords
- API Levels (lime imports or usings)
- Output (like JS Module Exports): Allows passing values to other bicep modules via Parameters
- String interpolation: var storageName = `'${prefix}20210927storage'`
- Functions: Array functions, date functions, file functions, etc
- `@`validators: MinLength(int), etc

Some Keywords:

- var: User-defined variables
- var: Supports creating arrays just like JS but no commas or semi-colon needed
- resource
- [for (item,index) in {instance}]: Loop over item in instance and include an index with each item
- if () = {}: Assigns a conditional to the following definition object {}

```bicep
param symbolicName type

@label()
param symbolicName type

keyword symbolicName API version = {
  property: propertyName | symbolicName
  property: {
    childProp: value
    childProp: value
  }
}
```

Symbolic Names are references for Bicep only, and do not appear in Azure.

Resource Names are **actual Azure Resources** and will appear in Azure upon deployment.

## Keywords

`resource`

- Add a variable name to it
- Select an Azure Resource type (there are hundreds)
- Also select an API version like `@2022-05-01`
- Assign required properties within the resource braces `{ ... }`

```bicep
resource stg 'Microsoft.Storage/storageAccounts@2022-05-01' = {
  name: 'string-interpolated-definition'
  location: 'define_with_a_param_if_able'
  kind: 'StorageV2'
  sku: {
    // name of sku as selectable in Azure
  }
  properties: {
    // encryption, access permissions, etc
  }
}
```

`param`

- A custom parameter
- Create and assign at the top of the Bicep file
- Can be used as a global variable

`output`

- Send Bicep output to a location
- Is evaluated last, after deployment
- Output **cannot be known** prior to deployment so an abstraction is used

Example of returning the FQDN of a public IP Address to the deployment pipeline:

```bicep
output ipFqdn string = publicIPAddress.properties.dnsSettings.fqdn
```

**Note**: Do not create output values for secrets.

`module`

- Template can include a reference to a module file
- The module reference looks like a resource definition but points to a filename instead

Example referencing 'mymodule' bicep file, assigning a symbolic name, providing a path to the file, naming the reference, and a list of params to use in the module:

```bicep
module myModule 'modules/mymodule.bicep' = {
  name: 'MyModule'
  params: {
    location: location
  }
}
```

Output from one MOdule  can be a parameter for another module!

- Chains bicep files together without losing modularity

`existing`

- Related to [Azure Key Vault](#azure-key-vault)
- Tells Bicep to Read an existing key (and not redeploy it)

## Parameters and Variables

Provide information to template during each deployment.

Use Parameters for:

- Things that change between deployments
- Resource names that need to be unique
- Location targets for resources
- Price-affecting settings
- Credentials and data needed to access other systems that aren't defined within a template
- Keep them simple but descriptive so it is easy to understand their purpose
- Referencing throughout a template
- Making a Parameter options by setting a default value

Example of a required parameter and an optional parameter with a default value:

```bicep
param appServiceAppName string
param appServiceWebName string = "default name to assign"
```

Tips:

- Avoid using too many parameters
- It's okay to change a template when necessary, instead of over-generalizing the template
- Variables assume a type when they are assigned ```var myName = "hello"``` knows the assigned value is a string
- Variables **must be assigned a value** upon declaration

Types include string, int, bool, object, and array

### Parameter Files

Specify parameter values together in a set.

- Extension `.bicepparam`
- JSON formatted
- `$schema` tells bicep this is a parameters file
- Ensure only used parameters are added to this file

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "parameterAlpha": {
      "value": 3
    },
    "parameterBravo": {
      "value": {
        "name": "P1v2",
        "tier": "PremiumV4"
      }
    },
    "parameterArray": {
      "value": [
        {
          "locationName": "westus2"
        },
        {
          "locationName": "centralus"
        },
        {
          "locationName": "westeurope"
        }
      ]
    },
    "sqlServerAdministratorPassword": {
      "reference": {
        "keyVault": {
          "id": "/subscriptions/{id}/resourceGroups/PlatformResources/providers/Microsoft.KeyVault/vaults/{vaultName}"
        },
        "secretName": "mySuperSafeAdminPassword"
      }
    }
  }
}
```

Specify the parameters file when defining a new resource group deployment:

```powershel
New-AzResourceGroupDeployment -Name main -TemplateFile main.bicep -TemplateParameterFile main.parameters.json
```

More about [Azure Key Vault](#azure-key-vault) later in this document

### Securing Parameters

Use the `@secure()` function:

- Precede the parameter to secure with this attribute
- Applies to string and object parameters
- Parameter is not made available in the deployment logs
- Interactive deployment requires entering secured parameters in-line at the terminal and the values will not display on-screen
- Restricts values to complex, 8-character or greater values
- Enforces complex key names i.e. "admin" should not work

**Avoid** creating outputs for parameters that have the `@secure()` attribute set.

Read about [Azure Key Vault](#azure-key-vault) later in this document

### Overriding Parameters

1. Command-line Parameters override Parameter Files
2. Parameter Files override Default Values

One way to think of this: Last one wins.

### Decorators
  
Attach constraints and metadata to a parameter:

- Protects secret data
- Limit parameter values
- Tied to the Parameter that follows
- Ensure parameters always contain the values you expect

Constraining Parameter Values

Too many SKUs to list all so use a parameter with an `@allow` constraint:

```bicep
@allowed([ 
  'nonprod'   
  'prod' 
])
param environmentType string
```

The allowed list is an [array](#arrays), of strings in this case.

Template will not deploy unless one of the two allowed values are set to the 'environmentType' parameter, because there is no default value.

[Min, Max, MinLength, MaxLength](#parameter-restrictions)

Parmaeter Descriptions:

- Document a parameter
- Precede the parameter with `@description(string)`
- Stick with critical info
- Keep them helpful

### Objects

Parameters can be defined to contain objects.

Object are used to set Tags.

Example:

```bicep
param resourceTags object = {
  EnvironmentName: 'Test'
  CostCenter: '101011'
  Team: 'Adv Prod'
}
```

Then, apply a tag:

```bicep
resource appServiceApp 'Microsoft.Web/sites@' = {
  name: appServiceAppname
  location: location
  tags: resourceTags
  ...
}
```

### Arrays

A collection of values:

- Value types cannot be defined (they are just Objects)
- Each item in the collection should be treated as its own instance
- No commas between instance items
- Be certain to use the type that the target consumer expects

```bicep
param myDbAccountLocations array = [
  {
    locationName: 'westeurope'
  }
  {
    locationName: 'westus'
  }
]
```

List of allowed string values:

```bicep
@allowed([
  'P1v3'
  'P2v3'
  'P3v3'
])
param ...
```

### Parameter Restrictions

Methods that apply limitations or constraints to the following parameter:

- Precede with a splat `@` character
- minLength(T value), maxLength(T value)
- minValue(T value), maxValue(T value): Can be used to define a range

```bicep
@minValue(1)
@maxValue(10)
param instanceCount int
```

## Expressions

When:

- Use expressions when you don't want to specify a parameter nor hard-code values
- Business rules enforce a common deployment parameter like "location"
- Provide a default value to a Parameter based on a resource like `resourceGroup().location`

How:

```bicep
param location string = resourceGroup().location
```

Access the location expression assignment when defining a resource:

```bicep
resource appServiceApp 'Microsoft.Web/sites@2024-04-01' = {
  name: appServiceAppName
  location: location
  properties: {
    serverFarmid: appServicePlan.id
    httpsOnly: true
  }
}
```

This assigns the Resource Group's location to the 'location' parameter.

**Keep In Mind**: Some Azure Resources cannot be deployed to certain locations.

## Functions

Use `uniqueString()`:

- To ensure unique naming
- Ensures constrained length requirements are met
- Set to a parameter
- Provide a seed value from which the unique value is calculated
- A good seed value ensures same-name for same-deployments, as well as unique new-deployment values

```bicep
param storageAccountName string = uniqueString(resourceGroup().id)
```

storageAccountName might look something like `/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/MyResourceGroup`

## Combining Strings

```bicep
param storageAccountName string = toylaunch${uniqueString(resourceGroup().id)}
```

## Conditionals, Ternary Operator

Just like C#, JavaScript, etc.

Example:

```bicep
var storageAccountSkuName = (environmentType == 'prod') ? 'Standard_GRS' : 'Standard_LRS'
```

Best Practice: Use variables instead of magic values within ternary/conditional expressions.

## Generate an ARM Template

```powershell
az bicep build -f .\file.bicep
```

Outputs an ARM Template to the same directory, based on input file 'file.bicep'

## Compose Bicep Modules

`module`

- Give it a name
- Then select other bicep files to piece-together multi-file bicep definitions
- Supply params in the module definition as a JSON-like object

Scoping is by file, avoiding variable name collisions.

**Note**: JSON-like means it looks like JSON but doesn't use commas to separate object properties.

## Deployment Using Bicep

1. Add a Deploy folder to your project
1. Add bicep files that describe the deployment
1. Execute Azure Powershell commands
1. Finally, deploy code to the Azure Resources

```powershell
New-AzResourceGroupDeployment -Name main -TemplateFile main.bicep -environmentType nonprod
```

## Set Scope to Bicep Script

Scope can be set to:

- Resource Group: 'resourceGroup'
- Subscription: 'subscription'
- Management Group: 'managementGroup'

Keyword `targetScope`

Assignment via equals sign:

- `targetScope = 'subscription'`
- Applies to the entire script

Assignment within a module or resource declaration:

- `scope: resourceGroup(rg-name)`
- Applies only to the current module or resource context
- Can be used to override scope within a bicep file that has `targetScope` already set

## Things To Be Aware Of

Az outputs when processing Bicep scripts can be helpful, but sometimes counter-intuitive:

- Errors processing a Bicep file usually point to the cause
- Successful deployments can return red text indicating something is unavailable
- Deployments that fail sometimes present an obscure red text message without details

Use the VS Code Bicep Extension:

- In-line Completions (activate with spacebar or start typing contextually relevant keywords)
- Code suggestions
- Snippets

Notes:

- These tend to be somewhat old/dated so use with caution
- Not all properties are available, such as VM image publisher, offer, sku, and several others

## Azure Key Vault

Designed to store and provide access to secrets:

- Integrate with Bicep templates
- Use a parameters files that references a Key Vault secret
- Value is never explosed, and is only representative as an ID
- Azure Resource Manager contacts Azure Key Vault to securely acquire the value(s)

Example:

```json
{
  ...
  "parameters": {
    "sqlAdminPassword": {
      "reference": {
        "keyVault": {
          "id": "/subscriptions/{sub_id}/resourceGroups/PlatformResources/providers/Microsoft.KeyVault/vaults/toysecrets"
        },
        "secretName": "myAdminPassword"
      }
    }
  }
}
```

**Note**: Azure Key Vault costs money. The more keys you request, the **less it costs**.

### Leverage Key Vault with Modules

Utilize `Microsoft.KeyVault/vaults` API to get access to an existing Azure Key Vault.

```bicep
resource keyVault 'Microsoft.KeyVault/vaults@2023-07-01' existing = {
  name: keyVaultName
}
```

The `existing` keyword tells Bicep to READ the key and not redeploy it.

```bicep
module applicationModule 'application.bicep' = {
  name: 'application-module'
  params: {
    apiKey: keyVault.getSecret("ApiKey')
  }
}
```

## Bicep Commands (Not Comprehensive)

- build: `bicep build main.bicep`

## Creating Interactive Automation Using PowerShell

Gather the Azure Key Vault name and login information so the correct keys can be securely used by Bicep:

```powershell
$keyVaultName = 'YOUR-KEY-VAULT-NAME'
$login = Read-Host "Enter the login name" -AsSecureString
$password = Read-Host "Enter the password" -AsSecureString

New-AzKeyVault -VaultName $keyVaultName -Location eastus -EnabledForTemplateDeployment
Set-AzKeyVaultSecret -VaultName $keyVaultName -Name 'sqlServerAdministratorLogin' -SecretValue $login
Set-AzKeyVaultSecret -VaultName $keyVaultName -Name 'sqlServerAdministratorPassword' -SecretValue $password
```

Get the RId of the vault so secrets can be used in a Bicep Parameters file:

```powershell
(Get-AzKeyVault -Name $keyVaultName).ResourceId
```

Add the return value to `parameters.main.json`:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "appServicePlanSku": {
      "value": {
        "name": "F1",
        "tier": "Free"
      }
    },
    "sqlDatabaseSku": {
      "value": {
        "name": "Standard",
        "tier": "Standard"
      }
    },
    "sqlServerAdministratorLogin": {
      "reference": {
        "keyVault": {
          "id": "YOUR-KEY-VAULT-RESOURCE-ID"
        },
        "secretName": "sqlServerAdministratorLogin"
      }
    },
    "sqlServerAdministratorPassword": {
      "reference": {
        "keyVault": {
          "id": "YOUR-KEY-VAULT-RESOURCE-ID"
        },
        "secretName": "sqlServerAdministratorPassword"
      }
    }
  }
}
```

Deploy the template using Azure Vault and a Parameters file:

```powershell
New-AzResourceGroupDeployment -Name main -TemplateFile main.bicep -TemplateParameterFile main.parameters.dev.json
```

## Learning Q and A

What is Infrastructure as Code?

- Declarative code that describes the infrastructure necessary for a cloud deployment

How can IaC help automate resource provisioning?

- Reproducible deployments to the cloud
- Rapid deployment
- Scalable
- Better manage cloud resources and configurations
- Imperative tools like Azure CLI commands are not easily scalable to increasingly large or complex deployments
- Imperative tools commands can become deprecated, requiring script review and refactoring
- Declarative tools describe an end-result, abstracting the complexities of underlying tools (and Azure) that make the deployment happen

What is Bicep and how does it work?

- Deterministic, declarative
- Bicep describes what Azure Resource Manager service acts upon to make templates and perform deployment steps
- Bicep will generate ARM Templates (so you don't have to)
- Modular, repeatable, orchestratable, and extensible
- Bicep is transpiled into ARM Template JSON when submitted, or manually via the Bicep tooling

When should Bicep be used instead of other options?

- Bicep is subset of ARM, as are ARM Templates (JSON), enabling easy transition from JSON
- Simplified language (DSL) compared to JSON
- Convenient: Uses same tooling as ARM Templates
- Azure-native
- No state management is necessary
- Bicep might **not** be a good fit: Multi-cloud systems, and scenarios where other tools are already deeply integrated into the Cloud configuration and deployment system, or target platform is not Azure

What is the difference between Control Plane and Data Plane?

- In Azure Operations, Control Plane is used to manage resources within a Subscription and Data Plane is used to access features of a resource
- Control Plane: Create VMs
- Data Plane: Connect to VMs using RDP
- Control Plane API: management.azure.com/subscriptions
- Data Plane API: {location}
- Control Plane and Data Plane permissions are not always mutually applicable (e.g. User can RDP to a VM but cannot manage the VM via the Control Plane)

What is a Resource Definition?

- bicep code
- ```resource {name} '{resource.Type/API@version}' = { ... }```
- Defines an Azure Resource in a code-like, assignment style
- Bracketed body contains required and optional properties needed to define the Resource configuration

How do Parameters make templates reusable?

- They add flexibility
- Deploy multiple resources using the same Bicep file with different inputs to parameters
- Avoids using fixed Resource names, replaced by parameters instead
- Enable deploying resoruces to different locations without changing Bicep file(s)
- Go hand-in-hand with Variables to increase flexibility
- Variables are defined and assigned within the template

Describe variables and expressions, and how they make writing and deploying templates easier?

- Variables allow assinging Template-wide, commonly used values, avoiding magic numbers
- Expressions allow simple generation of unique, constraint-following names based on a seed (like a ResourceGroup ID)
- Simplifies writing templates and minimizing deciding on naming schemes and name variations
- Allows deploying different skus, storage kinds, or to varying location based on a set of allowed parameter values

Why would you want to structure Bicep files into Modules?

- Group related resources
- Chain bicep operations and parameter values
- Create separate files with clear purpose for ...modularity
- Define sets of resources that are directly related e.g. AzureSQL servers and their Database instances

What is the purpose of using Outputs in Bicep files?

- Send data back to whatever started the deployment, including another bicep file (module)
- Pushes data to a deployment pipeline for use by other processes
- An expression is used to name a resource, and the calling process needs the generated name for a future action
- Get the resulting IP address endpoint of a newly created resource like VM's IP address for SSH/remote access

How can parameter values be limited?

- Length
- Value
- Secure storage

What are the 3 ways parameters can be supplied to a bicep template?

1. Param keyword assigns a value provided at the terminal command line.
2. Parameter values set from a Parameters json file.
3. Leverage Azure Key Vault to get an existing secured key.

What is best practice for working with secure parameters?

- Use Azure Vault using Module syntax with or without a parameters json file.
- Azure Resource Manager securely communicates Key Vault values to Azure when needed.
- Use the `@secure()` functiont to ensure the value is not revealed at the terminal, logs, or elsewhere in the deployment process.

## Resources

- [Bicep Parameters File](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/parameter-files?tabs=JSON)
- [Blog post about creating a web app with unique default host name](https://techcommunity.microsoft.com/blog/appsonazureblog/secure-unique-default-hostnames-ga-on-app-service-web-apps-and-public-preview-on/4303571)
- [Best Practices](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/best-practices)
- Microsoft Learn Path (3hrs) [Fundamentals of Bicep](https://learn.microsoft.com/en-us/training/paths/fundamentals-bicep/)
- Microsoft Learn Path (3hrs+) [Intermediate Bicep](https://learn.microsoft.com/en-us/training/paths/intermediate-bicep/)
- [Bicep Documentation Index](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/)
- [Azure App Service Deploy Best Practices](https://learn.microsoft.com/en-us/azure/app-service/deploy-best-practices)
