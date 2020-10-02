# azure key vault

key vault will be used to store secrets needed for CI/CD and during application runtime, phase 2 would include ssl certification storage as well.  

Access to the key vault is restricted to the application registration for that specific Application, and the terraform app registration and devops AD group for management uses.

![kv access](https://stdsoinventory0001.blob.core.windows.net/mdwikiimages/kv_access.png)