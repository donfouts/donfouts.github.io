# Non Production

non prod will be a more regulated area to run operationally functional environments. the following envriornments are a requirement as per our development and testing teams. the network will be managed like a hub and spoke model with route tables to restrict intra-environment traffic.

## Environments

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

![non_prod network](https://stdsoinventory0001.blob.core.windows.net/mdwikiimages/nonprod2.png)

### Terraform 

Terraform will be used to provision and manage configuration changes of the infrastructure in Non-Prod

![non_prod](https://stdsoinventory0001.blob.core.windows.net/mdwikiimages/nonprod1.png)