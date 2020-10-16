# Keyvault

all keyvaults will be provisioned with terraform, several secrets are generated during the terraform provisioning steps, and terraform can insert those secrets into the application's key vault during provisioning. in this example the Instrumentation Key created when the application insights instance is created can be stored in their key vault. The access policies for the keyvault will be limited to the Terraform application, the app registration created for the app and the devops team. 
this allows azure pipelines to pull the app insights intrumentation key from the vault during the app release while restricting access to the secrets to only critical applications. 

![kv](https://s3-us-west-1.amazonaws.com/donfouts.io/kv_access.png)

---
[terraform modules](tfmodules.md)