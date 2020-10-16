# azure key vault

key vault will be used to store secrets needed for CI/CD and during application runtime, phase 2 would include ssl certification storage as well.  The keyvault will be provisioned in the resource group for that application - for better security and cost management. 

Access to the key vault is restricted to the application registration for that specific Application, and the terraform app registration and devops AD group for management uses.

![kv access](https://s3-us-west-1.amazonaws.com/donfouts.io/kv_access.png)