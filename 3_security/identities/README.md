(under constuction)
# Implement Managed Identities for Azure resources

Rsources:
* [Managed Identities with Azure AD (video)](https://youtu.be/sA_mXKy_dKU)
* [Azure Data Factory Tutorial (video)](https://youtu.be/EpDkxTHAhOs)

### Scenario 1: Store keys in a configuration file
Searvice A connects to Service B using a key stored in a configuration file

<img src="../../images/mi_1.PNG" width="90%">

### Scenario 2: Use Azure AD for authentication accross two services
Azure AD will manage an authentication process. 

<img src="../../images/mi_2.PNG" width="90%">

But we still have a challenge to store identity credentials in a configuration file, the same as in the Scenatio1.

### Scenario 3: Use Azure AD Managed Identity

<img src="../../images/mi_3.PNG" width="80%">

#### Key service characteristic

* Credential are moved out of application code (out of config-files);
* Identity created and tied with resource lifecycle (i.e. when you delete a resource - an identity will be also deleted);
* One click/command to set up with no additional cost;
* Managed Identity are Service Principals of spacial type

