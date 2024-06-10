# Terraform Associate Study Notes

## Understand Infastucture as Code Concepts

### What is IAC
IAC allows users to build infastructure using text based files instead of using GUIs or CLIs. 

### Advantages of IAC Patterns
There are __BlAh____ benefits to using IAC:

1. Tack Infastructure: All changes are based off of the TF state file allowing you to view and track all changes in one central location.

2. Automnation: Terraform is smart and deploys your changes in the order that product needs them in. In AWS for example even if you created the subnet before the VPC, terraform knows to create the vpc first before it can deploy the subnet. 

3. Standardize Configurations: You can create or use publically available modules to keep your IAC standardized and easily repeatable. 

4. Collaborate: Using git or terraform cloud you are able to add version control to your code allowing you to easily collabarte with others on writing IAC.


## Understand the Purpose of Terraform vs Other IAC

### Cloud and provider agnostic

### The Benefits of State

