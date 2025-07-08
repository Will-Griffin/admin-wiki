# LACDMH Integration Services 

# 2. Maintenance & Operations 

## 2.1. Maintenance

## Release Schedule: 
![image.png](/.attachments/image-333f5978-e1e5-4028-a12b-1cb5579c7ece.png)

### 2.1.1 CSI Web service
### Current Status

- Latest Release: SR#753909 Initial Psychiatric Data capture modification is live now in Production environment as of 2024-12-17, current version: 202001 R2
- Testing in BTIDE3 environment was completed and reported back to the team.
- The query below shows the work items as work in-progress. Out of these following work items have been developed and deployed to DEV:
26457, 46377, 48666, 49985
- Deployment to DEV has an issue and it's being worked on (Work Item # [52556](https://lacdmh-integrationservices.visualstudio.com/CSI/_workitems/edit/52556))

### Next Steps
- Complete testing in DEV once the deployment issue is fixed and API is ready for testing.

Current Work Items In Progress
::: query-table 94c595b1-c57c-4f04-aff2-7b3e87915794
:::
Issues
::: query-table 486cf8fc-eb51-4d3c-9bf0-1eb1983bbb7b
:::

### 2.1.2 SRL Web service
### Current Status
- Screening Tool Questionnaire and Shool Based Data intake deployed to PRODUCTION on 01/28/205. 
- All backlogged items are marked ready for development and assigned to development team.

### Next Steps
- Complete the work item from the list below:

To Be Completed:
::: query-table a2a8d4b1-a285-4b8e-b137-5789bfd6c2e2
:::


### 2.1.3 Client Web Service (CS)
### Current Status
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
### CURRENT STATUS:
- Testing with Access Center dev team and ISD is in progress.
- Working with NTST to deploy the LA DEV changes they made in to LA UAT. NTST does not have an interface from LA UAT to MDM QA. Team is discussing impact and whether we can move from LA DEV to LA LIVE bypassing QA.

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
Current Trend (June ) : 105 Cases (Open & Closed)



![Untitled.png](/Integration-Services/.attachments/HEATReport.png)
 
Monthly trend for 2025: approx. 80 cases per month 


Tasks Assigned for Integration Team for June in HEAT systems:

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
| **Grand Total** | **105** |

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