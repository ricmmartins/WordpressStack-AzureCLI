
# WordpressStack-AzureCLI
Template to deploy Wordpress Stack from Azure CLI

# Demo of Azure CLI deployment

In this sample we will deploy an ARM template from Azure CLI that creates a Linux VM (Ubuntu 14.04) with Nginx, PHP, MySQL and Wordpress installed.

The ARM script will setup the VM, Network, Storage, Security Group, and an auxilliar script shell will do the "internal" settings such nginx installs and more. This script is available at https://github.com/rmmartins/scripts/blob/master/WordpressStack/wp-stack-install.sh

Bellow the commands:
```sh
azure login
azure group create -n <ResourceGroupName> -l "<Location>"
azure group deployment create --resource-group <ResourceGroupName> --template-file "<template.json path" --parameters-file "parameters.json path"
```
In this case:
```sh
azure login
azure group create -n LabWordpress -l "Brazil South"
azure group deployment create --resource-group LabWordpress --template-file "template.json" --parameters-file "parameters.json"
```


