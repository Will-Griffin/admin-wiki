[[_TOC_]]

## Overview

This document outlines information about provisioning a new HIDEX environment.

## Components

Resources are grouped into high-level components and assigned a corresponding Azure [resource group](/Architecture/Resource-Organization/Resource-Groups).

1. Infrastructure As Code
    1. Shared Infrastructure
        - Azure API Management
        - Azure Log Analytics
        - Azure FunctionApp - FHIR Proxy
        - Azure Application Insights - FHIR Proxy
        - Azure Storage Account - FHIR Proxy
        - Azure App Service Plan - FHIR Proxy
    1. DMH Infrastructure
        - Azure Health Data Services Workspace
        - Azure Health Data Services FHIR Service
        - Azure FunctionApp - SOAP Proxy
        - Azure Application Insights - SOAP Proxy
        - Azure App Service Plan - SOAP Proxy
    1. DPH Infrastructure
        - Azure Health Data Services Workspace
        - Azure Health Data Services FHIR Service
    1. EDI Infrastructure
        - Azure FunctionApp - Logic Flows
        - Azure Application Insights - Logic Flows
        - Azure Storage Account - Logic Flows
        - Azure App Service Plan - Logic Flows
        - Azure Storage Account - SFTP
        - Azure Storage Account - SFTP Backup
        - Azure Event Grid - Logic Flows
1. Pipelines
    1. Infrastructure
        - hidex-infrastructure-shared-ci
        - hidex-infrastructure-dph-ci
        - hidex-infrastructure-dph-ci
        - hidex-infrastructure-edi-ci
        - hidex-infrastructure-dmh-soap-ci
    1. Application
        - hidex-fhir-proxy-ci
        - hidex-edi-proxy-ci
        - hidex-soap-proxy-ci
## Azure Setup

1. Azure Subscription has been created for shared and department specific resources.
1. Azure Service Principal has `CustomRoleforDMHService` in the subscription it will deploy to.
1. Azure Service Principal has `Log Analytics Contributor` in the subscription where Azure Log Analytics service is deployed to.
1. An Azure Active Directory application registration has been setup for each department specific Azure Health Data Services FHIR Service in order to meet [authentication](https://dev.azure.com/LACDMH-DPH-Integration/HIDEX/_wiki/wikis/Wiki/22/Authentication) requirements.
1. Azure DevOps pipeline environments are setup and RBAC and approvals configured.
1. Azure DevOps pipeline ARM parameter file has been configured.
    - [`/solution/{component}/main.parameters.{env}.json`](https://dev.azure.com/LACDMH-DPH-Integration/HIDEX/_git/hidex-infrastructure-shared?path=/solution/shared/main.parameters.dev.json)    
1. Azure DevOps pipeline environment variable file has been configured.
    - [`/pipelines/vars/{component}/vars-{env}.yaml`](https://dev.azure.com/LACDMH-DPH-Integration/HIDEX/_git/hidex-infrastructure-shared?path=/pipelines/vars/shared/vars-dev.yaml)
1. Azure DevOps pipeline environment list has been updated.
1. NetSmart integration configuration is added to Azure KeyVault for the corresponding environment and accessible from Azure DevOps Pipeline.

## Deployment Order

::: mermaid
graph TD
Start[AzureSetup] -->|Manual| A(hidex-infrastructure-dmh-ci)
A[hidex-infrastructure-shared-ci] -->|Deploy| B(hidex-infrastructure-dmh-ci)
A --> |Deploy| C(hidex-infrastructure-dph-ci)
A --> |Manual| FhirProxyAuth(Configure FHIR Proxy Auth)
C -->|Deploy| D[rest of infra]
B -->|Deploy| D(rest of infra)
FhirProxyAuth -->|Deploy| D(rest of infra)
D -->|Deploy| E(hidex-infrastructure-edi-ci)
D -->|Deploy| F(hidex-infrastructure-soap-proxy-ci)
E -->|Deploy| G[apps]
F -->|Deploy| G(apps)
G -->|Deploy| H(hidex-fhir-proxy-ci)
G -->|Deploy| I(hidex-edi-proxy-ci)
G -->|Deploy| J(hidex-soap-proxy-ci)
:::

## Troubleshooting

1. Deployment of shared infrastructure fails when creating the backend in API Management for FHIR Proxy.

    This is an intermittent issue that has not been resolved. Re-running the pipeline fixes the issue though sometimes it must be run multiple times. The issue occurs when the backend is being configured in API Management to point to the FHIR Proxy FunctionApp. Extracting the FunctionApp code fails because the FunctionApp server is not ready.

    Steps to resolve:
    - Try to re-run the pipeline. Sometimes this must be done multiple times and/or try the next step as well.
    - After the FunctionApp is deployed while the pipeline is running, enter the FunctionApp via Azure Portal and view configuration screen and then the listing of functions. This seems to "wake" up the FunctionApp. Try to access the keys.

2. Deployment of shared infrastructure fails when setting up diagnostics between department specific resource and Log Analytics.

    This occurs when the Azure Service Principal used to deploy only has access to the department specific resource. It also needs `Log Analytics Contributor` in the shared infrastructure subscription where Log Analytics resides.

    Error: 
    ```json
    {
        "code": "DeploymentFailed",
        "message": "At least one resource deployment operation failed. Please list deployment operations for details. Please see https://aka.ms/DeployOperations for usage details.",
        "details": [
            {
                "code": "LinkedAuthorizationFailed",
                "message": "The client '6de080ac-afb1-418b-a252-5cef559250bb' with object id '6de080ac-afb1-418b-a252-5cef559250bb' has permission to perform action 'Microsoft.Insights/diagnosticSettings/write' on scope '/subscriptions/e0cb0d2f-6d86-41a0-80ba-42e38c9eee2d/resourcegroups/rg-LACDPH-HIDEX-qa/providers/Microsoft.HealthcareApis/workspaces/hclacdphhidexqaw2/fhirservices/main/providers/Microsoft.Insights/diagnosticSettings/diagnosticSettings'; however, it does not have permission to perform action 'Microsoft.OperationalInsights/workspaces/sharedKeys/action' on the linked scope(s) '/subscriptions/965126b9-a5ce-4974-b238-7edaab03e70a/resourceGroups/rg-lac-hidex-shared-qa/providers/Microsoft.OperationalInsights/workspaces/log-lac-hidex-qa-w2' or the linked scope(s) are invalid."
            }
        ]
   }
   ```

    Steps to resolve:
    - Grant the `Log Analytics Contributor` Azure RBAC role to the Azure Service Principal running deployment in the subscription where Azure Log Analytics resides.
