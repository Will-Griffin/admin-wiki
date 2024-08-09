# LACDMH Integration Services 

# 2. Maintenance & Operations 

## 2.1. Maintenance

## Release Schedule: 
![image.png](/.attachments/image-333f5978-e1e5-4028-a12b-1cb5579c7ece.png)

### CSI Web service
##Current Status
- Debugging deployment error in DEV.
- No risks to timeline in delivery plan above.

##
Next Steps
- Correct deployment issue

Current Features In Progress
::: query-table c7faaa46-e069-4b62-a85f-e00d63419d0c
:::
Risks
::: query-table 486cf8fc-eb51-4d3c-9bf0-1eb1983bbb7b
:::

### SRL Web service
### Current Status
- Business rules and bug fixes in progress.
- schema changes ready for deploy.
### Next Steps
- Finalize testing for release 1 schema changes.
- Finalize release 2 for validations.

Current Features in Progress
::: query-table 164edab6-443a-4e74-a8ca-6663d79bb93f
:::
Risks
::: query-table 1e3c461c-0651-4bc9-b14b-1a0b1bb7b686
:::

### Client Web Service (CS)

Current Features in Progress
::: query-table 507ae795-fde1-42e9-9412-bbb419bb5c57
:::
Issues/Risks
::: query-table 4cf3a176-7e5d-4a3f-ba64-3ada202c8389
:::

### MDM Web service

### Current Status:
- Testing with Access Center dev team and ISD is in progress.
- ISD security software is blocking authentication for Access Center update.
- Access Center project is on pause pending SOW issues.
- Netsmart released Avatar Cal-PM 2024 Update 54 (for returning data elements in getClientDetails operation). This relates to required MDM changes.

### Next Steps:
- Netsmart is still working on resolving the getClientDetails operation issue related to Avatar Cal-PM 2024 Update 54 (SF case CS2775727).
- Resolve authentication issue with ISD.
- Dev and testing as needed based on Netsmart changes.
- Test and confirm solution works with Access Center integration.
- Promote/schedule build deployment to upper environments.


Current Features In Progress
::: query-table 73965f26-c347-4258-a446-2c1da512122d
:::
Issues/Risks
::: query-table db4f3db4-fc4b-4331-b395-2081ea045960
:::

### Healthcare Provider Directory (HCPD) EDI274 Integration
### Current Status:
- Development is currently on hold pending DHCS issuing SFTP acount for automation.
- Monthly file processing as scheduled, no major issues to report.
### Next Steps:
- None.

Current Features in Progress
::: query-table fb0471f7-23a7-469a-ab5c-2fd11b43b486
:::
Risks
::: query-table a6421a9f-0b14-4a25-a9b3-a681513fbd8d
:::

###BizTalk Server maintenance

Current Features in Progress
::: query-table 7daee816-1f8e-4b96-9efd-7780b3435224
:::
Risks
::: query-table 6bed7806-4b75-4fd9-8f30-e6ec1315ba1b
:::

## 2.2. Operations

## EDI and Web service Onboarding

## 2.2.1. LE Onboarding Status 
::: query-table 2852a12e-3db1-4eb0-aceb-53cac84ab415
:::

## 2.2.2. FFS Onboarding Status
::: query-table 50781838-8e69-47b6-95d1-6446f82d8999
:::

###EFT/MFT Administration

::: query-table [insert query guid here]
:::

###Azure Cloud Administration

::: query-table [insert query guid here]
:::

###DevSecOps Services

::: query-table [insert query guid here]
:::

<div style="page-break-after: always"></div>

# 3. Help Desk Tickets
Current Trend (Jan 1st - Current) : 653 Cases (Open & Closed)

**Weekly trend for August is approximately 21 cases.**

![Untitled.png](/Integration-Services/.attachments/HEATReport.png)
 
Monthly trend for 2024: approx. 90 cases per month 


Tasks Assigned for Integration Team from July 1st to current in HEAT systems:

| Category|                     No of Tickets |
|  --- | --- |
| 999 | 2 |
| ACCESS | 5 |
| Certificate Status | 1 |
| Claim Status | 1 |
| Connection Issue | 2 |
| Error| 5 |
| Generation Questions | 3 |
| Installation Certificate | 1 |
| Update Request | 1 |
| **Grand Total** | **21** |

Salesforce Cases: 
::: query-table f565c801-1c1e-4d4c-afdf-880b63429b27
:::

<div style="page-break-after: always"></div>

# 4. Special Support 

## 4.1. In Progress

**Private Insurance Billing Implementation -- Active -- Priority 8**
Updates
::: query-table [insert query guid here]
:::

**ECM Data Exchange Implementation - Active -- Priority 9**

## 4.2. In Queue**

Issues/Risks
::: query-table 088f9aa3-6d65-4c74-a88f-a8c7487d8e79
:::

