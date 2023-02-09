[[_TOC_]]

## Overview

.NET [Configuration](https://docs.microsoft.com/en-us/dotnet/core/extensions/configuration-providers#file-configuration-provider) via the `JSON` file provider is used to manage all configuration.

## Requirements

- The Azure service principal used to deploy the configuration requires the `Azure App Configuration Data Owner` role assigned.

## Define secrets in app settings file

Secrets are only _defined_ in `appsettings.secrets.json`. No values should exist here other than a reference to Azure KeyVault.

> NOTE: The name of the keyvault instance should be a pipeline variable in the format of `__keyVaultName__`. This value is replaced by Azure Pipeline variables via the `replacetokens` step. This variable is currently stored under pipelines/vars/vars-global.yaml.
>
> The secret does not have to exist in Azure KeyVault to set this association but must exist when consumed.


```
{
  "items": [      
  {
    "content_type": "application/vnd.microsoft.appconfig.keyvaultref+json;charset=utf-8",
    "key": "FhirClient:ApimAuthKey",
    "label": null,
    "tags": {},
    "value": "{\"uri\":\"https://__keyVaultName__.vault.azure.net/secrets/Apim--AuthKey\"}"
  }
  ...
}
```

## Steps

1. Define secrets in `appsettings.secrets.json`.
1. Configure secret in Azure KeyVault.
1. Add property to configuration POCO in .NET.