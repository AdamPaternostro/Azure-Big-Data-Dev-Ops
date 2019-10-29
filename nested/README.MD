## This is for running a nested template locally
You need to sign in once and set your subscription once.

## Login, set subscription and resource parameters (only need to do once per session)
```
az login
az account set -s REPLACE_ME
resourceGroup="Azure-Big-Data-Dev-Ops"
location="centralus"
az group create --name $resourceGroup --location $location
```

## Test each nested template seperately
You can run each of the below blocks from your local development machine
```
today=`date +%Y-%m-%d-%H-%M-%S`
deploymentName="MyDeployment-$today"
az group deployment create \
  --name                 $deploymentName \
  --resource-group       $resourceGroup \
  --template-file        azuredeploy.loganalytics.json \
  --parameters           @local.parameters.loganalytics.json


```