[[_TOC_]]

## Overview

The intent of this document is to outline the steps to use Postman for sending FHIR requests to the Azure Health Data Services FHIR store.

## Tech Stack

1. [Postman](https://www.postman.com/downloads/) *Currently only the desktop version is supported for client-credential OAuth flow*
2. [FHIR Resources](https://www.hl7.org/fhir/resourcelist.html)
3. [JSON](https://www.w3schools.com/whatis/whatis_json.asp)
4. [OAuth 2.0 client credentials flow](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-client-creds-grant-flow)
5. [FHIR Authentication](/Architecture/Identity-&-Access-Management)

## Setup

1. Setup environment
2. Setup collection

### Setup Postman Environment

1. Download the file [FHIR Search.postman_environment](https://dev.azure.com/LACDMH-DPH-Integration/HIDEX/_git/hidex-fhir-proxy?path=/postman/FHIR%20Search.postman_environment&version=GBmain&_a=contents)
2. [Import](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/) the environment file.
3. [Update] the Postman environment settings according to the environment you are connecting to.

    > NOTE: Consider naming the configuration to the specific environment you are connecting to. i.e. `HIDEX DPH FHIR DEV`


| Variable        	| Description                                                                                                                                                                            	| Location                                                                                         	| Format                 	|
|-----------------	|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|--------------------------------------------------------------------------------------------------	|------------------------	|
| tenantId        	| The Azure AD tenant ID that represents the Identity Provider. Usually unique across all environments.                                                                                  	| This can be found from the Azure Active Directory overview pane.                                 	| Guid                   	|
| clientId        	| The Azure AD application registration `Application ID` that mocks a provider.                                                                                                          	| This can be found from the Azure Active Directory Application Registration overview pane.        	| Guid                   	|
| clientSecret    	| The Azure AD application registration secret that mocks a provider.                                                                                                                    	| This is stored in Azure KeyVault in each respective environment and department subscription.     	| Secret                 	|
| bearerToken     	| The auto-generated JWT token used to make requests. Leave this value alone as it will be initially blank and auto-populated.                                                           	|                                                                                                  	|                        	|
| resource        	| The `audience` identifier the request is being made for. This points to the Azure AD application registration identifier that represents the FHIR store the provider is connecting to. 	| This can be found from the Azure Active Directory Application Registration `Expose an API` pane. 	| api://{AppId}/.default 	|
| fhirurl         	| The url to the FHIR endpoint. This will be the Azure API Management external url.                                                                                                      	| This can be found from the Azure API Management overview pane in the shared subscription.        	| Url                    	|
| subscriptionKey 	| The "api-key" used to connect to Azure API Management. This is unique to each environment.                                                                                             	| This can be found from the Azure API Management in the shared subscription.                      	| Secret                 	|

### Import Postman Collection

1. Download the file [FHIR Search.postman_collection.json](https://dev.azure.com/LACDMH-DPH-Integration/HIDEX/_git/hidex-fhir-proxy?path=/postman/FHIR%20Search.postman_collection.json&version=GBmain&_a=contents)
2. [Import](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/) the collection file.

## Usage

> NOTE: Each request requires Authorization. Once a token is requested there is an expiration date so it can be reused for a certain time frame.

1. Select the [active](https://learning.postman.com/docs/sending-requests/managing-environments/#selecting-an-active-environment) environment you want to connect to in Postman.
1. Run `AuthorizeGetToken` request.
1. Run request such as `List Patient by Given,Family,Gender`

## Troubleshooting

1. 401 Unauthorized
    - Error
      ```json
      {
        "resourceType": "OperationOutcome",
        "issue": [
            {
                "severity": "error",
                "code": "login",
                "diagnostics": "The client needs to initiate an authentication process."
            }
        ]
      }
      ```
    - Solution: 
      - Confirm [active](https://learning.postman.com/docs/sending-requests/managing-environments/#selecting-an-active-environment) environment in Postman.
      - Run `AuthorizeGetToken` request.

1. Azure AD errors
    - Solution:
      - Confirm [active](https://learning.postman.com/docs/sending-requests/managing-environments/#selecting-an-active-environment) environment configuration in Postman.
      - Confirm `resource` variable points to the correct FHIR audience.
      - Confirm use of Postman Windows client vs Browser-based.

1. Valid authentication (JWT) token created but not authorized.
    - Error:
    - Solution:
      - Confirm `JWT` has expected roles by copying the data returned from the `AuthorizeGetToken` request in the `access_token` field. Go to [https://jwt.ms/](https://jwt.ms/) and paste the token value. Confirm the JSON display a collection of expected roles.

        ```json
        {
          "roles": [
            "Writer",
            "DPH",
            "Reader"
          ],
        }
        ````