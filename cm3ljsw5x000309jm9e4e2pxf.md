---
title: "How to Purchase a Domain on Azure via CLI"
datePublished: Tue Feb 16 2021 22:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm3ljsw5x000309jm9e4e2pxf
slug: how-to-purchase-a-domain-on-azure-via-cli
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1731844664243/2cc9004b-0a6e-41c5-bb32-8342a98e4497.jpeg
tags: azure, domain, appservices

---

Managing domains is a critical aspect of establishing an online presence, and Azure offers a streamlined way to acquire domains using the Azure Command-Line Interface (CLI). This guide explains the steps to purchase a domain on Azure using CLI commands.

## Prerequisites

1. **Azure Subscription**: Ensure you have an active Azure subscription.
    
2. **Azure CLI Installed**: Download and install Azure CLI from [Microsoft's official documentation](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli).
    
3. **Sign In**: Log in to Azure CLI by running:
    
    ```bash
    az login
    ```
    
    Follow the prompts to authenticate.
    
4. **Resource Group**: Identify an existing resource group or create one:
    
    ```bash
    az group create --name <resource-group-name> --location <location>
    ```
    

## Steps to Purchase a Domain

### 1\. Verify Domain Availability

Azure requires you to confirm if a domain is available for purchase. Use the following command:

```bash
az network dns zone list --output table
```

If the domain isn’t listed, check availability:

```bash
az network private-dns zone show --name <domain-name>
```

### 2\. Register the Domain

Azure doesn’t provide direct domain purchase functionality via CLI, but it supports integration with domain registrars through DNS zones. You can register a domain externally (e.g., GoDaddy) and configure it with Azure. If Azure Domain Registration is configured in your setup, run:

```bash
az network dns zone create --resource-group <resource-group-name> --name <domain-name>
```

This creates a DNS zone for the domain in Azure.

### 3\. Configure Name Servers

Update your domain’s name servers with those provided by Azure. To list Azure’s name servers:

```bash
az network dns zone show --name <domain-name> --query "nameServers"
```

Log in to your registrar’s portal and replace their default name servers with Azure’s.

### 4\. Validate Setup

After configuration, ensure the domain is functional by querying DNS records:

```bash
nslookup <domain-name>
```

### Optional: Add Custom Records

If needed, create additional DNS records, such as A, CNAME, or TXT:

```bash
az network dns record-set a add-record --resource-group <resource-group-name> --zone-name <domain-name> --record-set-name <record-name> --ipv4-address <ip-address>
```

Repeat this for other record types as necessary.

## Conclusion

Purchasing and managing domains through Azure CLI involves configuring DNS zones and name servers. While Azure doesn’t offer direct domain registration through CLI, its DNS services allow seamless integration with external registrars. This guide simplifies the process to help users manage their domains effectively.

For further reading, consult the [Azure DNS Documentation](https://learn.microsoft.com/en-us/azure/dns/).

---