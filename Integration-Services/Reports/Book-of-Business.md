# LACDMH Integration Services

## 1. HIDEX Project


## 1.1 Release Schedule


## 1.2 **Project -- LA County Healthcare Information Data Exchange -- HIDEx -- Priority 1**
* Lead Analyst: Philip Yau
* Developer: Willie Lam

Current Status:

-Team will start work on Sprint 59 activities, which includes 

- Sync data between FHIR store and NTST webservice for DCFS, Public Guardian, and Service History
- resolve NTST Patient Access SF cases
- Resolve NTST HIDEX FHIR Web Services Enhancements SF Cases
- Attach azure storage to web user
- create script to add folders in storage account for HIDEX/MFT providers
- add new wiki for go-anywhere
- provision MFT azure VMs
- automate testing after deployment
- use application insight BAM activities for LOCUS
- build LACDMH HIDEX PSC API test cases
- Da vinci pDex
- update Getquestionnaire output to include top dimension and subsequent child dimensions
- application logs ingestion to SEIM tools
- add required/optional field validation for PSC assessment
- Onboard LE
- update GetQuestionnaire response to include additional items
- Continuously performing analysis and creating user stories and work items
- Work on resource capacity planning in DevOps and Delivery Plans
- Reorganize DevOps backlog for project planning

Current Features In Progress

Risks

## 1.3 **Project -- Patient Access API**
* Lead Analyst: Mohammed Abdulla
* Developer: Tiffany Gaw

##

 - CMS Patient Access Final Rule
 - CalAIM BHQIP 
 - Client Access to the chart

CURRENT STATUS

*Release 1 is currently in progress
- Working with NTST to resolve errors in Patient Access operations - SF Cases CS3517022 and CS2786152. All NTST Patient Access operations are returning successful responses except for minor issues reported in the mentioned SF cases.
- Testing Patient Access operations through DMH FHIR Services. 

NEXT STEP

*Complete development 

*Consent feature

Current Features in Progress

::: query-table 76d6d41d-2502-4254-9344-78148ddfed91
:::

Risks
::: query-table 612cd27b-b482-41de-8df1-fce47670ecfe
:::

## 1.4 **Project -- Provider Directory API**
- CalAIM BHQIP

Current Features in Progress
::: query-table c9aedb3c-df99-4d82-8d48-0a0bcd6a2cdf
:::
Risks
::: query-table 8de19b8e-609a-4750-8bea-884033b14177
:::

## 1.5 **Project -- HIDEX FHIR & Support**

Current Features in Progress
::: query-table 3aab272d-7ab3-4fbf-981a-0ce2a51c4326
:::
Risks
::: query-table 7c02a075-04eb-4332-b854-df4f7e3e7de1




## 2. Maintenance & Operations

## 2.1. Maintenance

## Release Schedule: 


### 2.1.2 SRL Web service
* Lead Analyst: Zak Masud
* Developer:

### Current Status
- Screening Tool Questionnaire and Shool Based Data intake deployed to PRODUCTION on 01/28/205. 
- All backlogged items are marked ready for development and assigned to development team.

### Next Steps
- Complete the work item from the list below:

To Be Completed:
::: query-table a2a8d4b1-a285-4b8e-b137-5789bfd6c2e2
:::

### 2.1.1 CSI Web service
* Lead Analyst: Zak Masud
* Developer: Misikir Kebede


### Current Status

- Latest Release: SR#753909 Initial Psychiatric Data capture modification is live now in Production environment as of 2024-12-17, current version: 202001 R2
- DEV Deployment issue has been resolved. Complete Functional Tests have been performed. 
- Eight work items have failed testing. (See query below)

### Next Steps
- Fix the issues related to the Acceptance Criteria for the Failed work items.

Current REQUIREMENTS In Progress
::: query-table 486cf8fc-eb51-4d3c-9bf0-1eb1983bbb7b
:::
Issues
::: None
:::

### 2.1.2 SRL Web service
* Lead Analyst: Zak Masud
* Developer: Misikir Kebede

### Current Status
- Screening Tool Questionnaire and School Based Data intake deployed to PRODUCTION on 01/28/2025. 
- Screening Tool Business Rules are deployed and testing completed. For some work items all acceptance criteria did not meet. Developer is working on these.

