(under construction)
# Azure Container Registry (ACR) and Azure Container Instance (ACI)

1. Create Container registry

<img src="../../images/cr1.PNG" width="80%">

This will create ACR for you (your company) for images.

List all ACRs:

```
az acr list -o table
```

2. Log in to a registry

```
az acr login --name myregistry
```
or

```
docker login myregistry.azurecr.io
```

4. Tag an image before pushing it to ACR:
```
docker tag <IMAGE_ID> ebdregister.azurecr.io/nginx:latest
```

5. Publish an image to the ACR:
```
docker push ebdregister.azurecr.io/nginx:latest
```

6. List images in ACR:
```
az acr repository list -n ebdregister
```
You can also check an image in the portal:

<img src="../../images/cr3.png" width="80%">

Here you can also see a docker pull command:

<img src="../../images/cr4.png" width="80%">


7. Before deploying to Azure Container Instance (ACI) we need to enable access:

<img src="../../images/cr2.png" width="80%">

8. Create ACI:

<img src="../../images/cr5.png" width="80%">

9. Check the created container. Note, it is in a "Running" state:

<img src="../../images/cr6.png" width="80%">

Note the IP address of the running instance:

<img src="../../images/cr7.png" width="80%">

10. Make a call to the container from your browser:

<img src="../../images/cr8.png" width="80%">



