# resource management

## application grouped

### azure web app service Platform

Each microservice will be grouped with all its required services within resource groups. The api management service will act as the api gateway for all web apps
and multiple web apps will share app service plans to reduce costs and effectiveness
network security is controlled through one vnet and network security groups

![resource grouping](https://s3-us-west-1.amazonaws.com/donfouts.io/apim.png)

[App Services](app.md)

---

![resource grouping](https://s3-us-west-1.amazonaws.com/donfouts.io/container_use.png)

a very simplified version of how the application will flow on this architecture is here
-ember application at the client, will request information that will go to the api gateway - then to the Azure web app service, our goal is to keep DB resources in the cloud as well to reduce latency.  other on-prem apis the web app service needs to access will be tunneled  through our VPN to San Diego data center

![resource grouping](https://s3-us-west-1.amazonaws.com/donfouts.io/webapp2onpremflow.png)
