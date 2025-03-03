# LACDMH Integration Services 

# 2. Maintenance & Operations 

## 2.1. Maintenance

## Release Schedule: 
![image.png](/.attachments/image-333f5978-e1e5-4028-a12b-1cb5579c7ece.png)

### 2.1.1 CSI Web service
### Current Status
- SR#753909 Initial Psychiatric Data capture modification is live now in Production environment as of 2024-12-17
- Updated Companion Guide, Release Notes, WSDL published, all LEs have been notified
- GetCall date format issue is being fixed
- BRE policy to apply business rules for Initial Med Evaluation data is being developed
- SR#748178 SRTS validation being developed

### Next Steps
- Deploy SRTS validation, fix for the issue and BRE policy validations in the API.

Current Features In Progress
::: query-table 94c595b1-c57c-4f04-aff2-7b3e87915794
:::
Issues
::: query-table 486cf8fc-eb51-4d3c-9bf0-1eb1983bbb7b
:::

### 2.1.2 SRL Web service
### Current Status
- Screening Tool Questionnaire and Shool Based Data intake deployed to PRODUCTION on 01/28/205. 

### Next Steps
- Complete the work item from the list below:

To Be Completed:
::: query-table a2a8d4b1-a285-4b8e-b137-5789bfd6c2e2
:::


### 2.1.3 Client Web Service (CS)
### Current Status
- The Latest Client Services release, including all SOGI data elements, is in Production.
### Next Steps
- None

Current Features in Progress
::: query-table 507ae795-fde1-42e9-9412-bbb419bb5c57
:::
Risks
::: query-table 4cf3a176-7e5d-4a3f-ba64-3ada202c8389
:::

### 2.1.4 MDM Web service
### CURRENT STATUS:
- Testing with Access Center dev team and ISD is in progress.
- ISD security software is blocking authentication for Access Center update.
- Access Center project is on pause pending SOW issues.
- Netsmart released Avatar Cal-PM 2024 Update 54 (for returning data elements in getClientDetails operation). This relates to required MDM changes.

###NEXT STEPS:
- SOGI, Race, and Ethnicity data elements are being received now from the Create Client and Update Client transactions SF Case CS3317075. There is an issue with Race - We are not receiving multiple values for Race. NTST is working on this issue. 
- MDM is now receiving Client Merge transactions for post-merge clients in LA DEV. SF Case CS3317024. GetClient By ID operation in FHIR is not returning Non-Surviving ID in the Output of the Surviving ID response. 
We met with NTST on Monday 2/3/2025 to discuss remaining issues. We do not have an ETA on a resolution to these issues. Regarding the "An error has occurred" message BizTalk is returning to NTST, we are actively investigating the issue and working on a solution.


- Resolve authentication issue with ISD.
- Dev and testing as needed based on Netsmart changes.
- Test and confirm the solution works with Access Center integration.
- Promote/schedule build deployment to upper environments.


Current Features In Progress
::: query-table 73965f26-c347-4258-a446-2c1da512122d
:::
Issues/Risks
::: query-table db4f3db4-fc4b-4331-b395-2081ea045960
:::

### 2.1.5 Healthcare Provider Directory (HCPD) EDI274 Integration
### Current Status:
- Monthly file processing as scheduled, no issues to report.
- Automation configuration work is in-progress. State DHCS is working on providing a system account and it's related rights and other criteria.
- New work items have been created for DHCS Companion Guide v3.0 changes. DMBI will modify the source data to meet the state's requirements. Integration team will work on the items that needs edits in mapping and cardinalities.

### Next Steps:
- Start DHCS_CG_v3_Enhancements Iteration Sprint 1 from 2/18/2025

Current Work Items in Progress
::: query-table 2c444e11-0513-4907-92de-2d4eea1d98e2
:::
Risks
::: None
:::

## 2.2. Operations

## EDI and Web service Onboarding

## 2.2.1. LE Onboarding Status 
Closed = onboarding process completed and no issue reported

Active = not yet onboarded. check work item comment for current status
::: query-table 2852a12e-3db1-4eb0-aceb-53cac84ab415
:::

## 2.2.2. FFS Onboarding Status
Closed = onboarding process completed and no issue reported

Active = not yet onboarded. check work item comment for current status
::: query-table 50781838-8e69-47b6-95d1-6446f82d8999
:::

## 2.2.3. EDI File Archiving
::: query-table d9a33d74-b6ce-4094-83b1-4df41ed635de
:::


## 2.2.3 BizTalk Server maintenance
On-premises Server administration and maintenance:
::: query-table 7daee816-1f8e-4b96-9efd-7780b3435224
:::

## 2.2.4 EFT/MFT Administration
All non-HIDEX administration operations: 
::: query-table 3e5ab2b5-2334-4c98-97b1-467ca65d30a7
:::
GoAnywhere Implementation tracked as part of HIDEX.

## 2.2.5 Azure Cloud Administration
All non-HIDEX administration operations:
::: query-table 5d1c6cff-6056-4d90-bdda-f6144c36dad8
:::

## 2.2.6 DevSecOps Services
All non-HIDEX Security, Infrastructure, and DevOps service related operations in progress:
::: query-table 2996c28d-a4e6-46db-909d-728d3851e4bf
:::

<div style="page-break-after: always"></div>


## 2.2.7 ECM/MHP
### ECM/MHP Onboarding:

*   LACare currently has issue with SFTP disconnect.
*   BlueShield is in process of onboarding.


Current Features in Progress
::: query-table b4b5b9ad-e5b6-4007-bc27-5a8ea1205510
:::

# 3. Help Desk Tickets
Current Trend (Jan 1st - Current) : 93 Cases (Open & Closed)

**Weekly trend for February is approximately 84 cases.**

![Untitled.png](/Integration-Services/.attachments/HEATReport.png)
 
Monthly trend for 2024: approx. 80 cases per month 


Tasks Assigned for Integration Team for August in HEAT systems:

| Category|                     No of Tickets |
|  --- | --- |
| 999 | 2 |
| ACCESS | 18 |
| Account Request | 1 |
| Application Error | 2 |
| Certificate Status | 2 |
| Claim Status | 24 |
| Connection Issue | 3 |
| Documentation | 1 |
| Error| 18 |
| Generation Questions | 8 |
| How To| 1 |
| Installation Certificate | 2 |
| Login Issues | 1 |
| Payment | 1 |
| Processed | 1 |
| Update Request | 2 |
| **Grand Total** | **87** |

Salesforce Cases: 
::: query-table f565c801-1c1e-4d4c-afdf-880b63429b27
:::

<div style="page-break-after: always"></div>

# 4. Special Support 

## 4.1. In Progress


### 4.1.1 CBO/TTC
- automation on hold due to resource constraints.
- files are decrypted manually when received.
### 4.1.2 CalHHS
## 4.2. In Queue**

## 4.3. In Analysis**
###CalAIM-JI
## 4.4. Approved Projects - Not started**

None at this time.

<div style="page-break-after: always"></div>

# 5. On HOLD (Items in this section will remain static until re-activated) 

<div style="page-break-after: always"></div>