### Next Steps
- Resolve the issues showing below and deploy to TEST, QA and PRODUCTION.

Current Work Items Work-In-Progress:
::: query-table 278b2b2a-01ae-4d9e-9b82-ce28b89715b8
:::

### 2.1.3 Client Web Service (CS)

* Lead Analyst: Mohammed Abdulla
* Developer: 

### Current Status
- A new release being developed to map GetClientSrvHistory operation to NTST's getServiceDetails operation - Release around first Week of December 2025.
- The Latest Client Services release, including all SOGI data elements, is in Production as of  2024-12-17.
### Next Steps
- None

Current Features in Progress
::: query-table 507ae795-fde1-42e9-9412-bbb419bb5c57
:::
Risks
::: query-table 4cf3a176-7e5d-4a3f-ba64-3ada202c8389
:::

### 2.1.4 MDM Web service
* Lead Analyst: Mohammed Abdulla
* Developer:


### CURRENT STATUS:
- A new release being developed to prevent blank and null values from transferring to Access Center Dynamics - Release around first Week of December 2025.
- Three SF cases have been escalated (Priority 2): 
- CS3756862 (Delay in receiving transactions in Dynamics) and SF Case 
- CS3756977 (Multiple Create Client operations for the same Client). NTST made configuration changes and DMH is monitoring traffic.
- CS3767096  POST Encounter operation is returning an error.

- One SF Case (Priority 3):
- CS3762335 (Receiving Create transactions for old Clients) - Working with NTST to resolve this issue.
- Integration Team Deployed MDM to Production environment on 9/17/2025.

- New Project End Date: 2025-12-31


###NEXT STEPS:

###
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
* Lead Analyst: Zak Masud
* Developer:

### Current Status:
- Production file generation and submission working properly. No issue.
- Development on new enhancements based on State's Companion Guide v3.0 has been completed. DMBI loaded sample data and test file is generated.
- Testing completed. Issues reported to State DHCCS. They opened tickets with their IT group. No resolution yet.

### Next Steps:
- Generate a production file for June submission based on May data. 
- Deploy the solution to production.
- Continue on automation process pending tasks.


Current Work Items in Progress
::: query-table 2c444e11-0513-4907-92de-2d4eea1d98e2
:::
Risks
::: None
:::

## 2.2. Operations

## EDI and Web service Onboarding

#onboarding_status_05132025


1. On-Boarding for LE 01806: UMMA Community Clinic
Business configured the program ID 01806 so it can submit the CSI Admission web call. Provider tried and got the error. Nga confirmed it has been configured properly. Asked provider to try the transaction. Provider is still getting error with program id. Scheduling a session with them and their IT vendor to troubleshoot.

2. Change of Vendor: LE 00201: Penny Lane Centers:
Provider stated that they are still working on the programming and implementation with an expected completion date of 6/30. 

3. On-Boarding for LE 02457: Parents Anonymous Inc:
Successfully completed the cs script. All pending items have been re-submitted without anything missing. All good. 

4. Onboarding LE 01048: Pacifica Hospital of the Valley UCC:
Business and Integration met with them on 4/17/25. They understood the need for completing the script. Will reach out to Integration as needed. As of today - no update. Asked them to provide a status.

5. Change of Vendor for LE 00196: Vista Del Mar
Provider is working with Netsmart to finish up various configurations. No ETA yet.



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
Current Trend (August ) : 92 Cases (Open & Closed)



![Untitled.png](/Integration-Services/.attachments/HEATReport.png)
 
Monthly trend for 2025: approx. 80 cases per month 


Tasks Assigned for Integration Team for August in HEAT systems:

| Category|                     No of Tickets |
|  --- | --- |
| 999 | 2 |
| ACCESS | 16 |
| Account Request | 1 |
| Application Down| 2 |
| Application Error| 4|
| Connection Status | 2 |
| Claim Status | 16 |
| Connection Issue | 6 |
| Documentation| 1 |
| Download| 1 |
| EDI Certification| 1 |
| Error | 25 |
| General Questions | 4 |
| How To | 4 |
| Installation Certificate | 10 |
| Member Authorization| 1 |
| Password| 2 |
| PRM Data | 1 |
| Update Request | 1 |
| Website down| 4 |
| **Grand Total** | **92** |

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