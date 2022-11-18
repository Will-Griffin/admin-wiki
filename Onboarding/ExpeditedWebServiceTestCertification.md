# Expedited Certification DRAFT
## Overview
This document defines the processes for LA County Mental Health service API testing and certification. 

The following scenarios describe the Use Cases applicable to Contracted Providers undergoing certification. 

###Scenario 1 New provider with Vendor that has contracts with other providers in production --Step 1, 2, 4, and 14 NOTE: Are steps needed? 

Contracted Providers integrating with LACDMH via service API which fall under scenario 1 are required to submit successful calls for the following operations and workflows (Complete the existing script to extent applicable): 
###Fill in required operations

in the following environments: 
###Fill in required operations

Once submissions are complete, the Contractor shall provide csv of call information to HEAT ticket provided by DMH certification analysts. 


###Scenario 2 Both provider and vendor are in production (vendor change) --Step 1, 2
NOTE: Are steps needed? 

Contracted Providers integrating with LACDMH via service API which fall under scenario 2 are required to submit successful calls for the following operations: 
###Fill in required operations

in the following environments: 
###Fill in required operations

Once submissions are complete, the Contractor shall provide csv of call information to HEAT ticket provided by DMH certification analysts. 


###Scenario 3 ??

Submission Review Process 

Once DMH receives the CSV file from Contractor, Certification Analysts will review transactions in BAM from each environment and compare against csv.

BAM query to check for successful calls from each operation per environment.
TODO: define query here

BAM query to check for failed calls.
TODO: Define query here

Provider will activated in production environment upon all required submissions without errors? ##define criteria## and will be monitored until remaining operations are logged in BAM.

Consistent failures indicate a problem, and notify production that they will be disconnected.

BAM query to check for successful calls from each operation per environment.
TODO: define query here

BAM query to check for failed calls.
TODO: Define query here

##CSV Requirements
CSV files should contain only the following: 
Provider #, Date & time of submission, operation, message received, submission outcome (error, success, etc.)
Files should be | delimited and first row should contain headers for the data provided. 







