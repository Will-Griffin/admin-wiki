[[_TOC_]]

## Overview

Azure App Configuration is added to the .NET host configuration via dependency injection. This configuration is added for all environments _except_ `Local`.

## Register in dependency injection

Add the following NuGet packages:

  - Microsoft.Azure.AppConfiguration.AspNetCore
  - Microsoft.Extensions.Configuration.Json
  - Microsoft.Extensions.Configuration.UserSecrets

## Manage .NET environment variable

.NET uses the environment variable `ASPNETCORE_ENVIRONMENT` to define the environment under which the application is running.

### Environment values

| Environment 	| Description                                               	|
|-------------	|-----------------------------------------------------------	|
| Local       	| Used for local development inside Visual Studio.          	|
| Development 	| Used when running from the Azure development environment. 	|
| QA          	| Used when running from the Azure QA environment.          	|
| Production  	| Used when running from the Azure production environment.  	|

## Configure local environment

> NOTE: Currently Azure App Configuration is not loaded when running locally.

1. Update the file `\src\Lac.Hidex.SoapProxy\Properties\launchSettings.json` and set the environment variable `ASPNETCORE_ENVIRONMENT` to 'Local'.
1. Configure `appsettings.Local.json` with any non-secret values. This file is excluded from source control but .NET user secrets should be used for those.
1. Store any secret values via .NET user secrets using the CLI:

    ```
    dotnet user-secrets set FhirClient:ApimAuthKey ""
    ```

## Configure Azure environment

1. Set the environment variable `ASPNETCORE_ENVIRONMENT` to the correct value. This is done via IaC.
1. Set RBAC between the Azure Managed Identity (MSI) of the service (App Service or Azure Function) and the Azure App Configuration. Use the `Azure App Configuration Data Reader` role.

## Configure Azure App Configuration to run locally

1. Store the Azure App Configuration connection in .NET user secrets.

    ```
    dotnet user-secrets set ConnectionStrings:AppConfig ""
    ```
1. Install Azure CLI and connect to the correct tenant.

   ```
   az login -t {tenantID}
   ```

1. Set the access policy of the Azure KeyVault instance with the developer credentials. Use `Get`/`List` secret permissions at a bare minimum.