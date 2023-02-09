- Resource Provider Registrations: see https://docs.microsoft.com/en-us/azure/azure-resource-manager/troubleshooting/error-register-resource-provider?tabs=azure-cli

Registrations required for Synapse deployment (Microsoft.Network and Microsoft.Sql)


```
az provider list --query "[?namespace=='Microsoft.Network']" --output table
az provider register --namespace Microsoft.Network
az provider show -n Microsoft.Network --output table
```

 