## Overview[]()

The page describes the steps required to create an App Registration for Providers in Azure AD in an automated fashion using an existing bash script/Azure CLI

Note: This approach is to be utilized as an interim option till Provider Onboarding features are built-in as an out-of-the-box offering in the HIDEX platfrom.

## Reference

[[Authentication](/Architecture/Identity-&-Access-Management/Authentication)] ** see **Providers** section

## Usage

- Pre-requisite steps: 
1. Ensure Azure CLI is installed - see [here](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) for instructions 
2. Ensure that the jq json parser utility is installed and the executable is set in your PATH - see [here](https://stedolan.github.io/jq/download/) for download<br/><br>Shortcut command from Git Bash/Windows: <br/> 
`curl -L -o /usr/bin/jq.exe https://github.com/stedolan/jq/releases/latest/download/jq-win64.exe`  
         
- Checkout [hidex-shared-infrastructure](http://https://dev.azure.com/LACDMH-DPH-Integration/HIDEX/_git/hidex-infrastructure-shared) repo and navigate to the 'scripts' folder

- The App Registration script requires the following 3 param inputs. Ensure that you have these values ready -

| Param Name | Key | Values |
|--|--|--|
| tenantId | -t | Azure AD Tenant ID - see [here](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)|
| department | -d | DPH or DMH |
| appName | -a | This follows the pattern HIDEX-PROVIDER-{DMH or DPH}-{DEV or QA or PROD}-{alphanumeric min1 max7}. <br/><br/>Examples -> <br/>HIDEX-PROVIDER-DMH-DEV-0<br/>HIDEX-PROVIDER-DPH-QA-100<br/>HIDEX-PROVIDER-DMH-PROD-1234MOC|

- Run script 
          
      ./registerProviderApp.sh -t <tenantId> -d <department> -a <appName>

- If an existing Azure CLI session is not in place you will be prompted to login. You can login using the following command 
          
      az login


- If the app registration was successful then the following message will be displayed. Save the client secret for later usage as this value will not be retrievable later.


```
-----------------SAVE CREDENTIALS-------------------    
      CLIENT_ID=<<client_id>>  
      CLIENT_PWD=<<client_secret>>           
----------------------------------------------------
completed app registration successfully
```


- Verify the newly create App Registraiton on the Azure Management portal - https://portal.azure.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade

![image.png](/Integration-Services/.attachments/image-e1b84520-40db-45aa-833e-f325e5ed5dc8.png)

- The step to add 'API Permissions' to the newly created App Registration is not automated and needs to be done manually based on the permissions required for the provider. At a minimum the departmental (DMH vs DPH), Reader and Writer permissions will need to be set. To perform this step navigate to the 'API Permissions' -> Add Permissions -> Select an API -> APIs my organization uses -> Search Criteria (HIDEX-FHIR-{Department}-{Environment}) -> Select specific permissions 

![image.png](/Integration-Services/.attachments/image-fdebd03f-c5f1-4628-af6f-1490ebd0985c.png)
