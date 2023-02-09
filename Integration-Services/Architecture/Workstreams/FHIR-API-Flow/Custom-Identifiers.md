[[_TOC_]]

## Overview

Custom [identifiers](https://www.hl7.org/fhir/datatypes.html#identifier) are required to store additional metadata about the resource and uniquely search for it. These additional attributes about the resource are stored in the `Identifier` property of the resource.

Each identifier consists of a system and value along with an optional codeable concept. The `system` is a URI that defines a set of identifiers (i.e. how the value is made unique). It might be a specific application or a recognized standard/specification for a set of identifiers or a way of making identifiers unique. FHIR defines some useful or important system URIs directly.

The following are suggested custom identifiers to add which will allow correlating the FHIR resource to other processes such as Netsmart integration or EDI X12.

> NOTE : The custom system http://lacount.gov/fhir/sid/{type} is being used. This can be an URN with an OID or a URL that should resolve. The team will need to define this.

| Resource     	| Value                       	| Usage                                                                                                                           	| System                            	| CodingSystem                                  	| CodingCode 	| CodingDisplay                	|
|--------------	|-----------------------------	|---------------------------------------------------------------------------------------------------------------------------------	|-----------------------------------	|-----------------------------------------------	|------------	|------------------------------	|
| Patient      	| Social Security Number      	|                                                                                                                                 	| http://hl7.org/fhir/sid/us-ssn    	| http://terminology.hl7.org/CodeSystem/v2-0203 	| SS         	| Social Security number       	|
| Patient      	| Medical Record Number       	| Used to associate patient to Netsmart and EDI                                                                                   	| http://netsmart.com/fhir/sid/mrn  	| http://terminology.hl7.org/CodeSystem/v2-0203 	| MR         	| Medical record number        	|
| Organization 	| EDI DUNNS                   	| Used to query for organization during EDI claim processing.                                                                     	| http://lacounty.gov/fhir/sid/edi  	| N/A                                           	| N/A        	| N/A                          	|
| Organization 	| SOAP certificate thumbprint 	| Used to query for organization during SOAP processing. Allow one to take the SOAP thumbprint and convert it to a FHIR resource. 	| http://lacounty.gov/fhir/sid/soap 	| N/A                                           	| N/A        	| N/A                          	|
| Practitioner 	| NPI                         	| Used to query for doctor during SOAP and EDI processing.                                                                        	| http://lacounty.gov/fhir/sid/npi  	| http://terminology.hl7.org/CodeSystem/v2-0203 	| NPI        	| National provider identifier 	|
| Claim        	| Payer claim control number  	| Used to associate claims during EDI processing.                                                                                 	| http://lacount.gov/fhir/sid/clp07 	| N/A                                           	| N/A        	| N/A                          	|

## Querying for resource using identifier

The [identifier](https://www.hl7.org/fhir/search.html#token) field can be used to search as a token. There are various syntaxes that can be used and the recommended approach is `[parameter]=[system]|[code]`.

- Format: {{fhirurl}}/{ResourceType}?identifier={System}|{Value}
- Sample: `{{fhirurl}}/Organization?identifier=http://lacounty.gov/fhir/sid/soap|7a7981a3873eb71cc5c93c8c0d3317722de5a7b7`