## 4.3. In Analysis**

::: query-table [insert query guid here]
:::

## 4.4. Approved Projects - Not started**

::: query-table [insert query guid here]
:::

<div style="page-break-after: always"></div>

# 5. On HOLD (Items in this section will remain static until re-activated) 

**Project -- Subscription consolidation (Azure Gov & Commercial) --
Priority 4**

-   Provided list of resources to DMBI, App Dev and Int on 8/30/21
-   Began inventory of resources left on DMH's legacy subscription
-   Working with ISD to implement commercial subscription
-   Provided access to App Dev resources

**Project -- Subscription Organization and Ratification (Azure Gov &
Commercial) -- Priority 5**

-   Met with Mark Cheng and John Ortega 11/2/21
-   Integration to work with DMBI to produce organization proposal for
    Mark and John's approval

**Project -- BizTalk Azure Migration -- Cancelled**

-   This effort is no longer needed as HIDEx/IPaaS will replace the
    BizTalk on-prem functionality
-   ~~Team has implemented Vnet, subnets, Network security groups, and
    VMs~~
-   ~~Developed Azure Resource Management Templates for deployment of
    resources~~
-   ~~In process of Working with Security and Shared Services teams to
    deploy ARM template and validate access permissions~~
-   ~~ISD Security to provide feedback on ARM templates -- requested
    update on 12/16/20~~
-   ~~Meeting scheduled for 12/17/20~~
-   ~~ISD reviewing/processing proposed changes -- Review has been
    pending 3 weeks~~
-   ~~Update requested 1/7/2021~~
-   ~~Request for update escalated on 1/13/2021~~
-   ~~Azure ARM templates stalled due to ISD security review~~
-   ~~Team has not been able to get feedback from ISD security since Nov
    2021~~
-   ~~Escalating to ISD Management~~
-   ~~ISD requesting that all traffic be routed to ISD data center~~
-   ~~DMH team discussed with Microsoft and neither agrees traffic
    should be routed to ISD prior to Azure.~~
-   ~~Requires discussion with ISD and escalation with DMH.~~
-   ~~Integration team escalated with DMH Security. Working on diagram
    and documentation for discussion.~~
-   ~~Next steps to escalate with ISD Manager Rumi Salihue~~

**ITAM**

-   Use ITAM to track division assets and configuration
-   Melvin M to setup a meeting to demo
-   Follow up email sent to Melvin on 1/29/20
-   Demo scheduled for 2/13/20
-   Discussed necessary data for ITAM pilot
-   DevOps currently working on providing extract for load to ITAM
-   Draft extract provided to 5/14/20
-   Resuming Activity 9/9/20
-   EDI work put on hold to accommodate Client Services change deployed
    9/18/20
-   CS deployments to TST, QA, and Prod completed
-   EDI work resumed and currently testing application
-   Team working out issues with test Trading Partners

**VSee**

-   Telepsych solution, currently conducting discovery in partnership
    with Project Delivery
-   Requested documentation on 7/15/20, 7/22/20
-   No Documentation received as of ~~7/29/20~~, ~~8/5/20 8/12/20~~
-   Sent updated request for documentation on ~~8/12/20~~ 8/27/20
-   Requested update ~~10/8/20~~, 10/20/20
-   Technical documentation has not been provided as of 10/20/20,
    despite several requests.

<div style="page-break-after: always"></div>

# 6. Recently completed (Items in this section are removed once reviewed) 

**Service Request # 746493 -- EPSDT Service Modification**

-   All service changes are complete.

**Project -- Completed (Scriptlink Integration) -- Priority 4**

-   Service modifications complete -- working on deployments. See
    Release Schedule portion of BOB for deployment dates.
-   ~~Three uses cases defined by Informatics~~
-   ~~Documented processes for use cases~~
-   ~~Defined preliminary architecture~~
-   ~~ARM templates developed and tested~~
-   ~~DevOps pipelines being developed~~
-   ~~Current issue with DCI Import service~~
    -   ~~Service is not available outside of DMH network~~
    -   ~~Options are to:~~
        -   ~~Abstract DCI with BizTalk interface~~
        -   ~~Implement necessary networking between Azure and DCI
            Import service~~

**MDM Environment Migration - Completed -- Priority 10**

-   Migration of Production, Test, and Dev environments completed on
    1/18/2022.
-   Decommission of legacy servers completed in January 2022. Billing to
    stop in Feb 2022.

**Provider Merger -- Completed (Pacific Clinics & Uplift) -- Priority 7**

-   Team has implemented necessary profiles for new entity.
-   Production certs validated 3/16/22
-   Welligent ran scripts to create admissions for migrating clients to
    LE00120 on 3/16/22.
-   Merger completed 3/1/22

**Program Implementation - Active (STARS Behavioral Health/CRTP)**

-   All service changes are complete.

<div style="page-break-after: always"></div>