Azure Deployment with Terraform
Welcome to our comprehensive guide on deploying a project to Azure using Terraform, one of the most popular Infrastructures as Code (IaC) tools. This README will walk you through the basics and advanced concepts of Terraform, showcasing a real-world example of deploying a static website to Azure.

Table of Contents
Introduction
Requirements
Installation
Project Structure
Terraform Basics
Advanced Concepts
Deployment Steps
Cleanup
Conclusion

Introduction
In this project, we will deploy a static website to Azure using Terraform. Terraform allows you to define cloud and on-premises resources in human-readable configuration files, enabling automation, version control, and reusability of your infrastructure.

Requirements
To follow along, ensure you have the following:

Azure Account: With a valid subscription.
Terraform: Installed on your local machine.
Azure CLI: For authentication between Terraform and Azure.
Domain Name (Optional): For a personalized URL.
Installation
Azure CLI
Install Azure CLI by following Microsoft's official guide.

Terraform
Install Terraform using your preferred package manager:

macOS: brew install terraform
Windows: choco install terraform
Linux: sudo apt-get install terraform
Authenticate Azure CLI:

bash
Copy code
az login
Project Structure
Our project is organized as follows:

css
Copy code
.
├── infra
│   ├── main.tf
│   ├── provider.tf
│   ├── variables.tf
│   ├── backend.tf
│   └── terraform.tfvars
└── README.md
main.tf: Defines resources (Resource Group, Storage Account, Blob).
provider.tf: Specifies providers.
variables.tf: Contains variable definitions.
backend.tf: Configures remote state storage.
terraform.tfvars: Assigns values to variables.
Terraform Basics
Provider Configuration
hcl
Copy code
provider "azurerm" {
  features {}
}
Resource Group
hcl
Copy code
resource "azurerm_resource_group" "resource_group" {
  name     = var.resource_group_name
  location = var.location
}
Storage Account
hcl
Copy code
resource "azurerm_storage_account" "storage_account" {
  name                     = var.storage_account_name
  resource_group_name      = azurerm_resource_group.resource_group.name
  location                 = azurerm_resource_group.resource_group.location
  account_tier             = "Standard"
  account_replication_type = "LRS"
  kind                     = "StorageV2"
}
Blob Storage for Static Website
hcl
Copy code
resource "azurerm_storage_blob" "blob" {
  name                   = var.index_document
  storage_account_name   = azurerm_storage_account.storage_account.name
  storage_container_name = "web"
  type                   = "Block"
  source_content         = var.source_content
  content_type           = "text/html"
}
Advanced Concepts
Remote Backend
To store the state file remotely:

Create a storage account and container via Azure CLI.
Configure backend.tf:
hcl
Copy code
terraform {
  backend "azurerm" {
    resource_group_name   = "tfstate-rg"
    storage_account_name  = "tfstate"
    container_name        = "tfstate"
    key                   = "terraform.tfstate"
  }
}
Variables
Define variables in variables.tf:

hcl
Copy code
variable "location" {
  description = "The Azure region to deploy resources."
  type        = string
}

variable "resource_group_name" {
  description = "The name of the resource group."
  type        = string
}

variable "storage_account_name" {
  description = "The name of the storage account."
  type        = string
}

variable "index_document" {
  description = "The index.html file for the static website."
  type        = string
}

variable "source_content" {
  description = "The content of the index.html file."
  type        = string
}
Assign values in terraform.tfvars:

hcl
Copy code
location             = "East US"
resource_group_name  = "rg-terraform-demo"
storage_account_name = "tfstorageaccount12345"
index_document       = "index.html"
source_content       = "<html><body><h1>Ahoy! This website was deployed using Terraform.</h1></body></html>"
Deployment Steps
Initialize Terraform:

bash
Copy code
terraform init
Plan Infrastructure:

bash
Copy code
terraform plan
Apply Configuration:

bash
Copy code
terraform apply
Confirm the apply operation by typing yes when prompted.

Access the Deployed Website
After deployment, find the website URL in the Azure portal under the storage account's static website configuration.

Cleanup
To destroy the resources created by Terraform:

bash
Copy code
terraform destroy
Confirm the destroy operation by typing yes when prompted.

Conclusion
In this project, we successfully deployed a static website to Azure using Terraform. We covered the basics, advanced concepts, and best practices, including remote state storage and variable management. This setup not only automates infrastructure deployment but also ensures it is reproducible and maintainable.
