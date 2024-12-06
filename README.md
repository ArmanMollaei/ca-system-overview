# ca-system-overview


This repository automates the provisioning of Azure resources for containerized applications. It includes an Azure DevOps pipeline and ARM templates to streamline the process of creating and deploying key Azure resources such as Azure Container Registry (ACR), Azure Container Apps (ACA), and ACR service connections. The solution is designed to help automate the creation and deployment of containerized workloads while ensuring security and scalability in the cloud environment.

## Prerequisites

Before you can deploy and configure the solution, ensure you have the following:

1. **Azure Cloud Account**  
   You will need an active Azure Cloud account to provision resources like Azure Container Registry (ACR) and Azure Container Apps (ACA). If you don’t have an account, you can create one [here](https://azure.microsoft.com/en-us/free/).

2. **Azure DevOps Account**  
   An active Azure DevOps account is required to configure and run the CI/CD pipelines. You can create an Azure DevOps account [here](https://dev.azure.com/).
   
3. **A PAT In Azure Devops.**
   A Personal Access Token (PAT) with the necessary permissions.


Make sure you have the necessary permissions to create and manage resources in Azure and to configure and execute pipelines in Azure DevOps.

## Repository Structure

The repository consists of the following key components, each hosted in its own repository:

1. **[ca-system-overview](https://github.com/ArmanMollaei/ca-system-overview)**:  
   This repository contains the overall system structure, including the main setup and configurations for the solution. It serves as the central repository for managing the complete solution's deployment process.

2. **[ca-repo](https://github.com/ArmanMollaei/ca-repo)**:  
   This repository contains the core containerized application code. It holds the Dockerfiles, application source code, and related configuration files needed to build and deploy the application to Azure Container Apps (ACA).

3. **[ca-azazure-template](https://github.com/ArmanMollaei/ca-azazure-template)**:  
   This repository contains the Azure Resource Manager (ARM) templates used to provision Azure resources such as Azure Container Registry (ACR), Azure Container Apps (ACA), and the Azure Devops service connection. The templates define the infrastructure needed for the application.



## Instructions on how to fork, configure and deploy the solution on our own cloud environment


### 1. Fork the GitHub Repository
- Go to your GitHub repository.
- Click on the **Fork** button in the top-right corner to create a copy of the repository under your GitHub account.

### 2. Create an Azure DevOps Project
Sign in to Azure DevOps.
Create a new project to host the repo and pipelines.

### 3. Import both GitHub repositories into Azure DevOps.
In your Azure DevOps project, navigate to Repos. 
Click on Import Repository and enter the URL of your forked GitHub repository and do this for both repositories:
  * [ca-repo](https://github.com/ArmanMollaei/ca-repo)
  * [ca-azazure-template](https://github.com/ArmanMollaei/ca-azazure-template)

### 4. Generate a Personal Access Token (PAT)
- Go to your Azure DevOps account.
- Navigate to **User Settings** > **Personal Access Tokens**.
- Click on **New Token** and generate a token with `Read, query, & manage` access to manage Service Connections.
- Copy the generated token. 

### 5. Add the PAT as a Variable in Azure DevOps Library
- In your Azure DevOps project, navigate to **Pipelines** > **Library**.
- Click on **+ Variable Group** to create a new variable group and name it `CI`.
- Add a variable named `PAT` and paste the generated token as its value.
- Make sure to mark the `PAT` variable as **secret** to keep it secure.












• High-level documentation explaining the overall architecture of the solution implemented.
We'd love that you are rewarded for your effort by sharing your best work online as part of your
personal portfolio, but please be so kind as to remove references to Capgemini first!
