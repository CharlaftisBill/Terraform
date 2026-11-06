# Azure Terraform Provider

In this directory you can find a terraform file named `main.tf`.

This file consists of the following parts:

## Terraform Block

The `terraform` block contains configuration.

`required_providers` will be used to "import" the provider that will be used to provision our infrastructure.

```terraform
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm" # or registry.terraform.io/hashicorp/azurerm
      version = "~> 3.0.2"
    }
  }
}
```

## Provider Block

The `provider` block configures the providers, refered by `terraform` block.

A provider is a plugin that `Terraform` uses to manage resources.

```terraform
terraform {...}

provider "azurerm" {
  features {}
}
```

In this example we didn't configured the `provider`.

## Resource

Inside `resource` blocks we describe components of our infrastructure (vm, pod, resource groups, etc).

```terraform
terraform {...}

provider "azurerm" {...}

resource "azurerm_resource_group" "rg" {
  name     = "myTFResourceGroup"
  location = "westus2"
}
```

Resource blocks defined by two identifiers expressed in **double quotes** as strings:

- `resource type`,
- `resource name`

```terraform
# resource type -> "azurerm_resource_group"
# resource name -> rg

resource "azurerm_resource_group" "rg" {
  name     = "myTFResourceGroup"
  location = "westus2"
}
```

The `resource type` and `resource name`form a **unique ID** for the resource.

 ```terraform
resource "azurerm_resource_group" "rg" { ... }

# will be reffered as `azurerm_resource_group.rg` from this point on
```

Resource blocks contain `arguments` which you use to **configure the resource**.

```terraform
resource "azurerm_resource_group" "rg" {
  name     = "myTFResourceGroup"
  location = "westus2"
}
```

## Terraform commands

**A.** Move on right directory:

```bash
cd ./src/0.Azure-Terraform-Provider
```

**B.** Format and Validate tf files:

```bash
terraform fmt
terraform validate
```

**C.** Initialize the directorys set-up:

```bash
terraform init
```

This coomand will create some **files and directories** that will be used later to manage the `Azure`.

**D.** Let's see what result would our `.tf` would have if we `apply` it right now

```bash
terraform plan
```

In this simple and linear case this `plan` will be run exactly as `apply` (we will see next). In a real world example though may have to use a `-out` argument to make sure that the `plan` that will be followed will be the same.

**E.** Let's run our execution `plan`

```bash
terraform apply

# validate the plan and type yes to execute it
```

**F.** Validate that the `Resource Group` created successfully and state lists it

```bash
az group list -o table

terraform state list
```

**G.** Inspect the current state using:

```bash
terraform show
```


## Modify the state

You can update the `main.tf` by adding, deleting or updating it and then run:

```bash
terraform apply
```

## Release the created resources

```bash
terraform destroy

# check the execution plan and then type `yes`
```

## Variables and Outputs

There are two more files at this dierctory that help us refer to values with friendly names:

```terraform
# variable.tf
variable "virtual_network_name" {
  default = "myTFVnet"
}

# outputs.tf
output "resource_group_id" {
  value = azurerm_resource_group.rg.id
}
```

After `terraform apply` we can inspect the values of our `output` aliases using:

```bash
terraform output resource_group_id
```