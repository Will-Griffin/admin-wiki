Expedited Web Service

This document defines the web service expedited web service testing.

Provider is required to submit successful calls from each operation.  Each operation has a weighted score.  Complete as much as the existing script as possible.

For providers already in production with vendor already in production: (vendor change example Clinivate --> Exym)

minimum is create an admission, diagnosis, episode.

Submit a csv to heat with this information:

providerno, datetime of call, operation, message recieved (error, success, etc.)


BAM query to check for successful calls from each operation per environment.



BAM query to check for failed calls.
None should exist in prod.
Consistent failures indicate a problem, and will disable the connection.

