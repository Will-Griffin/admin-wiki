[[_TOC_]]

## Overview

![fhir](/Integration%20Services/.attachments/workstream-apis.png)

## System Components

1. FHIR Store - Represents the data layer using Azure Health Data Services FHIR Service.
1. [FHIR Proxy](/Integration%20Services/Architecture/Workstreams/FHIR-API-Flow) - Component used to add custom business logic for requests to the FHIR store
1. [SOAP Proxy](/Integration%20Services/Architecture/Workstreams/SOAP-Flow) - Component used for backwards compatibility for DMH Client Services used to send SOAP based messages to the REST based FHIR API.
1. [EDI X12](/Integration%20Services/Architecture/Workstreams/X12-Claim-Flow) - Component used for processing EDI x12 messages. Uses Azure Logic Apps.
1. API Gateway - Uses Azure API Management to expose all APIs to external consumers.
1. Reporting - Uses Azure Synapse and PowerBI for reporting.
