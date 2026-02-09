# Azure CLI

| WHAT | LINK |
| --- | --- |
| Azure CLI | [https://learn.microsoft.com/en-us/cli/azure/?view=azure-cli-latest](https://learn.microsoft.com/en-us/cli/azure/?view=azure-cli-latest) |
| Azure Subscription CLI | [https://learn.microsoft.com/en-us/cli/azure/manage-azure-subscriptions-azure-cli?view=azure-cli-latest&tabs=bash](https://learn.microsoft.com/en-us/cli/azure/manage-azure-subscriptions-azure-cli?view=azure-cli-latest&tabs=bash) |

### Shortcut CLI commands:

```powershell
az login
```

```powershell
az account show
```

```powershell
az account subscription list
```

```powershell
az account set --subscription "xyz"
```

#### webapp 

```powershell
az webapp config access-restriction show --name *REPLACE_ME* --resource-group *REPLACE_ME* --query "ipSecurityRestrictions" -o json | ConvertFrom-Json
```
