# Deploying Infrastructure to Azure using Terraform

## Table of Contents
1. [Introduction](#introduction)
2. [Requirements](#requirements)
3. [Setting Up the Environment](#setting-up-the-environment)
4. [Terraform Basics](#terraform-basics)
5. [Creating the Infrastructure](#creating-the-infrastructure)
6. [Advanced Terraform Concepts](#advanced-terraform-concepts)
7. [Conclusion](#conclusion)

---

## Introduction

In this project, we will deploy infrastructure to Azure using Terraform. The course is divided into two parts: 

1. Understanding Terraform basics.
2. Covering advanced Terraform concepts.

By the end of this guide, you'll have a good understanding of how to deploy and manage Azure resources using Terraform.

---

## Requirements

To follow along, ensure you have the following:

1. **Azure Account**: Ensure you have a subscription with billing enabled.
2. **Terraform Installed**: Install Terraform on your local machine.
3. **Azure CLI Installed**: Install Azure CLI for authentication.
4. **Optional**: A domain name for a personalized URL.

---

## Setting Up the Environment

### Azure CLI Installation

1. Visit [Microsoft Learn](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli).
2. Follow the instructions for your operating system to install the Azure CLI.
3. Authenticate to your Azure account using:
   ```sh
   az login
