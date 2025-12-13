# LACDMH Integration Services

## 1. **PROJECTS**

## 1.1 Project Release Schedule

![image.png](/.attachments/image-4e2a4fb4-8e65-4368-9b9a-01993d82c098.png)

## 1.2 **Project -- Access Center Modernization (ACM) Project Integration -- Priority 1**
All HIDEX FHIR operations and data processes required by the Access Center Modernization project. 
* Project URL: 
* Planview URL:
* Analyst: Philip Yau
* Developer: Willie Lam, Tiffany Gaw
* DevOps: Thaer Rumaneh, Charlie Wang
### Current Features in Progress

![image.png](/.attachments/image-d010c3f3-5f9f-49da-8302-c9a1d14ecb8c.png)
### Risks
- Booking issues with the UI
- Data synchronizing issues
### Current Status
- ETA for update 12/23/2025
### Next Steps
- Resolve outstanding issues, coordinate with AppDev and Microsoft team.

## 1.3 **Project -- LOCUS API**
* Project URL: https://lacdmh-integrationservices.visualstudio.com/LOCUS
* Planview URL: [Click here](https://lacdmh.ppmpro.com/home.pa#%5BT5%5DT%2Fdyn%2Fproject%2FprojectInfo.pa%3Fx%3D1765581299525%26projectid%3D16584500245)
* Analyst: Zak Masud
* Developer: Tiffany Gaw
### Current Features In Progress

  - [Issues · LACDMH-Integration/LOCUS](https://github.com/LACDMH-Integration/LOCUS/issues)
### Risks
  - None
### Current Status
- Completed Synapse notebook to load sql db for reporting for Business Stakeholders to review LOCUS data
- Met with Business team to review the sql data load and took notes for new enhancements. See current features in progress.
### Next Steps
- Complete the work items in GitHub.

## 1.4  **Project -- Provider Access API**
* Project URL: 
* Planview URL:
* Analyst: Philip Yau
* Developer: Willie Lam
* DevOps: Charlie Wang
### Current Features In Progress
### Risks
### Current Status
### Next Steps

## 1.5  **Project -- GoAnywhereMFT - Replace Globalscape Electronic File Transfer (EFT)**
* Project URL: 
* Planview URL:
* Analyst: Joe Martinez
### Current Features In Progress
### Risks
### Current Status
### Next Steps

## 2. **Maintenance & Operations**

## 2.1. Maintenance

Updates to existing applications and processes.

## **2.1.1 CSI Web service**
* Project URL: https://lacdmh-integrationservices.visualstudio.com/CSI
* Planview URL: <None Found>
* Analyst: Zak Masud
* Developer: Misikir Kebede
### Current Features In Progress
::: query-table 486cf8fc-eb51-4d3c-9bf0-1eb1983bbb7b
:::
### Risks
None
### Current Status

- New Development for SRTSID validation feature, Treatment Appointment First Date omit with respective closure reasons, other business rules are deployed to DEV, TST, QA environments on 12/08/2025 and 12/11/2025 respectively. Providers are notified through GovDelivery Bulletin on 12/11/2025. 

- Last Release for Production: SR#753909 Initial Psychiatric Data capture modification is live now in Production environment as of 2024-12-17, current version: 202001 R2
### Next Steps
- Promote the changes from QA to PRODUCTION environment on 12/16/2025.

## **2.1.2 SRL Web service**
* Project URL: https://lacdmh-integrationservices.visualstudio.com/SRL
* Planview URL: <None Found>
* Analyst: Zak Masud
* Developer: Misikir Kebede
### Current Features In Progress
::: query-table acd79995-55fd-49fc-8ce3-f9e0a20619bf
:::
### Risks
::: query-table 278b2b2a-01ae-4d9e-9b82-ce28b89715b8
:::
### Current Status
- Screening Tool Questionnaire and School Based Data intake deployed to PRODUCTION on 01/28/2025. 
- Screening Tool Business Rules are deployed to DEV and testing completed. For some work items all acceptance criteria did not meet. Developer is working on these.
### Next Steps
- Resolve the issues with the acceptance criteria showing above under Risks section.
- Deploy the fix in DEV by 12/23/2025, test and eventually deploy to TEST, QA and PRODUCTION upon successful testing by 12/30/2025.

## **2.1.3 Client Web Service (CS)**
* Project URL: https://lacdmh-integrationservices.visualstudio.com/CS
* Planview URL: None found
* Analyst: Mohammed Abdulla
* Developer: Tiffany Gaw
### Current Features in Progress
::: query-table 7b4991cb-2690-4139-a459-ef483164c1a5
:::
### Risks
::: None
:::
### Current Status
- A new release being developed to map GetClientSrvHistory operation to NTST's getServiceDetails operation - Release around first Week of December 2025.
- The Latest Client Services release, including all SOGI data elements, is in Production as of  2024-12-17.
### Next Steps
- Roll out Service History mapping change to DEV, TST, QA and PRODUCTION according to release schedule.

## **2.1.4 MDM Web service**
* Project URL: 
* Planview URL:
* Analyst: Mohammed Abdulla
* Developer: Tiffany Gaw
### Current Features In Progress
::: query-table 73965f26-c347-4258-a446-2c1da512122d
:::
### Issues/Risks
::: query-table db4f3db4-fc4b-4331-b395-2081ea045960
:::
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

## **2.1.5 Healthcare Provider Directory (HCPD) EDI274 Integration**
* Analyst: Zak Masud
* Developer: Willie Lam

### Current Status:
- Production file generation and submission working properly. No issue.
- Development on new enhancements based on State's Companion Guide v3.0 has been completed. DMBI loaded sample data and test file is generated.
- Testing completed. Issues reported to State DHCCS. They opened tickets with their IT group. No resolution yet.
### Risks
### Next Steps:
- Generate a production file for June submission based on May data. 
- Deploy the solution to production.
- Continue on automation process pending tasks.


### Current Work Items in Progress
::: query-table 2c444e11-0513-4907-92de-2d4eea1d98e2
:::



## **2.1.6 Provider Directory API**
* Project URL: [HIDEX/Provider Directory API](https://lacdmh-integrationservices.visualstudio.com/HIDEX/_backlogs/backlog/HIDEX%20Team/Epics?workitem=29233)
* Planview URL: None found
* Analyst: Zak Masud
* Developer: Willie Lam
### Current Features In Progress
None
### Risks
None
### Current Status
-Monthly data load is done by DMBI to comply with State DHCS mandate.
### Next Steps
-None

## **2.1.6 Patient Access API**
* Project URL: 
* Planview URL:
* Analyst: Mohammed Abdulla
* Developer: Willie Lam
### Current Features In Progress
### Risks
### Current Status
### Next Steps

## **2.1.7 Healthcare Information Data Exchange (HIDEX)**
* Project URL: 
* Planview URL:
* Analyst: Philip Yau
* Developer: Willie Lam
* DevOps: Charlie Wang, Joe Martinez
### Current Features In Progress
### Risks
### Current Status
### Next Steps

## 2.2. Operations

## **2.2.1 Onboarding**

### Current Status

BizTalk - Client Web Services API 
onboarding_status_1209_2025

- Change of Vendor for LE 00196: Vista Del Mar:
Provider asked for test clients. Explained to them they need to create clients for testing in QA environment. Referred them to cs script and provided a copy.

- On-Boarding for LE 01806: UMMA Community Clinic:
As of 12/5/2025 Friday - provider did not provide an update. Sent email asking for an update. Previously they reported on 11/18/25 their connection issue is resolved. 

- On-Boarding for LE 02470: GHC of MLK:
As of 10/14/25, provider was still working on test claims. Asked them to provide an update once cs development is completed.

- On-Boarding for LE 02394: MLK Jr-BHC DBA Alpine Special Treatment:
Provider is having Program of Admission error. Asked business to confirm what Program of Admission code is tied to provider's LE 02394. 

- Onboarding LE 01048: Pacifica Hospital of the Valley UCC:
Business had two values for LE number. Nga cleared it out. After confirmation - Integration added 19JUX as the Program Of Service code and 19JU as the Provider Number for LE 01048. Dictionary Service script is getting updated. Pull Requests are created in shared site. It is supposed to be applied to DEV environment thru TEST/QA/PROD on 12/8/2025. Once completed - provider/vendor will be notified.

- On-Boarding for LE 02471: Abounding Rivers:
Provider reported an issue with their admit call throwing guarantor error. Integration investigated and found no issue with the data. Asked DMH Revenue Systems team to verify if LE02471 needs any guarantor setup. Notified provided that we are working on the issue.




## Legal Entities (LE)
Closed = Provider is no longer active with the Department.
Active = Provider is process of onboarding or actively sharing data with the Department. PROD and/or NonProd tags indicate if provider is active in the environment.

::: query-table 2852a12e-3db1-4eb0-aceb-53cac84ab415
:::

## Fee-for-Service (FFS)
Closed = Provider is no longer active with the Department.
Active = Provider is process of onboarding or actively sharing data with the Department. PROD and/or NonProd tags indicate if provider is active in the environment.

::: query-table 50781838-8e69-47b6-95d1-6446f82d8999
:::

## Mental Health Plans (MHP)

*   LACare currently has issue with SFTP disconnect.
*   BlueShield is in process of onboarding.
::: query-table b4b5b9ad-e5b6-4007-bc27-5a8ea1205510
:::
## Vendors
* TODO: SFTP for NetsmartCM project
* TODO: New PBM onboarding

## Other Government Agencies/County Departments
* CA DHCS Medical Connect integration testing
* DPSS
* DPH
* DCFS
* TTC

## **2.2.2 BizTalk Server maintenance**
On-premises Server administration and maintenance.
* DevOps: Charlie Wang
::: query-table 7daee816-1f8e-4b96-9efd-7780b3435224
:::

## **2.2.3 EFT/MFT Administration**
All non-HIDEX administration operations.
* DevOps: Joe Martinez
::: query-table 3e5ab2b5-2334-4c98-97b1-467ca65d30a7
:::
GoAnywhere Implementation tracked as part of HIDEX.

## **2.2.5 Azure Cloud Administration**
All non-HIDEX administration operations:
* DevOps: Charlie Wang
::: query-table 5d1c6cff-6056-4d90-bdda-f6144c36dad8
:::

## **2.2.6 DevSecOps Services**
All non-HIDEX Security, Infrastructure, and DevOps service related operations in progress:
* DevOps: Joe Martinez
::: query-table 2996c28d-a4e6-46db-909d-728d3851e4bf
:::

<div style="page-break-after: always"></div>


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