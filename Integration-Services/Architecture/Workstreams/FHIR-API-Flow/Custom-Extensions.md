[[_TOC_]]

## Overview

Every FHIR resource has the ability to be extended using [extensions](https://www.hl7.org/fhir/defining-extensions.html). These are part of the `extensions` collection. They are defined by a custom [`StructureDefinition`](https://www.hl7.org/fhir/structuredefinition.html) and the values are backed with custom [`ValueSet`](https://www.hl7.org/fhir/valueset.html).

Extensions cannot be queried natively but can be exposed via custom [search parameters](https://docs.microsoft.com/en-us/azure/healthcare-apis/fhir/how-to-do-custom-search).

This system uses the following extensions to further classify some of the FHIR resources and enhance reporting.

> NOTE: The following codeable concepts are samples and have not been created nor defined.

| Resource     	| Purpose          	| Usage                                                    	| Code          	| Display                   	| System        	| Url                                                         	|
|--------------	|------------------	|----------------------------------------------------------	|---------------	|---------------------------	|---------------	|-------------------------------------------------------------	|
| Organization 	| Type             	| Used to classify the organization and filter in reports. 	| ValueSet Code 	| ValueSet Friendly Display 	| ValueSet Guid 	| {{url}}/v4/StructureDefinition/organization-type            	|
| Organization 	| Legal Entity     	| Used to classify the organization and filter in reports. 	| ValueSet Code 	| ValueSet Friendly Display 	| ValueSet Guid 	| {{url}}/v4/StructureDefinition/organization-legalentity     	|
| Organization 	| Billing Provider 	| Used to classify the organization and filter in reports. 	| ValueSet Code 	| ValueSet Friendly Display 	| ValueSet Guid 	| {{url}}/v4/StructureDefinition/organization-billingprovider 	|
|              	|                  	|                                                          	|               	|                           	|               	|                                                             	|


## Organization type extension

TBD

### Organization type structured definition

TBD

### Organization type value set

SAMPLE:
```json
{
	"fullUrl": "https://hclacdmhhidexdevw2-main.fhir.azurehealthcareapis.com/ValueSet/031f3d8b-d466-4e0f-a1d7-13bdc6fa55f2",
	"resource": {
		"resourceType": "ValueSet",
		"id": "031f3d8b-d466-4e0f-a1d7-13bdc6fa55f2",
		"meta": {
			"versionId": "1",
			"lastUpdated": "2022-06-21T21:50:51.415+00:00"
		},
		"url": "urn:uuid:org-type",
		"name": "OrgType",
		"status": "active",
		"description": "Defines the Organization type.",
		"expansion": {
			"identifier": "urn:uuid:bf99fe50-2c2b-41ad-bd63-bee6919810b4",
			"contains": [
				{
					"system": "urn:uuid:org-type",
					"code": "amb",
					"display": "Ambulatory"
				}
			]
		}
	},
	"search": {
		"mode": "match"
	}
}
```