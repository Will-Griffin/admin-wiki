[[_TOC_]]

## Overview

Application roles will be used to grant both user and application member types access to various system components.

## FHIR Proxy Roles

The following roles will be exposed by the FHIR Proxy and used to grant access to end users or applications.

| Role          	| Description                                            	| User 	| Application 	|
|---------------	|--------------------------------------------------------	|------	|-------------	|
| Organization  	| Managing Organization of the FHIR Server               	| x    	| x           	|
| Writer        	| Writer of the FHIR Server                              	| x    	| x           	|
| Reader        	| Reader of the FHIR Server                              	| x    	| x           	|
| DataScientist 	| DataScientist Role with de-id access to all resources. 	| x    	|             	|
| RelatedPerson 	| RelatedPerson Access to FHIR resources                 	| x    	|             	|
| Patient       	| Patient Access to FHIR resources                       	| x    	|             	|
| Practitioner  	| Practitioner Access to FHIR resources                  	| x    	| x           	|
| Administrator 	| Administrator of the FHIR Server                       	| x    	|             	|

### Managing Organization Role

This role is used to represent the County of Los Angeles managing department such as DPH or DMH. When creating the FHIR proxy application registration for a specific FHIR store, this application role will use one of the following possible values depending on the department:

1. DMH - Allows access to DMH FHIR store
2. DPH - Allow access to DPH FHIR store

## Azure Active Directory Role Manifest

[FHIR Roles](https://dev.azure.com/LACDMH-DPH-Integration/HIDEX/_git/hidex-infrastructure-shared?path=/scripts/fhirroles.json) are can be imported into the application registration via the manifest.