[[_TOC_]]

## Overview

Azure Active Directory will be used as the identity provider for OAuth based authentication flows. Some of the applications exposed publicly will use Azure Active Directory [application registration](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app).

External clients such as providers will be represented as an application registration in Azure Active Directory.

Application registrations will be required for each environment.

## OAuth Client-Credential Flow

Approach used to authenticate requests from the provider to the healthcare APIs. The provider is represented as an application registration Azure Active Directory and granted access to other applications.

![cicd](/.attachments/authn-client-credential-flow.png)

## Application Registrations

- [API Registrations](#apis) - Various components will require an application registration.
- [Provider Registrations](#providers) - Each provider will require an application registration. This is the case where the provider system is the entity authenticating against the County of Los Angeles system.

![cicd](/.attachments/authn-aad-app-registrations.png)

### Request Flow

:::mermaid
graph LR;
    A[Provider] -->|register for API| B(OnBoarding) --> C{Grant Consent}
    C -->|One| D[Grant consent to DPH Store]
    C -->|Two| E[Grant consent to DMH Store]
:::

### APIs

1. FHIR Proxy - An application registration will be required for each FHIR store that the proxy fronts. This will allow for providers to be granted consent to each store individually.

    - One of these app registrations will be used to secure the FHIR proxy.
    - Both of the app registrations' uri will be used as the audience configuration in the Azure Function's auth settings. The format is `api://{application-id}`

    | Registration Setting 	| API or Application                                                                 	| Azure Portal                                                                                               	 |
    |----------------------	|------------------------------------------------------------------------------------	|------------------------------------------------------------------------------------------------------------	|
    | Name                 	| HIDEX-FHIR-API-{DPH \| DMH}-{environment}                                          	|                                                                                                            	 |
    | Redirect Urls        	| Department specific FHIR API Host                                                  	|                                                                                                            	 |
    | Identifier Uris      	| `api://{Application/Client ID}`                                                    	| Under "Expose an API" set "Application ID URI"                                                             	 |
    | Permissions          	| see table below                                                                    	| Under "API permissions"                                                                                    	 |
    | Application Roles    	| see [Authorization](/Architecture/Identity-%26-Access-Management/Authorization.md) 	| Under "App Roles" or manually updating the "Manifest". Override the "appRoles" array in the manifest JSON. 	|

    | Permissions        	| API                   	| Description                                                                    	|
    |--------------------	|-----------------------	|--------------------------------------------------------------------------------	|
    | User.Read          	| Microsoft Graph       	| Microsoft Graph delegated permission User.Read (Sign in and read user profile) 	|
    | user_impersonation 	| Azure Healthcare APIs 	| Access Azure Healthcare APIs                                                   	|

### Providers

Each provider system requires an application registration. This will support system to system authentication using OAith client-credential flow.

| Registration Setting 	| Provider                          	|   	|
|----------------------	|-----------------------------------	|---	|
| Name                 	| HIDEX-PROVIDER-{DMH or DPH}-{DEV or QA or PROD}-{alphanumeric min1 max7}              	|   	|
| Redirect Urls           	| Url or Uri of the provider system 	|   	|
| Identifier Uris      	| `api://{Application/Client ID}`   	|   	|
| Permissions          	| see table below                   	|   	|

The FHIR Proxy roles are described [here](/Architecture/Identity-%26-Access-Management/Authorization.md).

| Permissions  	| API        	| Description         	|
|--------------	|------------	|---------------------	|
| Reader       	| FHIR Proxy 	| Resource Writer     	|
| Writer       	| FHIR Proxy 	| Resource Reader     	|
| Organization 	| FHIR Proxy 	| FHIR Store Instance 	|