# Azure-Big-Data-Dev-Ops

```
# Login
az login

# Script parameters
subscriptionId=<<REMOVED>>
resourceGroup="Azure-Big-Data-Dev-Ops"
location="centralus"
today=`date +%Y-%m-%d-%H-%M-%S`
deploymentName="MyDeployment-$today"


# Select Subscription
az account set -s $subscriptionId


# Create resource group
az group create \
  --name        $resourceGroup \
  --location    $location


# Deploy the ARM template
az group deployment create \
  --name                 $deploymentName \
  --resource-group       $resourceGroup \
  --template-file        azuredeploy.json \
  --parameters           @azuredeploy.parameters.json \
  --mode                 Incremental


# Deploy Security Center at the Subscription Level (not resource group)
deploymentName="MyDeployment-SecurityCenter-$today"


# Deploy Security Center
az deployment create \
  --name                 $deploymentName \
  --location             $location \
  --template-file        azuredeploy.securitycenter.json \
  --parameters           @azuredeploy.parameters.securitycenter.json


# Clean up resource group (for testing - delete everything)
az group delete --name $resourceGroup
```



