# Deploying FastAPI on Azure Container Instance

This guide will walk you through the process of deploying a FastAPI application on Azure Container Instance (ACI) using Docker commands with Azure authentication. Azure Container Instance is a platform-as-a-service (PaaS) offering that allows you to run containerized applications in the cloud without managing the underlying infrastructure.

## Prerequisites

Before you begin, make sure you have the following:

- An [Azure account](https://azure.com/free).
- [Docker](https://www.docker.com/) installed on your local machine to build the container image.
- Your FastAPI application codebase ready for deployment.

## Steps

### 1. Containerize FastAPI Application

#### Build and Push Docker Image

1.1. Open a terminal and navigate to your FastAPI application's root directory.

1.2. Create a Dockerfile in the app directory.

1.3. Build and test your Docker image:
   ```bash
   docker build -t myimage .
   docker run -p 80:80 myimage
```
Access your FastAPI app locally by opening a web browser and visiting [http://localhost:80](http://localhost:80).

1.4. Stop the running Docker container (`Ctrl+C`).

### 2. Deploy on Azure

2.1. Log in to the Azure portal.

2.2. Create a Resource Group:

   - Click on "+ Create a resource".
   - Search for "Resource group" and click "Create".
   - Provide a unique name and choose a region, then click "Review + Create" and finally "Create".

2.3. Create an Azure Container Registry:

   - In the Azure portal, navigate to your Resource Group.
   - Click "+ Add" > "Containers" > "Container Registry".
   - Fill in the registry details and click "Review + Create" and then "Create".

![create-cont-registry](https://github.com/Dana2024/fastapi-container-azure/assets/130597970/bc655d36-d26d-49b2-bbb8-2b5bb6304779)


2.4. Log in your local server to Azure:
   ```bash
   docker login login-server -u user-name -p password
```
(Note: You can access login server, user name and password in the container registry under Access keys tab, and you will need to enable admin user to have a password.)

2.5. Build and push your Docker image to Azure Container Registry:

 ```bash
docker build -t login-server/container-name:build-tag .
docker push login-server/container-name:build-tag
```
In the Azure portal, navigate to your Resource Group.
Click "+ Add" > "Containers" > "Container Instances".

Fill in the container instance details:
Container Name:
Image Source: Azure Container Registry
Image:

Click "Review + Create" and then "Create".

![container-instance](https://github.com/Dana2024/fastapi-container-azure/assets/130597970/0311285b-18aa-4baa-a7cf-3e600c3ea0f8)


### 3. Access Your FastAPI Application
3.1. Once the container is running, you can access your FastAPI application using the provided IP address.

Congratulations! You have successfully deployed your FastAPI application on Azure Container Instance using Docker commands. 
Your application is now accessible via the provided URL.

![fastapi-on-container-instance](https://github.com/Dana2024/fastapi-container-azure/assets/130597970/37fe473d-7c8b-4c79-adce-4c14f3311411)


For more information and advanced configurations, refer to the Azure Container Instances documentation.

