How to Troubleshoot HIDEX problem by using Azure Portal:

Using Application Insight to trace the message sending to NTST:
Example of tracing of post call to NTST QUERY:

traces
| where message has 'netsmart | Received response' or message has 'netsmart | Sending POST'




Follow the steps below to validate/verify the LOCUS Script transactions:

Step # 1: 
Identify the LE number (Program ID), Client ID, Encounter ID, Practitioner ID from the submitted script.