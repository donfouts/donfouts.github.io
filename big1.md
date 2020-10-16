# 3 subscriptions 1 tenant

![inter-subscription-map](https://s3-us-west-1.amazonaws.com/donfouts.io/inter-subscription-map.png)

The 10k foot view is architected to have 3 subscriptions (Research and Development, Non Production, and Production) each with separate VPN tunnels to the Corporate datacenter, all three are initially set to 3gig but there is capacity to increase production up to 10 gig if needed in the future. Resources will be group logically by application and environment to allow for security measures to deny inter-environment traffic. 

## Research and Development

A sandbox for software/database/ops/appsec engineers to build solutions, tune performance and security, and develop IaC (Hashicorp config language.)

#### outstanding progress

- continual auditing
- policy enforcement
- auto spin down


## Non Production

non prod will be a more regulated area to run operationally functional environments. the following envriornments are a requirement as per our development and testing teams. the network will be managed like a hub and spoke model with route tables to restrict intra-environment traffic.

### Environments

#### DEV

- Component tests
- Mocked data

#### TST

- Intergration tests
- System tests 
- UX review
- Internal Load tests

#### STG

- PEN tests
- UAT
- Training
- PO approval
- Ops Perf tests
- Accessibility tests

---

![non_prod network](https://s3-us-west-1.amazonaws.com/donfouts.io/nonprod2.png)

## Production

production will be the most regulated, limited access subscription. 

* no changes will occur outside of IaC *

### Terraform 

Terraform will be used to provision and manage configuration changes of the infrastructure in Non-Prod

![non_prod](https://s3-us-west-1.amazonaws.com/donfouts.io/nonprod1.png)

