
## Sample Query

```kusto
AzureDiagnostics 
| where OperationName == "Microsoft.Logic/integrationAccounts/trackingEvents" and TimeGenerated >= ago(24h)
| project
    TimeGenerated,
    MessageType=event_record_messageProperties_messageType_s,
    MessageStatus=iif(event_record_messageProperties_isMessageFailed_b, "Failed", "Success"),
    MessageDirection=event_record_messageProperties_direction_s,
    Workflow=source_workflow_name_s,
    WorkflowRunId=source_runInstance_runId_s,
    WorkflowOperation=source_operation_operationName_s,
    TradingPartner=event_record_agreementProperties_senderPartnerName_s,
    TradingPartnerId=event_record_agreementProperties_senderIdentifier_s,
    Error=event_error_message_s,
    ErrorCode=event_error_code_s,
    GS08=event_record_messageProperties_gs08_s,
    GS01=event_record_messageProperties_gs01_s,
    ISA=event_record_messageProperties_isaSegment_s
```

## References

- https://docs.microsoft.com/en-us/azure/logic-apps/monitor-b2b-messages-log-analytics
- https://docs.microsoft.com/en-us/azure/logic-apps/monitor-b2b-messages-log-analytics#install-b2b-solution

