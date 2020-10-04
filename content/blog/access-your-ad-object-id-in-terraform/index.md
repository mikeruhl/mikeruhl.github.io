---
title: "Access your Azure AD Object ID in Terraform"
date: 2019-06-05
description: import from previous blog.
---
I ran into an issue today trying to use the azurerm provider in Terraform. I needed to create a Key Vault, then add myself as an access policy so that in the same .tf I could add a certificate. Once I saw a [similarly frustrated user](https://serverfault.com/a/970269/526579) on Serverfault, I decided to figure this out.

What I came up with was a powershell script that used the az cli to get the current user's object id.

Here is a demo of the solution, also posted as my answer:

There is a way to do this using the Azure CLI. Here is a demo:

Powershell Script:
```powershell
#scripts/getuser.ps1
$t = az ad signed-in-user show
$t = "$t"
$j = ConvertFrom-Json $t
Write-Output "{`"object_id`":`"$($j.objectId)`"}"
```

<br/><br/>
Terraform:
```hcl
//main.tf
provider "azurerm" {
  subscription_id = var.subscription_id
}

data "external" "user" {
  program = ["powershell.exe", "${path.module}/scripts/getuser.ps1"]
}

output "object_id" {
    value = data.external.user.result.object_id
}
```

Keep in mind `az ad signed-in-user` is fairly new so make sure everything is up to date.

Resources:

[https://docs.microsoft.com/en-us/cli/azure/ad/signed-in-user?view=azure-cli-latest](https://docs.microsoft.com/en-us/cli/azure/ad/signed-in-user?view=azure-cli-latest)

[https://www.terraform.io/docs/providers/external/data_source.html](https://www.terraform.io/docs/providers/external/data_source.html)



