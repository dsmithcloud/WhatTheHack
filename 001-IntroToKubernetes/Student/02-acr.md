# Challenge 2: The Azure Container Registry

[< Previous Challenge](./01-containers.md) - **[Home](../README.md)** - [Next Challenge >](./03-k8sintro.md)

## Introduction

Now that we have our application packaged as container images, where do they go?

## Description

In this challenge we will be creating and setting up a new, private, Azure Container Registry. This will be the new home of the containers we just created. We will see later on how Kubernetes will pull our images from this registry.

- Deploy an Azure Container Registry (ACR)
- Ensure your ACR has proper permissions and credentials set up
- Login to your ACR
- Push your Docker container images to the ACR
- List all images in your ACR

- To create the registry from the CLI, use:
    - `az acr create -n <name of registry> -g <resource group> --sku Standard`
- To login to the ACR, use:
    - `az acr login --name <name of ACR>`
- To tag images, use:
    - `docker tag <name of image> <name of ACR>/<namespace>/<name of image>`
- For example:
    - `docker tag content-web peteacr01.azurecr.io/wthaks/content-web`
    - `docker tag content-api peteacr01.azurecr.io/wthaks/content-api`
- To push the docker image, use:
    - `docker push <name of ACR>/<namespace>/<name of image>`
- For example:
    - `docker push peteacr01.azurecr.io/wthaks/content-web`
    - `docker push peteacr01.azurecr.io/wthaks/content-api`
- To list images in the repository, use:
    - `az acr repository list --name <name of ACR>`

## Success Criteria

1. You have provisioned a new Azure Container Registry
1. You have deployed your container images to the registry.
2. You can log into the registry and see all images.