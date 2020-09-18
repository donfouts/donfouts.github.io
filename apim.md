# api management services
I won't go into the concept of or benifits of a api gateway, there are plenty of sites to help you determin if that is benificial to your project. 
---
- The api management service (apim) can be intergrated into our private network and also can trust internal CA issued certs
- the apim will have its own app service plan to remove it from the operational conditions and costs of individal web apps
- the apim is considered a "shared" resource, cross team all api traffic should end up going through the apim in the application layer archetecure provided as a requriement from the DEVs. 
![apim](https://stdsoinventory0001.blob.core.windows.net/mdwikiimages/apim.png)
---
- config changes to the apim will be managed via the apim repo intergration option stored in its own azure repos repository, to allow for shared - - - - contribution with standard git branching stratgies, and proper versioning capacity. 
![apim_repo](https://stdsoinventory0001.blob.core.windows.net/mdwikiimages/apim_repo.png)

---
[terraform modules](tfmodules.md)
