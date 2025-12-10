# LACDMH Integration Services

## 1. **PROJECTS**

## 1.1 Project Release Schedule

## 1.2 **Project -- Healthcare Information Data Exchange -- HIDEx -- Priority 1**
* Analyst: Philip Yau
* Developer: Willie Lam

Current Status:

Current Features In Progress

Risks

## 1.2 **Project -- Access Center Modernization Project Integration -- Priority 1**
* Analyst: Philip Yau
* Developer: Willie Lam

![Untitled.png](/Integration-Services/.attachments/ACM_Status.png)

## 1.3 **Project -- LOCUS API**
* Analyst: Zak Masud
* Developer: Tiffany Gaw

Current Features In Progress
- Synapse notebook to load sql db for reporting

Risks
- Onboarding delays due to vendor(s)
- MS ticket

## 1.5  **Provider Access API**
* Analyst: Philip Yau
* Developer: n/a

Current Features In Progress

Risks

## 1.5  **GoAnywhereMFT - Replace Globalscape Electronic File Transfer (EFT)**
* Analyst: Joe Martinez
* Developer: n/a

Current Features In Progress

Risks

## 2. **Maintenance & Operations**

## 2.1. Maintenance

Updates to existing applications.

### 2.1.1 CSI Web service
* Analyst: Zak Masud
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


### 2.1.2 SRL Web service
* Analyst: Zak Masud
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

* Analyst: Mohammed Abdulla
* Developer: Tiffany Gaw

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
* Analyst: Mohammed Abdulla
* Developer: Tiffany Gaw


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


### NEXT STEPS:

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
* Analyst: Zak Masud
* Developer: Willie Lam

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

### 2.1.6 Healthcare Provider Directory (HCPD) FHIR Integration
* Analyst: Zak Masud
* Developer: Willie Lam

Current Work Items in Progress

Risks

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
Current Trend (November ) : 59 Cases (Open & Closed)



![Untitled.png](/Integration-Services/.attachments/HEATReport.png)
 
Monthly trend for 2025: approx. 80 cases per month 


Tasks Assigned for Integration Team for Nov in HEAT systems:

| Category|                     No of Tickets |
|  --- | --- |
| 999 | 2 |
| ACCESS | 11 |
| Account Request | 1 |
| Application Down| 2 |
| Application Error| 1|
| Connection Status | 1 |
| Claim Status | 8 |
| Connection Issue | 5 |
| Documentation| 1 |
| Download| 1 |
| EDI Certification| 1 |
| Error | 11 |
| General Questions | 4 |
| How To | 4 |
| Installation Certificate | 7 |
| Member Authorization| 1 |
| Password| 2 |
| PRM Data | 1 |
| Update Request | 1 |
| Website down| 4 |
| **Grand Total** | **59** |

Salesforce Cases: 
::: query-table f565c801-1c1e-4d4c-afdf-880b63429b27
:::

<div style="page-break-after: always"></div>

# 4. **Special Support** 

## 4.1. In Progress


### 4.1.1 CBO/TTC
- automation on hold due to resource constraints.
- files are decrypted manually when received.

### 4.1.2 CalHHS

## 4.2. **In Queue**

- Payer-to-Payer FHIR endpoint
- Pre-Authorization FHIR service
- Vendor workflow (Disable Avatar lookup in Dev/lower environments)

## 4.3. **In Analysis**

- CalAIM-JI

## 4.4. Approved Projects - Not started**

- SRL Azure migration
- BHSA
- COE

<div style="page-break-after: always"></div>

# 5. On HOLD (Items in this section will remain static until re-activated) 

<div style="page-break-after: always"></div>