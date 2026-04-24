# Cloud-Native-Internal-Developer-Platform-on-Microsoft-Azure
This repository contains the configuration and deployment logic for an Internal Developer Platform (IDP) hosted on Microsoft Azure. The platform is designed to streamline application development and deployment by integrating CI/CD, containerization, orchestration, and comprehensive monitoring.

Architecture Overview
The platform utilizes a modern cloud-native stack:

Developer Portal: Backstage

CI/CD: GitHub Actions

Container Registry: Azure Container Registry (ACR)

Orchestration: Azure Kubernetes Service (AKS)

Observability: Azure Log Analytics & Managed Grafana

Project Structure
/infrastructure: Shell scripts for provisioning Azure resources.

/app: Source code for the Backstage internal developer portal.

/.github/workflows: Automated pipelines for building and deploying the platform.

Deployment Steps
1. Azure Infrastructure Setup
Initialize the base resources including the Resource Group, Container Registry, and AKS Cluster:

Bash
# Create Resource Group
az group create --name idp-project-rg --location canadacentral

# Create Azure Container Registry
az acr create --resource-group idp-project-rg --name myproject --sku Basic

# Create AKS Cluster
az aks create --resource-group idp-project-rg --name myAKSCluster --node-count 1 --node-vm-size Standard_B2s_v2 --generate-ssh-keys

# Link ACR to AKS
az aks update -n myAKSCluster -g idp-project-rg --attach-acr myproject
2. Application Deployment
The platform uses Docker to containerize the Backstage application.

Build the image locally or via GitHub Actions.

Push the image to the myproject registry.

Deploy the Backend App to the AKS cluster.

3. Monitoring & Insights
To ensure platform stability, the following monitoring tools are integrated:

Log Analytics: Centralized logging for cluster operations.

Azure Managed Grafana: Visualizing cluster performance and application health.

Bash
# Create Log Analytics Workspace
az monitor log-analytics workspace create --resource-group Practice --workspace-name Monitoring --location Canadacentral

# Create Grafana Instance
az grafana create --name myGrafana --resource-group Practice --location Canadacentral
Getting Started
To get a local instance running or to contribute:

Clone this repository.

Ensure you have the Azure CLI installed and authenticated.

Navigate to the /infrastructure directory to run the setup scripts.
