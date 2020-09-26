# Operational Azure cloud strategy and architecture 

The goal of this wiki is to document the Operational plan and strategies while moving; legacy "monalith" applications, cloud enabled applications / micro-services, and clound native microservices along with any supporting assets required.  I am going to keep this free from "fluf" - if you want to learn about why you should move to the cloud, or why you shouldn't move to the cloud there are thousands of other people who have published those conversations for your thought provoking. I will also keep the details of highly technical aspects out of this document as these specifics change too quickly to maintain a wiki with its details. I am trying to create an ecosystem where technical details that need to be discovered by technical staff for technical reasons - don't have to search wiki pages, or worry the documentation is kept up todate, but rather have tools and systems in place to get those details from the running state - and allowing the infrastructure itself be the "known good."

---
# Requirements 

I was provided (well helped define) the following requirements for this evolution:
The architecture supports multiple types of services in the microservices platform; stateful, stateless, and orchestration/integration.

![ash_platform_architecture](https://stdsoinventory0001.blob.core.windows.net/mdwikiimages/ASH-platform-architecture.png)

---
## Stateful

Stateful services persist data to some sort of data store. These data stores could be a SQL database, NoSQL database, or blob storage.

---
## Stateless

Stateless services do not persist data, rather they are used for business rules, computations, data massaging, integration, etc. An example of a stateless service could be a website which we have indicated in the diagram. A stateless website could simply host static HTML, Javascript, images, and CSS.

---
## Orchestration/Integration

Orchestration/integration services are a special type of stateful service that "orchestrates" or "integrates" work with other microservices. This type of stateful service will be common within the architecture where they direct the workflow of long running business processes. Stateful services persist data specific to the state of the workflow in which they direct.

---
## Versioning

Services can be versioned, deployed, and run independently of each other. This is an important feature of the architecture that it will allow development teams to perform A/B testing and blue/green deployments.

---
## Scaling

Lastly, auto scaling is a fundamental feature of the architecture. As demand for a services increases, the platform will spin up additional instances of a service, based on pre-configured rules, to prevent bottlenecks, timeouts, and overall failure. After the demand has passed the platform will scale back down based up the pre-configured rules.

---
## Load Balancing

Load balancing technology sits in front of our services in order to evenly distribute network traffic across the individual instances of ASH's services. This ensures no one instance is overwhelmed by a surge in traffic and prevents bottlenecks, sluggishness, and failure.

---
## CI/CD

Continuous Integration / Continuous Deployment is a fundamental piece of the ASH DevOps culture. No application or service is manually configured and deployed into the environments. Rather as change is introduced, it is automatically validated and deployed frequently. This method of delivery will continue in the new architecture.

---
## Data Ingestion/Export

ASH receives data from both clients and vendors through various methods and formats. The ability to manipulate and act upon this data as it is received is important so that business processing is fluid and agile. The architecture supports data and event streams to support this requirement. Additionally as our systems process data, our business requires insight into that processing. Exporting that data into big data storage such as data warehouses or data lakes is critical so that it can be analyzed and reported on.

---
## RBAC Security

Role-Based Access Controls are a fundamental part of the architecture security. These controls enable ASH to control who has access to the various layers and components of the architecture and what operations they can perform.

---
## Application Monitoring

The ability to monitor the health of the architecture and the systems running within it is critical. Development teams, DevSecOps, and IT Operations are concerned with the health and performance of the systems and services ASH owns. Monitoring allows ASH to ensure business processing is functioning properly and that ASH's customers and members are being served well.

---
## Security Monitoring

Understanding security risks and mitigating those risks is critical to ASH's business. The architecture supports the monitoring of ASH's network, servers, applications, and services to understand where vulnerabilities are and addressing them.

---
# takeway

There is no book on how to ramp up this solution for an enterprize with 120+ web applications, dozands of data bases, built in a method that was not cloud native.  This site is not a tutorial on how to setup xyz service in azure, this site will hopfully walk through the trials and tribulations of this journey. The cloud has "Power, Unlimited power!" and "Your focus determines your reality"
[![the master](https://stdsoinventory0001.blob.core.windows.net/mdwikiimages/master-yoda-vector.png)](https://devopsdays.org/)
