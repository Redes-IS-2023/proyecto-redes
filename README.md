# Azure Infrastructure

## Requirements

- [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-windows?tabs=azure-cli)
- [Terraform](https://developer.hashicorp.com/terraform/downloads)
- Have an [Azure Student](https://azure.microsoft.com/en-us/free/students/) account

## Login to Azure using shell

Use the next command to login using the web browser

```bash
az login
```

Use in case there is more than one subscription use the next command to set it up

```bash
az account set --subscription "cec75a14-921a-4051-a74d-9b3650c17559"
```

## Run with Make

Use the next Make commands to make use of the project:

```
make init
```

```
make destroy
```

```
make clear
```

## Initialize Terraform

```
terraform init
```

## Create a Terraform execution plan

```
terraform plan --var-file=conf/group.tfvars -out main.tfplan
```

```
terraform apply main.tfplan
```

## Verify the results

terraform output -raw resource_group_name
terraform output -raw dns_zone_name

```
az network dns zone show \
 --resource-group $resource_group_name \
 --name $dns_zone_name
```

## Clean up resources

```
terraform plan -destroy --var-file=conf/group.tfvars -out main.destroy.tfplan
```

```
terraform apply main.destroy.tfplan
```

## Validate resources

Use the next command to check if the DNS is routing the IPs correctly

```
nslookup [domain-name] [name-server]
```

Use the next command to check to which DNS is the local machine routing to

```
ipconfig /all | findstr "DNS\ Servers"
```

## Source

- [Quickstart: Create an Azure DNS zone and record using Terraform](https://learn.microsoft.com/en-us/azure/dns/dns-get-started-terraform?tabs=azure-cli)

- [Exercise - Create alias records for Azure DNS](https://learn.microsoft.com/en-us/training/modules/host-domain-azure-dns/6-exercise-create-alias-records)
