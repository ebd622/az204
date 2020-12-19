(under construction)
# Azure Container Registry and Azure Container Instance

1. Create Container registry

<img src="../../images/cr1.PNG" width="80%">


This will create a container for you (your company) for images.

2. Log in to a registry

```
az acr login --name myregistry
```
or

```
docker login myregistry.azurecr.io
```



3. Publish an image to the Register

```
docker pull ebdregister.azurecr.io/nginx:latest
```
