[[_TOC_]]

## Overview

[Azure App Configuration](https://docs.microsoft.com/en-us/azure/azure-app-configuration/overview) centrally manages application settings and feature flags. 

## Design considerations

- Centrally manage application settings
- Manage application configuration and secrets from a single store
- Connect various system components to a central configuration store
- Single pane of glass view of configuration for a given environment
- Dynamically update application settings without the need to redeploy or re-start an application
- Provide feature flag management

## Design recommendations

- Each department will use an instance of Azure App Configuration in each environment.
- Shared infrastructure will use a separate instance of Azure App Configuration in each environment.
- Each system component that requires configuration will use key-based identifiers to separate and structure configuration for multiple components in a single instance of the configuration store.
    - `FhirProxy:FhirClient:Url`
- Each system component will maintain configuration as code (CaC) using [.NET configuration](https://docs.microsoft.com/en-us/dotnet/core/extensions/configuration) json files.
- Azure DevOps pipelines will be used to deploy application specific configuration into the configuration store.
- Only secret references will be maintained with the configuration as code.
- Azure KeyVault will be used to store secrets and integrated with Azure App Configuration.
- Application configuration will be validated on application startup. This will allow for the application to fail fast and during a blue/green deployment, the application configuration errors will be identified much sooner.

## Strategy

![strategy](/Integration-Services/.attachments/config-strategy.png)

## .NET Configuration

- Use simple .NET POCOs to define configuration. There should be no business logic in these classes.
- Use `appsettings.json` files to manage [configuration](https://docs.microsoft.com/en-us/azure/azure-app-configuration/concept-config-file) for ASP.NET Core applications. See an example [here](https://dev.azure.com/LACDMH-DPH-Integration/HIDEX/_git/hidex-soap-proxy?path=/src/Lac.Hidex.SoapProxy/appsettings.json).

```cs
builder.ConfigurationBuilder.AddAzureAppConfiguration(options =>
{
  options.Connect("Endpoint=https://{storename}.azconfig.io;{connection}").Select("FhirProxy", LabelFilter.Null);
}, true);
```

### Registering and consuming configuration
- Register into .NET dependency injection

    ```csharp
    services.Configure<TOptions>(config.GetSection(section))
    ```
- Inject `IOptions<MyConfiguration>` into the corresponding .NET class that needs the configuration.


### Publishing configuration to the configuration store
- Configure Azure DevOps pipelines with the Azure App Configuration [DevOps task](https://docs.microsoft.com/en-us/azure/azure-app-configuration/push-kv-devops-pipeline) to publish configuration as code into the configuration store.

### Managing secrets with configuration as code

Use Key Vault references when configuring secrets in the `appsettings.json` files.

> NOTE: Use a separate file for Key Vault references such as `appsettings-secrets.json` This is required to when publishing configuration to the store.

```json
{
    "FhirClient": {
        "ClientSecret": "{\"uri\":\"https://<your-vault-name>.vault.azure.net/secrets/FhirClient:ClientSecret\"}"
    }
}
```