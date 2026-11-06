# Terraform: Stractured Learning

A structured, practical learning journey to evolve my HomeLab/on-prem Terraform experience into building production-ready Infrastructure as Code (IaC) on Microsoft Azure.

---

## From a HomeLab/On-Prem Mindset to Public Cloud

I started learning `Terraform` during COVID-19, when I built my `Proxmox HomeLab` cluster.

Together with `Ansible`, this was my first introduction to the world of [Infrastructure as Code](https://developer.hashicorp.com/terraform/tutorials/azure-get-started/infrastructure-as-code) with `Terraform`.

Over the years, I worked at organisations that used `Terraform` with on-premises cloud environments.

In my current position, I work on a project that uses `Bicep` on `Azure`. `Bicep` is a great tool, but my personal preference tends to lean towards `Terraform`.

To make a long story short, I realized that I had never learned `Terraform` in a structured way that would be a good fit for a `public cloud` environment. I thought this would make a great personal project, so here we are!

Please note that many concepts you can find here, are taken by [Terraform - Up and Running](https://www.oreilly.com/library/view/terraform-up-and/9781098116736/) book.

Prerequises:
- Create A free [Azure Account](https://azure.microsoft.com/en-us/pricing/purchase-options/azure-account-b).
- [Install Docker](https://docs.docker.com/engine/install/)
- [Install Vs Code](https://code.visualstudio.com/download)
- *Clone* this repo and open it as *DevContainer*.

## Environment Setup

1. Open the repo on `vs-code`. The editor should prompt to open the project as `DevContainer`. If that never happens `ctrl+shift+p`/`cmd+shift+p` and type: `Dev Containers: Rebuild Container`.

2. Make sure that everything runs, `ctrl+shift+~` and check:

```bash
az login
terraform -version
```

3. Connect to `Azure` and make the proper setup:

> **Warning:** You may need to `az logout` & `az login` again to proceed `az ad sp create-for-rbac ...`. Follow the instructions and then return!

```bash
az login # follow the browser process
ARM_SUBSCRIPTION_ID=$(az account list | grep id | awk '{{print $2}}' | tr -d '"' | tr -d ',')

az account set --subscription "$ARM_SUBSCRIPTION_ID"
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/$ARM_SUBSCRIPTION_ID"
```

4. Create envs with the last command output:

```bash
export ARM_CLIENT_ID="<APPID_VALUE>"
export ARM_CLIENT_SECRET="<PASSWORD_VALUE>"
export ARM_SUBSCRIPTION_ID="$ARM_SUBSCRIPTION_ID"
export ARM_TENANT_ID="<TENANT_VALUE>"
```

Or even beter create `.env` file on the roor of this repo:

```bash
ARM_CLIENT_ID="<APPID_VALUE>"
ARM_CLIENT_SECRET="<PASSWORD_VALUE>"
ARM_SUBSCRIPTION_ID="$ARM_SUBSCRIPTION_ID"
ARM_TENANT_ID="<TENANT_VALUE>"
```

## Next steps

Lets explore [Azure Terraform Provider](./src/0.Azure-basics/README.md).