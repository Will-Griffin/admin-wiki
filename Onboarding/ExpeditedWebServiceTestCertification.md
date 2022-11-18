# Expedited Certification DRAFT

## Overview
This document defines the web service expedited web service testing.

##Requirements

Provider is required to submit successful calls from each operation for each environment and provide csv of call information to HEAT in lieu of the full script/outcome.  Complete as much as the existing script as possible.  Minimum accepted operations are available in defined below:

###Scenario 1 New provider with Vendor that has contracts with other providers in production
Step 1, 2, 4, and 14 
###Scenario 2 Both provider and vendor are in production (vendor change)
Step 1, 2
###Scenario 3 ??


##When complete 
submit a csv to heat with this information:

providerno, datetime of call, operation, message recieved (error, success, etc.)


Team will review transactions in BAM from each environment and compare against csv.

BAM query to check for successful calls from each operation per environment.
TODO: define query here

BAM query to check for failed calls.
TODO: Define query here



Provider will proceed to production but be put on a watch list until remaining operations are logged in BAM.

BAM query to check for successful calls from each operation per environment.
TODO: define query here

BAM query to check for failed calls.
TODO: Define query here

Consistent failures indicate a problem, and notify production that they will be disconnected.

