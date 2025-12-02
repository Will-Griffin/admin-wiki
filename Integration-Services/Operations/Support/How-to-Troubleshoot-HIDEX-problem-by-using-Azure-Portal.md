How to Troubleshoot HIDEX problem by using Azure Portal:

Using Application Insight to trace the message sending to NTST:

Example of tracing of post call to NTST QUERY:

traces
| where message has 'netsmart | Received response' or message has 'netsmart | Sending POST'

Using Log Analytics to trace the message sending to HIDEX:


