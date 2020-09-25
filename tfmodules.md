# Modulated Terraform for multi-application deployment (non-code)

This is my approach to be able to configure and deploy various azure services that are grouped by "application" - and using a modulated HCL makes sence.

my [plaster](plaster.md) script spits out a folder that is the name of the application, and all of the modules in their own sub-folders.

![folders](https://stdsoinventory0001.blob.core.windows.net/mdwikiimages/plasterresults.png) 

## /main.tf

main.tf in the root of the application is the root main.tf - and has all the modules listed inside that file, some commented out.  
this is where we have the provider and backend:

    provider "azurerm" {
    alias = "westus"
    version = "=2.5.0"
    features {}
    }

    terraform {
    backend "azurerm" {
        access_key           = "yourkeyhere"
        storage_account_name = "yourstorageaccount"
        container_name       = "applications"
        key                  = "exerciserewards.terraform.tfstate"
    }
    }

using plaster to create this folder of HCL - you can automaticly set the backend key to be specific to this application, as you can't use HCL variables in the backend. 
**note i am using azurerm 2.5 and terraform 13.3**

### madatory modules

The only actual mandatory module is the resource group, as we can use this same system to use terraform to spin up IaaC web farms, Vnets, database clusters, pretty much anything terraform azurerm can do - and some of that would not need the "madatory" services a web app does. 

web-applications would have the app registration module and app insights module set as defaults

### resource group 

#### application resource group 

    module "resourcegroup" {
    source    = "./rg"
    providers = {
        azurerm = azurerm.westus
    }
    rgid = var.rgid
    Sengineeriamrole = var.Sengineeriamrole
    engineeriamrole = var.engineeriamrole
    mgmtiamrole = var.mgmtiamrole
    Sengineerobject = var.Sengineerobject
    engineerobject = var.engineerobject
    mgmtobject = var.mgmtobject
    team = var.team
    application = var.application
    enviro = var.enviro
    azlocname = var.azlocname
    principal_id = module.appreg.principal_id
    }

note any variables you want to pass into a module have to be declared and have vaules in the root of the HCL. so i am passing in various things, like AD group objects and their IaM roles - as i am setting RBAC roles on the RG level by default. 
you can also pass in values you get from other modules by default the resource group would set IAM roles for the app registration module - this allows each application to have its own app registration and unique IAM roles for the application resources per environment. 