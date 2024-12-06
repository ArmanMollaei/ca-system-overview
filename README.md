# ca-system-overview


This repository automates the provisioning of Azure resources for containerized applications. It includes an Azure DevOps pipeline and ARM templates to streamline the process of creating and deploying key Azure resources such as Azure Container Registry (ACR), Azure Container Apps (ACA), and ACR service connections. The solution is designed to help automate the creation and deployment of containerized workloads while ensuring security and scalability in the cloud environment.


## Repository Structure

The repository consists of the following key components, each hosted in its own repository:

1. **[ca-system-overview](https://github.com/ArmanMollaei/ca-system-overview)**:  
   This repository contains the overall system structure, including the main setup and configurations for the solution. It serves as the central repository for managing the complete solution's deployment process.

2. **[ca-repo](https://github.com/ArmanMollaei/ca-repo)**:  
   This repository contains the core containerized application code. It holds the Dockerfiles, application source code, and related configuration files needed to build and deploy the application to Azure Container Apps (ACA).

3. **[ca-azazure-template](https://github.com/ArmanMollaei/ca-azazure-template)**:  
   This repository contains the Azure Resource Manager (ARM) templates used to provision Azure resources such as Azure Container Registry (ACR), Azure Container Apps (ACA), and the ACR service connection. The templates define the infrastructure needed for the application.



## Instructions on how to fork, configure and deploy the solution on our own cloud environment


### 1. Fork the GitHub Repository
- Go to your GitHub repository.
- Click on the **Fork** button in the top-right corner to create a copy of the repository under your GitHub account.

### 2. Clone the Forked Repository to Your Local Machine
- Clone both repositories using the following command:
  ```
  git clone https://github.com/ArmanMollaei/ca-azazure-template.git
  git clone https://github.com/ArmanMollaei/ca-repo
  ```

### 3. Create an Azure DevOps Project
Sign in to Azure DevOps.
Create a new project to host the repo and pipelines.

### 4. Import both GitHub repositories into Azure DevOps.
In your Azure DevOps project, navigate to Repos. 
Click on Import Repository and enter the URL of your forked GitHub repository adn do this for both repositories.
  ```
  git clone https://github.com/ArmanMollaei/ca-azazure-template.git
  git clone https://github.com/ArmanMollaei/ca-repo
  ```













• High-level documentation explaining the overall architecture of the solution implemented.
We'd love that you are rewarded for your effort by sharing your best work online as part of your
personal portfolio, but please be so kind as to remove references to Capgemini first!
