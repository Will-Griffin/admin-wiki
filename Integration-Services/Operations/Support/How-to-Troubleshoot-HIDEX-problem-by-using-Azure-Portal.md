How to Troubleshoot HIDEX problem by using Azure Portal:

Using Application Insight to trace the message sending to NTST:

![image.png](/.attachments/ApplicationInsight.png)

Example of tracing of post call to NTST QUERY:

traces
| where message has 'netsmart | Received response' or message has 'netsmart | Sending POST'

Using Log Analytics to trace the message sending to HIDEX:

![image.png](/.attachments/LogAnalytic.png)

Example of tracing calls for HIDEX QUERY:

ApiManagementGatewayLogs

| project
TimeGenerated,
ApiId,
OperationId,
ApimSubscriptionId,
RequestBody,
ResponseCode,
ResponseBody,
BackendUrl
| where OperationId has 'post-encounter' 
//| where ApimSubscriptionId !contains "acm" and ApimSubscriptionId !contains "scriptlink"
//| where toint(ResponseCode) == 201
//| where toint(ResponseCode) == 200
| where toint(ResponseCode) == 500
| order by TimeGenerated desc

//| where ApimSubscriptionId !contains "acm" and ApimSubscriptionId !contains "scriptlink"

ApiManagementGatewayLogs
//| where ApimSubscriptionId !contains "acm" and ApimSubscriptionId !contains "scriptlink"
| project TimeGenerated, ApiId, OperationId, ApimSubscriptionId, RequestBody, ResponseCode, ResponseBody, BackendUrl
//| where isnotempty( RequestBody)
//| where OperationId  has 'put-appointment' or OperationId has 'put-slot' or OperationId has 'put-schedule'
| where OperationId  has 'post-encounter' 
//| where toint(ResponseCode) == 201
//| where toint(ResponseCode) == 200
| where toint(ResponseCode) == 500
//| where ResponseBody has 'Program not provided for new admission'
| order by TimeGenerated desc


