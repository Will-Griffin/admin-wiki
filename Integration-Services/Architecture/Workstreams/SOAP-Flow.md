[[_TOC_]]

## Overview

The SOAP workstream supports existing DMH providers that integrate with the LA County Client Services. This approach abstracts the new FHIR-based architecture for those existing consumers.

![soap](/Integration%20Services/Integration%20Services/.attachments/workstream-soap-dotnet.png)

## Design considerations

- Provide backwards compatibility for SOAP messages and responses to existing providers.
- Continue to use the existing X.509 client certificate authentication for existing SOAP-based providers.
- Providers to not supply identifiers with messages other than the certificate.

## Design recommendations

- Migrate to [CoreWCF](https://github.com/CoreWCF/CoreWCF) in order to modernize WCF hosting
- Create a SOAP Facade that will map incoming SOAP calls to FHIR requests and send them to the FHIR proxy.
- Move all business logic and requirements around processing the request to the FHIR proxy. This allows for centralizing logic for both SOAP and FHIR clients.
- Only manage code to map incoming SOAP to FHIR and FHIR to SOAP in the new WCF SOAP Facade service.
- Providers shall be represented as a FHIR organization resource.
- SOAP certificate thumbprint shall be mapped to the FHIR organization resource via the identifier collection.

## Components

1. [SOAP Proxy](https://dev.azure.com/LACDMH-DPH-Integration/HIDEX/_git/hidex-soap-proxy?version=GBmain&_a=preview&path=/README.md)
2. API Gateway
3. [FHIR Proxy](https://dev.azure.com/LACDMH-DPH-Integration/HIDEX/_git/hidex-fhir-proxy?path=/README.md&_a=preview)

## SOAP Request Flow

This flow shows the interaction between the actors required to process a SOAP request and return data from the FHIR store.

::: mermaid
sequenceDiagram
    participant P as Provider
    participant S as SOAP Proxy
    participant A as APIM
    Note right of A: Store RAW Message
    participant FP as FHIR Proxy
    participant H as FHIR Store
    P->>+S: AdmitNewClient
    S->>+A: Send FHIR Request
    A->>+FP: Validate Request
    FP->>+H: Commit Bundle
    H-->>-FP: FHIR Response
    FP-->>-A: FHIR Response
    A-->>-S: FHIR Response
    S-->>-P: SOAP Response    
:::       

## SOAP Proxy Command Pattern

This flow shows the interaction between the components inside the SOAP Facade. 

::: mermaid
sequenceDiagram
    participant S as SOAP Host
    participant C as Admit Command
    participant B as Bundle Service
    participant F as FHIR Client
    participant H as FHIR Store
    S->>+C: AdmitNewClient
    C->>C: Map to FHIR
    C->>+B: Generate Bundle
    B-->>-C: JSON Bundle
    C->>+F: Construct FHIR Request
    F->>+H: Submit FHIR Bundle
    H-->>-F: FHIR Response
    F-->>-C: FHIR Response
    C->>C: Map to SOAP
    C-->>-S: SOAP Response 
:::   


## Security

Several levels of security are applied to the SOAP Proxy:

1. Transport security - SSL is used to secure the transport channel
2. FHIR RBAC - The SOAP Proxy acts on-behalf of the provider when submitting requests to the FHIR store. The SOAP proxy requires its own Azure Active Directory [Application Registration](https://dev.azure.com/LACDMH-DPH-Integration/HIDEX/_wiki/wikis/Wiki/22/Authentication) with `DMH` consent.
3. Provider Identity - The provider uses a certificate assigned to them to communicate with the SOAP Proxy. The `thumbprint` of this certificate will be mapped to the FHIR `Organization` resource that represents the provider. This will be used to load the identity context of the FHIR request along with populating any references in FHIR resources such as `managingOrganization` in the `Patient` resource.

### Transport Security

[CoreWCF](https://devblogs.microsoft.com/dotnet/corewcf-v1-released/#features) supports both BasicHttp and WSHttp Transport level security.

WCF Configuration:
```cs
app.UseServiceModel(builder =>
{
    builder.AddService<ClientService>()
    .AddServiceEndpoint<ClientService, ClientServiceInterface>(new BasicHttpBinding(BasicHttpSecurityMode.Transport), "/ClientService/basichttp")
    // Add a WSHttpBinding with Transport Security for TLS
    .AddServiceEndpoint<ClientService, ClientServiceInterface>(new WSHttpBinding(SecurityMode.Transport), "/ClientService/WSHttps")
    .ConfigureServiceHostBase<ClientService(serviceHost =>
    {
        serviceHost.Credentials.ServiceCertificate.SetCertificate(
                    StoreLocation.LocalMachine,
                    StoreName.My,
                    X509FindType.FindByIssuerName,
                    "MY ISSUING CA");
            });
});
```

### Service Impersonation

SOAP Proxy requires an AAD [Application Registration](https://dev.azure.com/LACDMH-DPH-Integration/HIDEX/_wiki/wikis/Wiki/22/Authentication) including the consent to the `DMH` FHIR API App Registration.

The application registration data is configured in `appsettings.{env}.json` in order to allow the SOAP Proxy to request an OAuth token in order to send requests to the FHIR API.
```json
"FhirClient": {
    "Url": "https://apim-lac-hidex-dev-w2.azure-api.net/healthcare",
    "ApimAuthKey": "...",
    "Authority": "https://login.microsoftonline.com",
    "TenantName": "...",
    "Audience": "api://.../.default",
    "ClientId": "...",
    "ClientSecret": "..."
  }
```

### Provider Identity

Messages sent by the provider does not collect details about the provider themselves. This identity context will be loaded from mapping the `thumbprint` of the certificate to the FHIR Organization resource that represents them via the `identifier` property.

#### FHIR Organization Configuration:

```json
{
	"identifier": [
		{
			"use": "official",
			"type": {
				"coding": [
					{
						"system": "http://dmh.lacounty.gov/hidex/org-identifiers",
						"code": "SOAPCert",
						"display": "SOAP Certificate Thumbprint"
					}
				]
			},
			"system": "http://dmh.lacounty.gov/hidex/1234",
			"value": "{thumbprint}",
			"period": {
				"start": "2022-06-07",
				"end": "2024-06-07"
			}
		}
	]
}
```

#### Querying for organization using thumbprint

Use the thumbprint and the extension (ValueSet) system url to query for the organization FHIR resource.

```
GET [base]/Organization?identifier=http://dmh.lacounty.gov/hidex/1234|{thumbprint}
```

#### Referencing organization in FHIR resources

Option \#1:

- Query for organization using identifier
- Extract the organization resource ID.
- Set the `ResourceReference` with the id.

This approach allows one to validate the thumbprint to organization mapping potentially in the mediator pipeline. A scoped singleton context can be used to track this context and injected into mappers or command handlers.

.NET Reference:
```cs
new ResourceReference($"Organization/123456")
```

Request Context Flow:
::: mermaid
sequenceDiagram
    participant M as Mediator
    participant P as RequestContext Pipeline
    participant S as AuthService
    participant F as FHIR Client
    participant H as FHIR Store
    participant C as Command Handler
    M->>+P: Dispatch Command
    P->>+S: Create Context
    S->>+F: Send Query
    F->>+H: GET /Organization
    H-->>-F: Org Details
    F-->>-S: response
    S-->>-P: context
    P->>+C: Handle Command
    C-->>-P: SOAP Response
    P-->>-M: Command Results
:::   

Option \#2:

The resource reference can be associated using the identifier syntax. This will enforce that the organization must exist before the FHIR resource is committed to the store. An `OperationOutcome` will be returned with the error messages and must be parsed accordingly.

```cs
new ResourceReference($"Organization?identifier=http://dmh.lacounty.gov/hidex/1234|{thumbprint}")
```
