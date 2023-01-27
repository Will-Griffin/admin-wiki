# Service API Certification DRAFT
## Overview
This document defines the processes for LA County Mental Health service API testing and certification. 

The following scenarios describe the Use Cases applicable to Contracted Providers undergoing certification: 

- ###Scenario 1: New provider with Vendor that has contracts with other providers in production
  Contracted Providers integrating with LACDMH via service API which fall under scenario 1 are required to submit successful calls for the following operations and workflows (Complete the existing script to extent applicable): 
  - Search
  - Admission
  - Diagnosis
  - CSI

  In the following environments: 
  - QA
  - PROD

  Once submissions are complete, the Contractor shall provide csv of call information to HEAT ticket provided by DMH certification analysts. 


- ###Scenario 2: Both provider and vendor are in production (vendor change)

  Contracted Providers integrating with LACDMH via service API which fall under scenario 2 are required to submit successful calls for the following operations: 

  - Search
  - Admission

  In the following environments: 
  - QA
  - PROD

  Once submissions are complete, the Contractor shall provide csv of call information to HEAT ticket provided by DMH certification analysts. 
- ###Scenario 3: Both provider and vendor are New to LA County

  Contracted Providers integrating with LACDMH via service API which fall under scenario 3 are required to submit successful calls for all operations listed in the certification script in the following environments: 
  - QA

  Once submissions are complete, the Contractor shall provide csv of call information and the completed certification script to the HEAT ticket provided by DMH certification analysts.

##CSV Requirements
CSV files should contain only the following: 
- Provider #
- Date & time of submission
- operation
- message received
- submission outcome (error, success, etc.)

Files should be | delimited and first row should contain headers for the data provided. 

##Submission Review Process 


1. Once DMH receives the CSV file from Contractor, Certification Analysts will review transactions in the logs from each environment and compare against csv.

2. Provider will be activated in production environment when all required service request messages and their corresponding responses are logged without errors in QA.

3. In production, monitoring will continue for providers in Scenario 1-2 by Certification Analysts until all remaining operations listed in the certification script are logged.

NOTE: Consistent failures indicate a problem, and the provider will be notified to correct or be disconnected from production.

###Queries Used
- Successful messages:

  ```sql
  SELECT TOP (1000) [RecordID]
      ,[ActivityID]
      ,[PortName]
      ,[SenderName]
      ,[StartTime]
      ,[EndTime]
      ,[MessageIDIn]
      ,[InterchangeID]
      ,[MessageIDOut]
      ,[MessageActivityID]
      ,[EndToEndTrackingID]
      ,[RootNode]
      ,[MessageType]
      ,[IsRequestReply]
      ,[MessageSubType]
      ,[TransportLocation]
      ,[IsSyncFault]
      ,[LastModified]
  FROM [BAMPrimaryImport].[dbo].[bam_CSMessageReceive_AllInstances] with (nolock)
  where sendername like '%Provider Name%'
  and IsSyncFault = 0
  order by startTime desc

- Failure/Error messages:

  ```sql
  SELECT TOP (1000) [RecordID]
      ,[ActivityID]
      ,[PortName]
      ,[SenderName]
      ,[StartTime]
      ,[EndTime]
      ,[MessageIDIn]
      ,[InterchangeID]
      ,[MessageIDOut]
      ,[MessageActivityID]
      ,[EndToEndTrackingID]
      ,[RootNode]
      ,[MessageType]
      ,[IsRequestReply]
      ,[MessageSubType]
      ,[TransportLocation]
      ,[IsSyncFault]
      ,[LastModified]
  FROM [BAMPrimaryImport].[dbo].[bam_CSMessageReceive_AllInstances] with (nolock)
  where sendername like '%Provider Name%'
  and (IsSyncFault = 1 OR MessageIDOut is Null)
  order by startTime desc
