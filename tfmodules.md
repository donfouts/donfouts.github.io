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

## mandatory modules

The only actual mandatory module is the resource group, as we can use this same system to use terraform to spin up IaaC web farms, Vnets, database clusters, pretty much anything terraform azurerm can do - and some of that would not need the "mandatory" services a web app does. 

web-applications would have the app registration module and app insights module set as defaults

## resource group 

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

note any variables you want to pass into a module have to be declared and have values in the root of the HCL. so I am passing in various things, like AD group objects and their IaM roles - as I am setting RBAC roles on the RG level by default. 
you can also pass in values you get from other modules by default the resource group would set IAM roles for the app registration module - this allows each application to have its own app registration and unique IAM roles for the application resources per environment. 

## optional modules (web application focus)

Different web applications will need different cloud services so by commenting out modules you can ensure that terraform won't execute them. 

## key vault

Most applications will leverage a key vault per environment to isolate secrets and limit access.
The module call passes in metadata for tagging and naming like 

- team name
- application name
- environment name

Variables required for the creation of the key vault are also passed in

- resource group it should be created in
- unique ID to conform to naming schema
- app registration ID to grant access to the vault


    #key vault

    module "kv" {
    source    = "./kv"
    providers = {
        azurerm = azurerm.westus
    }
    team = var.team
    application = var.application
    enviro = var.enviro
    azlocname = var.azlocname
    rg_name = module.resourcegroup.rg_name
    kvid = var.kvid
    principal_id = module.appreg.principal_id
    } 

[terraform links](https://www.terraform.io/docs/providers/azurerm/r/key_vault.html)

Some things worth mentioning

#### azure name limits 
so key vault's have to be 3-24 characters with the other strings I needed in the vault name - i had to shorten the application name to ensure it wasn't more than 13 characters.

    resource "azurerm_key_vault" "example" {
    name                        = join("-", ["kv",substr(var.application, 0, 13),var.enviro, var.kvid])
    ....
    }

terraform does tell you if you find it buried somewhere in the pages: that the ip_rules are a list... what does that mean - your network_acls block would look like this if you are whitelisting IPs to access the vault

    network_acls {
      default_action = "Deny"
      bypass         = "AzureServices"
      ip_rules       = [
          "x.x.x.x/32",
          "x.x.x.x/32"
      ]
    }

## azure cache for redis

Most applications are using a Redis cache for various aspects of their application, again these are provisioned per application per environment - and can be sized as needed with terraform.
The module call passes in metadata for tagging and naming like 

- team name
- application name
- environment name

Variables required for the creation of the key vault are also passed in

- resource group it should be created in (notice how i pulled RG name from the RG module results)
- sizing values like capacity/family/sku

    # redis

    module "redis" {
    source    = "./redis"
    providers = {
        azurerm = azurerm.westus
    }
    rediscapacity = var.rediscapacity
    redisfamily = var.redisfamily
    redissku = var.redissku
    team = var.team
    application = var.application
    enviro = var.enviro
    azlocname = var.azlocname
    rg_name = module.resourcegroup.rg_name
    } 

[terraform links](https://www.terraform.io/docs/providers/azurerm/r/redis_cache.html)

#### still to come....

## app service

## api management service

## DB options