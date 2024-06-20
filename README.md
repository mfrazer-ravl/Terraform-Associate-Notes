# Terraform Associate Study Notes

## Understand Infrastructure as Code Concepts

### What is IAC
Infrastructure as Code allows users to build infrastructure using text based files instead of using GUIs or CLIs. These files are made up of Terraform code that is designed to be human readable, while also be flexible enough to work across many providers.

### Advantages of IAC Patterns
There are 4 main benefits to using IAC:

1. Tack Infrastructure: All changes are based off of the TF state file allowing you to view and track all changes in one central location.

2. Automation: Terraform is smart and deploys your changes in the order that product needs them in. In AWS for example even if you created the subnet before the VPC, terraform knows to create the vpc first before it can deploy the subnet. 

3. Standardize Configurations: You can create or use publically available modules to keep your IAC standardized and easily repeatable. 

4. Collaborate: Using git or terraform cloud you are able to add version control to your code allowing you to easily collaborate with others on writing IAC.


## Understand the Purpose of Terraform vs Other IAC

### Cloud and provider agnostic
Being cloud agnostic helps to make Terraform a more universal tool than other IAC products out there that are typically restricted to single provider such as cloudformations for aws. While requiring more expertise Terraform can deploy into multi providers all at once. This can increase fault tolerence incase one provider was unable to deploy the requested infastructure.

### The Benefits of State
The Terraform state file plays the cruical role of maintaining Terraform's knowledge of what infastructure is currently deployed. The state file is located based on the terraform backend definition. It is recommended that this is not stored locally but rather kept in a shared, secured location. This is beneficial so that mutiple people can edit the file and so that it does not get deleted. Another important part of the state file is understanding the crucial role of the lock that is in placed on the file to prevent multiple edits to the state file at once.


## Terraform Basics

### Installing and Versioning Providers
A provider in Terraform is the magic that help makes it all run. The provider converts your Terraform code into the necessary api structure needed to build out your desired infastructure. There are three tiers to providers in Terraform:

1. Official: Published by the company that owns the technology.
2. Verified: Is actively maintained and is up-to-date.
3. Community: A community member has built this, no-guarantee of function.

Provider version can also be specified so that a minimum version of the provider can be verified to be in use. In a terraform block use the <required_providers> block to the call the desired version. Adding >= before the version will set it to the minimum required, where default or = will specify the exact requirement. 

### Plugin Based Architecture
| Terraform Core | Terraform Plugins |
|---|---|
| Terraform core is responsible for interpreting the IAC, finding the difference between the desired state and current state, and communicating the plan to the plugins over RPC | Terraform plugins are responsible for making the API calls, authentication with the provider, define managed resources and functions |

### Terraform with Multiple Providers
One of the excellent features of Terraform is that it can support multiple providers in one deployment. By specifying the provider in each resource block you are able to launch into multiple public clouds for example at once. If you need to lauch into multiple regions at once for aws, you can use the alias parameter e.g. aws.west or aws.east. 


## Terraform Outside the Core Workflow

### Terraform Import
The terraform import command lets you bring in resources that were not deployed using terraform into your terraform.tfstate file so that it can then be tracked and managed. 

### Terraform State
The terraform state command let's you make changes to the terraform state file directly.

### Verbose Logging
Terraform has detailed logs that are enabled by setting TF_LOG one of 5 levels (Trace -> Error).


## Terraform Modules

### Module Source Options
There are roughly three main sources for modules.

1. Make your own: You can right your own modules that you can either source locally or upload them to an online repo.

2. Terraform Registry: This is Terraform's Public Registry where providers can upload pre-built modules to take care of commonly needed use cases. 

3. Private Registry: Terraform cloud let's you create a private Registry for your organization allowing you to pull from your own internally created modules.

### Module Input and Output
All input variables are declared in variable blocks. You are able to add the following arguments to the block:
|  Optional Arguments | Effect  |
|---|---|
| default  | The default argument let's you assign a stock value that terraform will assign to the variable if you don't |
| type  | The type argument constrains what the variable block will accept. This can be a mix of type keywords (string, number, bool) and type constructors (list, set, map...) |
| description  |  The description allows you to describe what the purpose of the variable is |
| sensitive  | When you assign sensitive to true terraform will sensor the variable in the plan and apply output. The value will still appear however in the statefile.  |
| nullable  | When set to true nullable will allow terraform to set this variable to nul. When false if null is assigned it will attempt to use the default value before throwing an error. | 

### Variable Scope Within Modules
Modules are used as containers to run multiple resource commands in a systematic/automated way.

A module is called by using the following format:

module "name" {
  source = "foo" #(required)
  version = "bar" #(version is recommended for registry modules)
}

This is considered a "child module", in this case called name.

Modules are typically going to have you describe other variables as well in the module declaration.

### Module Version
Specifying a version is important when sourcing a module from a public or private registry so that you are able to meet the known constraints.


## Terraform Core Workflow

### Write -> Plan -> Create

1. Write: Author infrastructure as code.

	Individual
	Writes terraform code in the editor of their choice, storing their code either locally or using a remote version controlled repository.

	Team
	When writing with a team it is vital to be uploading code to a shared version controlled repository. On top of that individual team members will make their changes to a unique branch that can be merged to the main branch later. 

2. Plan: Preview changes before applying.

	Individual
	Using terraform plan or apply will highlight the changes that you wrote previously.

	Team
	When working with a team the terraform plan command becomes even more important and lets the team take a collaborative approach when reviewing changes.

3. Apply: Provision reproducible infrastructure.



### Terraform Init

### Terraform Validate

### Terraform Apply

### Terraform Destroy

### Terraform FMT



