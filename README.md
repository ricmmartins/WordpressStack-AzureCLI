
# WordpressStack-AzureCLI
Template to deploy Wordpress Stack from Azure CLI

# Demo of Azure CLI deployment

In this sample we will deploy an ARM template from Azure CLI that creates a Linux VM (Ubuntu 14.04) with Nginx, PHP, MySQL and Wordpress installed.

The ARM script will setup the VM, Network, Storage, Security Group, and an auxilliar script shell will do the "internal" settings such nginx installs and more. This script is available at https://github.com/rmmartins/scripts/blob/master/WordpressStack/wp-stack-install.sh

Bellow the commands:
```sh
az login
az group create -n <ResourceGroupName> -l "<Location>"
az group deployment create --resource-group <ResourceGroupName> --template-file "<template.json path>" --parameters "<parameters.json path>"
```
In this case:
```sh
cd /tmp
wget https://raw.githubusercontent.com/rmmartins/WordpressStack-AzureCLI/master/template.json
wget https://raw.githubusercontent.com/rmmartins/WordpressStack-AzureCLI/master/parameters.json
az login
az group create -n LabWordpress -l "Brazil South"
az group deployment create --resource-group LabWordpress --template-file "template.json" --parameters "parameters.json"
```

And now, connect to VM via SSH:

```
azure vm show vm show LabWordpress ubuntuvm
ip=`azure vm show LabWordpress ubuntuvm | grep "Public IP address" | awk -F ':' '{print $3}'`
ssh rmartins@"$ip"
```

# Useful Links

* [Install Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [Overview Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview)
* [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)

