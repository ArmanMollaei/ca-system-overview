# Architecture of the Solution

## Cloud:
I prefer to use Azure Cloud , but we can also use other cloud providers like AWS or GCP.

## High-level Design:

![pip](https://github.com/user-attachments/assets/d2b45280-2911-4acf-bba1-21b9aed23c49)


## Infrastructure Architecture:

The solution leverages Azure Container Registry (ACR), Azure Container Apps (ACA), Azure DevOps, and Resource Groups to implement a modern, scalable, and efficient application delivery pipeline. The architecture ensures that containerized applications are built, stored, and deployed seamlessly in a secure and controlled manner.

### Why Select These Components?

#### 1. Azure Container Registry (ACR)
Azure Container Registry (ACR) is used to store Docker images in a secure, private registry within Azure.

#### 2. Azure Container Apps (ACA)
Azure Container Apps (ACA) provides scalable infrastructure that meets all the necessary requirements for containerized applications. This includes features like certificates, ingress, versioning, replicas, health checks, and more. 
ACA also supports automatic scaling based on HTTP concurrent requests, which is managed through KEDA (Kubernetes Event-Driven Autoscaling).
  
#### 3. Resource Group
A Resource Group in Azure helps manage all resources in one place. It simplifies the process of managing, organizing, and monitoring resources.
Additionally, it allows granting access to multiple user accounts, facilitating collaboration and access control.

#### 4. Azure DevOps
Azure DevOps is a set of development tools and services that helps teams to store source code, implement continuous integration (CI), and continuous deployment (CD) pipelines. With Azure DevOps, you can automate build, test, and release processes using Azure's build machines.

#### 4. Automation Infra Souloution Azure Resource Management:
I use ARM templates in JSON format, with two separate files for each resource: one for the template and one for the parameters.

## Conclusion
I could use other solutions like Azure Container Instances or AKS, but these components—ACR, ACA, Azure DevOps, and Resource Group—have all the necessary features, are easy to use, and are suitable for this small stack with a cost that fits.
For automation, we could use other solutions like Terraform and others, but since this stack is for testing and is small, I chose to use ARM templates.


* Below is a picture of the pipeline stages:
  
The last stage is for cleaning up all resources and the Azure service connection.

<img width="1417" alt="Screenshot 2024-12-06 at 10 36 32 AM" src="https://github.com/user-attachments/assets/7b43fc43-b284-4fcd-a879-d384228ecc7f">

#### Pipeline Stages:

- The first stage creates the Resource Group.
- The second stage creates ACR and the Service Connection in Azure through an API call.
- The third stage creates ACA for production.
- The fourth stage creates ACA for development.
- The last stage performs cleanup (This stage requires approval).

* This pipeline runs on a commit to the main branch.


## Application Architecture:

In this application, we have a React app and a Java backend. The Dockerfile uses multi-stage builds to reduce the size of the image.
I build the app and have devised branches for multiple environments:

- The dev branch deploys to the development environment.
- The main branch deploys to the production environment.
- Each image is tagged with the corresponding environment.

For testing, I use Trivy for security scanning, but we can also use other tools like SonarQube or others.

The stages are shown in the image below:

<img width="1435" alt="Screenshot 2024-12-06 at 10 48 51 AM" src="https://github.com/user-attachments/assets/8409b4d4-9c02-445f-adaf-cd7d1cb4c8fa">



Final deployment picture:

<img width="1438" alt="Screenshot 2024-12-06 at 11 02 15 AM" src="https://github.com/user-attachments/assets/d9bcf183-4c07-443f-915c-4b078ae12560">



<img width="1440" alt="Screenshot 2024-12-06 at 11 04 59 AM" src="https://github.com/user-attachments/assets/1e16440e-b41e-440d-98bc-618836f00c44">

<img width="1440" alt="Screenshot 2024-12-06 at 11 04 09 AM" src="https://github.com/user-attachments/assets/2a1ca29d-9973-4e60-a511-63b4b740bf45">




