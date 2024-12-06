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


### 6. Set Up Azure Pipelines

#### For ac-azazure-template Pipeline:
- Go to Pipelines in your Azure DevOps project (e.g., ac-azazure-template).
- Click New Pipeline.
- Choose Azure Repos Git as the source.
- Select the ca-azazure-template repo from the list.
- Choose Existing Azure Pipeline YAML file.
- Define the branch as main and specify the path to the pipeline YAML file:
- Path: /azure-pipelines.yml
- Azure DevOps will use this YAML file to define your pipeline.

#### For ac-repo Pipeline in main Branch:
- Go to Pipelines in your Azure DevOps project (e.g., ac-repo).
-Click New Pipeline.
- Choose Azure Repos Git as the source.
- Select the ca-azazure-template repo from the list.
- Choose Existing Azure Pipeline YAML file.
- Define the branch as main and specify the path to the pipeline YAML file:
- Path: /azure-pipelines.yml
- Azure DevOps will use this YAML file to define your pipeline.

#### For ac-repo Pipeline in dev Branch:
- Go to Pipelines in your Azure DevOps project (e.g., ac-repo).
- Click New Pipeline.
- Choose Azure Repos Git as the source.
- Select the ca-azazure-template repo from the list.
- Choose Existing Azure Pipeline YAML file.
- Define the branch as dev and specify the path to the pipeline YAML file:
- Path: /azure-pipelines.yml
- Azure DevOps will use this YAML file to define your pipeline.
- And edit this pipline and click on settings and change name of pipline to dev






### 7. Set Up Service Connection Between Azure DevOps and Azure Cloud

Before running pipelines, you need to create a connection between Azure DevOps and Azure Cloud by setting up an **Azure Resource Manager** service connection. Follow these steps:

#### 1. Create Service Connection in Azure DevOps

##### Step 1: Go to Azure DevOps
- In your Azure DevOps project, go to **Project Settings**.
- Navigate to **Service Connections** under **Pipelines**.

##### Step 2: Add a New Service Connection
- Click on **New Service Connection**.
- Select **Azure Resource Manager**.
- Choose the **Identity type** as **App registration or managed identity (manual)**.
- Set **Credential** to **Workload identity federation**.

##### Step 3: Configure Service Connection
- **Service connection name**: `AzureDevops-ServiceConnection` (You can choose any name).
- **Description**: (Optional)
  
Click **Next**.

##### Step 4: Provide Azure Subscription Details
- **Subscription ID**: Enter your Azure Subscription ID.
- **Subscription Name**: Enter your Azure Subscription Name.
- **Application (Client) ID**: Enter the **Client ID** of the Azure App you create (described below).
- **Directory (Tenant) ID**: Enter the **Tenant ID** of the Azure App you create.

Click **Next**.

#### 2. Create the Azure App (Service Principal)

##### Step 1: Go to Azure Active Directory
- Sign in to the [Azure portal](https://portal.azure.com).
- Go to **Azure Active Directory**.

##### Step 2: Register a New Application
- Click **Add** > **App Registration**.
- Fill in the required data for the application:
  - **Name**: Choose a name for the app (e.g., `AzureDevOpsApp`).
  - **Supported account types**: Select **Accounts in this organizational directory only**.
  - **Redirect URI**: Leave it empty (or specify if required).

##### Step 3: Get Azure App Details
- After registration, go to the **Overview** page of your app and note down the following details:
  - **Application (Client) ID**
  - **Directory (Tenant) ID**

#### 3. Set Up Federated Credentials for Workload Identity Federation

##### Step 1: Set Up Federated Credentials
- Go to **Certificates & Secrets** for the application.
- Go to the **Federated Credentials** tab.
- Click **Add** and fill in the details:
  - **Issuer**: Use the issuer URL provided by Azure DevOps for the service connection.
  - **Subject Identifier**: Enter the subject identifier from Azure DevOps that corresponds to the service connection you want to create.

#### Step 3: Grant Access to the Application

1. Go to your **Azure Subscription** and navigate to the **Access control (IAM)** section.
2. Click on **Add role assignment**.
3. Under **Privileged administrator roles**, select either **Reader** or **Contributor**, depending on the level of access needed.
4. Click **Next**, then select **Members**.
5. Search for the Azure app you created, select it, and click **Save** to grant access.

#### 4. Finalize Service Connection Setup

- Once the above steps are completed, return to Azure DevOps and click **Verify and Save** to finalize the creation of your **Azure Resource Manager** service connection.
- The service connection should now be available for use in your pipelines.

---

After creating the service connection, you will be able to run pipelines that interact with Azure resources.






• High-level documentation explaining the overall architecture of the solution implemented.
We'd love that you are rewarded for your effort by sharing your best work online as part of your
personal portfolio, but please be so kind as to remove references to Capgemini first!
