# web app services

we are a .net shop - so the following guidelines are in place for this inital blueprint:

- azure devops is our build and release pipeline tool
- To accomidate interal CA issued certs to access both on-prem and lower environments (non-public) we are containerizing the application
- .net core gives us the flexibility to run applications in both windows or linux - the containers will be linux for the reduced overhead of the os layer of the container infrastructure.

![container_use](https://s3-us-west-1.amazonaws.com/donfouts.io/container_use.png)

containers on app servers might be a stepping stone to a Kubernetes Platform option in the future, but until then azure container registry will sufice for managing continer images. 

---
# app service plans

The approach for deployment of app service plans (plan) are to consolidate web applications into general plans to maximize the effeciences of each plan.  Addtional plans will be created as needed by app requiremnts, and if a (1) application demands enough to warrent it's own plan - the plan will be named accordly.  

![plans](https://s3-us-west-1.amazonaws.com/donfouts.io/plans.png)
---
[terraform modules](tfmodules.md)