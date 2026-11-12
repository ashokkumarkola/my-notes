# Azure Cheat Sheet

## Hierarchy

```text
Tenant (Entra ID) → Management group → Subscription → Resource group → Resource
```

## Core services

| Service | Use |
|---|---|
| Virtual Machines | VMs |
| App Service | PaaS web apps |
| Functions | Serverless |
| AKS | Managed Kubernetes |
| Container Apps | Simple containers |
| Blob Storage | Object storage |
| Azure SQL / MySQL | Managed SQL |
| Cosmos DB | NoSQL |
| VNet | Private network |
| Entra ID | Identity (was Azure AD) |
| Key Vault | Secrets, keys, certs |
| Monitor | Logs, metrics |

## CLI setup

```bash
az version
az login
az account list -o table
az account set --subscription <id-or-name>
az account show
```

## Resource groups

```bash
az group create -n rg-demo -l eastus
az group list -o table
az group delete -n rg-demo --yes --no-wait     # deletes everything inside
```

## VM

```bash
az vm create -g rg-demo -n vm1 --image Ubuntu2204 \
  --admin-username azureuser --generate-ssh-keys
az vm list -o table
az vm start      -g rg-demo -n vm1
az vm stop       -g rg-demo -n vm1             # still billed
az vm deallocate -g rg-demo -n vm1             # stops billing compute
az vm list-ip-addresses -g rg-demo -n vm1 -o table
```

## Storage

```bash
az storage account create -n mystorage123 -g rg-demo -l eastus --sku Standard_LRS
az storage container create --account-name mystorage123 -n files
az storage blob upload --account-name mystorage123 -c files -f file.txt -n file.txt
```

## App Service, AKS, Key Vault

```bash
az webapp up -n my-app --runtime "PYTHON:3.12"
az aks get-credentials -g rg-demo -n aks1      # kubectl access
az keyvault secret set  --vault-name kv1 -n db-pass --value '***'
az keyvault secret show --vault-name kv1 -n db-pass --query value -o tsv
```

## Output tips

```bash
-o table | json | tsv
--query "[].name"               # JMESPath filter
```
