# Terraform Associate Study Notes

## Understand Infastucture as Code Concepts

### What is IAC
Infastructure as Code allows users to build infastructure using text based files instead of using GUIs or CLIs. These files are made up of Terraform code that is designed to be human readable, while also be flexable enough to work across many providers.

### Advantages of IAC Patterns
There are 4 main benefits to using IAC:

1. Tack Infastructure: All changes are based off of the TF state file allowing you to view and track all changes in one central location.

2. Automnation: Terraform is smart and deploys your changes in the order that product needs them in. In AWS for example even if you created the subnet before the VPC, terraform knows to create the vpc first before it can deploy the subnet. 

3. Standardize Configurations: You can create or use publically available modules to keep your IAC standardized and easily repeatable. 

4. Collaborate: Using git or terraform cloud you are able to add version control to your code allowing you to easily collabarte with others on writing IAC.


## Understand the Purpose of Terraform vs Other IAC

### Cloud and provider agnostic
Being cloud agnostic helps to make Terraform a more universal tool than other IAC products out there that are typically restricted to single provider such as cloudformations for aws. While requiring more expertise Terraform can deploy into multi providers all at once. This can increase fault tolerence incase one provider was unable to deploy the requested infastructure.

### The Benefits of State
The Terraform state file plays the cruical role of maintaining Terraform's knowledge of what infastructure is currently deployed. The state file is located based on the terraform backend definition. It is recommended that this is not stored locally but rather kept in a shared, secured location. This is beneficial so that mutiple people can edit the file and so that it does not get deleted. Another important part of the state file is understanding the crucial role of the lock that is in placed on the file to prevent multiple edits to the state file at once.


## Terraform Basics

### Installing and Versioning Providers
A provider in Terraform is the magic that help makes it all run. The provider converts your Terraform code into the necessary api structure needed to build out your desired infastructure. There are three tiers to providers in Terraform:

1. Offical: Published by the company that owns the technology.
2. Verified: Is actively mainted and is up-to-date.
3. Community: A community member has built this, no-guarantee of function.

Provider version can also be specified so that a minium version of the provider can be verified to be in use. In a terraform block use the <required_providers> block to the call the desired version. Adding >= before the version will set it to the minimum required, where default or = will specify the exact requirment. 

### Plugin Based Architecture
| Terraform Core | Terraform Plugins |
|---|---|
| Terraform core is responsible for interpreting the IAC, finding the difference between the desired state and current state, and communicating the plan to the plugins over RPC | Terraform plugins are responsible for making the API calls, authentication with the provider, define managed resources and functions |

### Terraform with Multiple Providers
One of the excellent features of Terraform is that it can support multiple providers all in one piece of code. To s

### Terraform Providers in Depth