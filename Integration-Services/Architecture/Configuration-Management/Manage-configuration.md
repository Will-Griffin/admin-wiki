[[_TOC_]]

## Overview

.NET [Configuration](https://docs.microsoft.com/en-us/dotnet/core/extensions/configuration-providers#file-configuration-provider) via the `JSON` file provider is used to manage all configuration.

## Requirements

- The Azure service principal used to deploy the configuration requires the `Azure App Configuration Data Owner` role assigned.

## App Settings File

Configuration is managed in `appsettings*.json` files. The main file should include all configuration with default values. Additional files respective to the environment exist to override settings respective to that environment. Only configuration that is different is required to exist in the environment specific file.

| File                         	| Description                                                                                       	|
|------------------------------	|---------------------------------------------------------------------------------------------------	|
| appsettings.json             	| Used for cross environment or base configuration. All properties should be defined at this level. 	|
| appsettings.Local.json       	| Used local configuration only.                                                                    	|
| appsettings.Development.json 	| Used for Azure development environment configuration.                                             	|
| appsettings.QA.json          	| Used for Azure QA environment configuration.                                                      	|
| appsettings.Production.json  	| Used for Azure production environment configuration.                                              	|

## Push configuration to Azure App Configuration

```
az appconfig kv import --separator : --name appcs-lacdmh-hidex-soap-config-dev-w1 --source file --path "appsettings.json" --format json

az appconfig kv import --label Development --separator : --name appcs-lacdmh-hidex-soap-config-dev-w1 --source file --path "appsettings.Development.json" --format json
```