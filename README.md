# WordpressStack-AzureCLI
Template to deploy Wordpress Stack from Azure CLI

# Demo of Azure CLI deployment

In this sample we will deploy an ARM template from Azure CLI that creates a Linux VM (Ubuntu 14.04) with Nginx, PHP, MySQL and Wordpress installed.

The ARM script will setup the VM, Network, Storage, Security Group, and an auxilliar script shell will do the "internal" settings such nginx installs and more. This script is available at https://github.com/rmmartins/scripts/blob/master/WordpressStack/wp-stack-install.sh

You need to have the [Azure CLI installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).

Bellow the commands:
```sh
az login
az group create -n <ResourceGroupName> -l "<Location>"
az group deployment create --resource-group <ResourceGroupName> --template-file "<template.json path>" --parameters "<parameters.json path> --verbose"
```
In this case:
```sh
cd /tmp
wget https://raw.githubusercontent.com/rmmartins/WordpressStack-AzureCLI/master/template.json
wget https://raw.githubusercontent.com/rmmartins/WordpressStack-AzureCLI/master/parameters.json
az login
az group create -n LabWordpress -l "Brazil South"
az group deployment create --resource-group LabWordpress --template-file "template.json" --parameters "parameters.json" --verbose
```

And now, connect to VM via SSH:

```
ip=`az vm show --resource-group LabWordpress --name ubuntuvm --show-details -d | grep "publicIps" | awk -F'"' '{ print $4}'`
ssh rmartins@"$ip"
```

Once logged, if want  in you can retrieve all metadata from instance

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-03-01"
```

# Video demonstrations

You can see the demo of CLI deployment here: [https://asciinema.org/a/ct0oEipYq9wCnVfJqpiUxjmKY](https://asciinema.org/a/ct0oEipYq9wCnVfJqpiUxjmKY)

If you would like to see the demo of Visual Studio deployment, see at: [https://youtu.be/joZvr-sP3xE](https://youtu.be/joZvr-sP3xE)
