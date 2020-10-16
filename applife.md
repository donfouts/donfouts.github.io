# Application lifecycle

![applife](https://s3-us-west-1.amazonaws.com/donfouts.io/applife.png)

## Exploration

The process of manual creation not just of dotnet code but all Azure assets by Dev/Ops staff - can be for Proof of Concepts or Research
happens in the [Research and Development](rnd1.md) and should be considered nonpermanent - clean up of RND assets can happen frequently.

## IaC Development

To eliminate the development of [HCL](https://www.terraform.io/docs/configuration/syntax.html) in funcational environments IaC development will happen in [Research and Development](rnd1.md). This could be new modules, module feature modifications all 4 funcational environments should be the same from an operational infrasctural viewpoint.
all development should be checked into the terraform application repo, and plaster templates updated / created. 

## Ash IaC Application

The steps of this phase are as follows:

- [new-ashapplication.ps1](plaster.md), the powershell script that uses *plaster* to create a new "application"
- modify the [HCL](https://www.terraform.io/docs/configuration/syntax.html) as requrired for the application
- check into a feature branch
- request a PR to master in azure devops 

## Application Iteration

Once an application is checking to the repo - changes to the [HCL](https://www.terraform.io/docs/configuration/syntax.html) can be performed. 
changes to an application's IaC should be made in a feature branch and assigned to the approprate Product backlog item and or tasks. 
examples of this work could be the change of a specific resource *upgrading your redis cache from standard to premium* or adding additional resources into your application's resource group - there was no Key Vault in catpictures-api's Resource group, the dev team needs a Key vault now - *this is a feature branch* change to the IaC repo. 

## Application Retirement

process not planned out yet, but Terraform will be used to clean up resources in azure and powershell will be used to release IDs and names from internal systems. 