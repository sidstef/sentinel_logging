# Azure Logging Deployment

This repository contains ARM templates for deploying various Azure logging resources, including Log Analytics workspaces, custom log functions, alerts, and Sentinel incidents.

## Prerequisites

- Azure CLI installed
- An Azure subscription
- Appropriate permissions to create resources in the target resource group

## Deployment Steps

### 1. Deploy Log Analytics Workspace and AKS Cluster Logging

This template deploys a Log Analytics workspace and configures diagnostic settings for an AKS cluster.

#### Parameters

- `logAnalyticsWorkspaceName`: Name of the Log Analytics workspace.
- `aksClusterName`: Name of the existing AKS cluster.
- `diagnosticName`: Desired name of the diagnostic setting.

#### Command

```sh
az deployment group create \
  --name deploy-logging \
  --resource-group <your-resource-group> \
  --template-file infra/azure-logging/deploy.logging.json \
  --parameters @infra/azure-logging/parameter.logging.json
```

### 2. Deploy Custom Log Function

This template deploys a custom log function in the Log Analytics workspace.

#### Parameters
- `workspaceName`: Name of the existing Log Analytics workspace.
- `functionName`: Desired name of the function.
- `location`: Region of the Log Analytics workspace.
- `functionDisplayName`: Desired display name of the function.
- `category`: Desired category of the function.
- `query`: KQL query for the function.
- `functionAlias`: Desired alias for the function.

#### Command

```sh
az deployment group create \
  --name deploy-custom-log-function \
  --resource-group <your-resource-group> \
  --template-file infra/azure-logging/deploy.custom-log-function.json \
  --parameters @infra/azure-logging/parameters.custom-log-function.json
```

### 3. Deploy Alerts

This template deploys an alert rule in the Log Analytics workspace.

#### Parameters

- `logAnalyticsWorkspaceName`: Name of the existing Log Analytics workspace.
- `alertName`: Desired name of the alert.

#### Command

```sh
az deployment group create \
  --name deploy-alerts \
  --resource-group <your-resource-group> \
  --template-file infra/azure-logging/deploy.alerts.json \
  --parameters @infra/azure-logging/parameters.alerts.json
  ```

 ### 4. Deploy Sentinel Incidents

This template deploys a Sentinel incident rule in the Log Analytics workspace.

#### Parameters

- `workspace`: Name of the existing Log Analytics workspace.
- `alert-rule-name`: Desired name of the alert rule.


#### Command

```sh
az deployment group create \
  --name deploy-sentinel-incidents \
  --resource-group <your-resource-group> \
  --template-file infra/azure-logging/deploy.sentinel-incidents.json \
  --parameters @infra/azure-logging/parameters.sentinel-incidents.json
```

### Notes

- Ensure that the parameter files are correctly filled with the required values before running the deployment commands.
- Replace <your-resource-group> with the name of your Azure resource group.