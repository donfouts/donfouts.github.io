# ASH Naming Schema Dictionary
Below are agreed upon names for resources - if you are building out a resource that is not listed below present your request to the DevOps Tribe to solidify the ASHTech standard before provisioning.

## Genernal

|Asset type| Scope| Format|Examples|
|--|--|--|--|
| Resource Group | Subscription | rg-<App or service name>-<Subscription type>-<###> | rg-pactbroker-rnd-001 |
| API management service instance | Global | apim-<App or service name> | apim-apigateway-dev |


## Networking

|Asset type| Scope| Format|Examples|
|--|--|--|--|
| Virtual network | Resource group | vnet-<Subscription type>-<Region>-<###> | vnet-rnd-westus-001 |
| Subnet | Virtual network | snet-<subscription>-<subregion>-<###> | snet-rnd-westus-001 |
| Network interface (NIC)  | Resource group | nic-<vm name>-<subscription> | nic-vmiis001-rnd |
| Load balancer (external) | Resource group | lb-<application>-<env>-<###>| lb-ashlink-prd-001|
| Traffic Manager Profile | Global | traf-<application>-<env> | traf-empowereddecisions-prd |
| Public IP address| Resource Group | pip-<application>-<env>-<###> | pip-ashlink-prd-001|

## Compute

|Asset type| Scope| Format|Examples|
|--|--|--|--|
| Virtual Machine | Resource group | vm<policy name or app name><###> | vmiis001 |
| web app | global | app-<App Name>-<Environment>-<###>.[{azurewebsites.net | app-clinicdetail-rnd-001.azurewebsites.net|
| function app | global | func-<App Name>-<Environment>-<###>.[{azurewebsites.net}] | func-name-rnd-001.azurewebsites.net|
| app service plan | global | plan-<grouping>-<Environment> | plan-dsowebapps-dsodev|
| container registry | global | acr<application> | acrdsogateway|

## Storage

|Asset type| Scope| Format|Examples|
|--|--|--|--|
| storage account | Global | st<storage name><###> | stdsoinfra001 |

## Database

|Asset type| Scope| Format|Examples|
|--|--|--|--|
| Redis | Global | redis-<app name>-<Environment> | redis-clinicdetail.api-rnd |
| Cosmos DB | Global | cosmos-<app name>-<Environment> | cosmos-clinicdetail.api-rnd |

## Management and governance

|Asset type| Scope| Format|Examples|
|--|--|--|--|
| Key Vault | Global | kv-\<vault use>-\<Environment>-\<\#\#\#> | kv-isoautomation-rnd-001 |
| Application Insights | Global | appi-\<application name>-\<Environment> | appi-clinicdetail-dev |