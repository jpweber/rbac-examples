# RBAC Examples
This repo contains examples of how to use RBAC for creating specific roles and service accounts for different use cases. Throughout the namespace is set to `jpw`. To use these in your environment the namespace should be changed to your desired namespace with a simple find and replace. PRs are welcome for new use cases or modificaitons to existing ones. 


## Use Cases
### [Image Setter](image-setter.yaml)
An account that can only modify the image of a deployment. Change the image in a deployment spec is one way people perform upgrades. This service account only has access to update, patch and get a deployment. 


### [App Deployer](app-deployer.yaml)
A service account that can create what an applicate deployment or job would need. It has abilities to get, list, watch, create, update and patch but cannot delete anything. It also has the ability to create and update secrets but cannot read or delete them. Purposely left out is the `DaemonSet` resource. The intent here is to prevent the normal deployment pipeline from deploying a `DaemonSet` that are commonly some form of infrastructure component and not an application or service. Essentially a very thin security layer, but a layer none the less. 


### [Support Staff](support-staff.yaml)
The Goal here is to create a role that has access to read many things and take part in some basic remediation, such as delete a pod, so that a replica set can generate a new one. A service account is here for example/testing purposes but this role should be bound to something using OIDC auth and not a single service account. 

### [Namespace Admin](ns-admin.yaml)
A common pattern is to provide a namespace per development team. In these cases the cluster operators will allow this team to have full access to their own name space to create and destroy things. This is an example role and role binding to provide Namespace level admin privileges. However some actions are restricted such as deleting the namespace or altering resource quotas or limits. A service account is here for example/testing purposes but this role should be bound to something using OIDC auth and not a single service account.