# Standard Operating Procedures — Support Team

[[_TOC_]]

---

## Overview

The Support Team is the operational backbone of Integration Services. This document defines the standard procedures every Support Team member must follow to ensure consistent, high-quality service delivery across incident management, vendor/provider onboarding, API testing coordination, and data validation.

---

## 1. Incident & Ticket Management

### 1.1 HEAT Ticket Triage

| Step | Action |
|------|--------|
| 1 | Log in to the HEAT ticketing system and review the queue each morning by **8:15 AM**. |
| 2 | Categorize each new ticket: **P1 – Critical**, **P2 – High**, **P3 – Medium**, **P4 – Low**. |
| 3 | Assign the ticket to the appropriate team member or escalate to Dev/DevOps as needed. |
| 4 | Update the ticket status to **In Progress** within 15 minutes of assignment. |
| 5 | Document all troubleshooting steps as internal notes within the ticket. |
| 6 | Resolve and close the ticket with a resolution summary; notify the requestor. |

**Priority Definitions:**

| Priority | Description | Response SLA | Resolution SLA |
|----------|-------------|--------------|----------------|
| P1 – Critical | Production outage or data loss | 15 minutes | 4 hours |
| P2 – High | Significant feature impaired | 1 hour | 8 hours |
| P3 – Medium | Minor issue with workaround | 4 hours | 3 business days |
| P4 – Low | Informational / enhancement | Next business day | As scheduled |

### 1.2 Escalation Path

```
Support Team Member → Support Lead → Development Team Lead → Integration Services Manager
```

- Escalate **P1** issues immediately; do not wait for the next standup.
- Create an Azure DevOps work item linked to the HEAT ticket for all P1 and P2 issues.
- Send a notification to the **#incidents** channel in Teams when escalating.

---

## 2. Daily Operations

### 2.1 Morning Checklist (8:00 AM)

- [ ] Review HEAT ticket queue and triage new items.
- [ ] Check NTST SF for open ticket status updates.
- [ ] Verify nightly batch job completions (EDI, EFT pipelines).
- [ ] Confirm BizTalk host instances are running — log any anomalies.
- [ ] Review any overnight alerts in Log Analytics / Application Insights.
- [ ] Attend daily standup at **8:00 AM** (brief updates: blockers, open items).

### 2.2 Afternoon Checklist (2:00 PM)

- [ ] Attend afternoon sync at **2:00 PM**.
- [ ] Update status on all active tickets.
- [ ] Coordinate any late-day provider or vendor communications.
- [ ] Document resolutions or discoveries from the day.

---

## 3. Vendor & Provider Onboarding

### 3.1 New Provider Onboarding Steps

1. **Intake:** Receive onboarding request via HEAT ticket or email; confirm scope (EDI, API, EFT).
2. **Coordination:** Schedule Provider Onboarding call (Tuesdays at 11:30 AM).
3. **Certificate Review:** Validate certificates and credentials submitted by provider:
   - Check expiry dates.
   - Verify thumbprint matches the configured party in BizTalk.
4. **Script Review:** Review LOCUS certification scripts per the [LOCUS Validation guide](../../Operations/Support/How-To-Validate-Submitted-LOCUS-Certification-Script-for-Providers.md).
5. **Configuration:** Work with DevOps to provision new ports, agreements, and pipeline configurations.
6. **Testing:** Conduct end-to-end testing using Bruno or Postman; validate response codes.
7. **Go-Live:** Confirm go-live date and communicate to stakeholders; update Book of Business.
8. **Documentation:** Update relevant wiki pages and close the HEAT ticket.

### 3.2 Provider Cutoff (Monthly)

- Disable LE or FFS groups in EFT on the scheduled cutoff date.
- Run the PS1 SQL query to verify the record is correctly removed from the database.
- Document the change with a screenshot and link in the monthly cutoff ticket.

---

## 4. API Testing Coordination

### 4.1 Pre-Go-Live API Validation

1. Obtain the test case matrix from the Development Team.
2. Execute test cases in Bruno (preferred) or Postman against the **QA** environment.
3. Log defects as Azure DevOps work items linked to the parent story.
4. Coordinate with Development for fixes; re-test after each fix.
5. Sign off with a pass/fail summary before Production deployment.

### 4.2 HIDEX Troubleshooting (Quick Reference)

- **Application Insights (Netsmart trace):**
  ```kql
  traces
  | where message has 'netsmart | Received response'
      or message has 'netsmart | Sending POST'
  ```
- **Log Analytics (APIM gateway):**
  ```kql
  ApiManagementGatewayLogs
  | project TimeGenerated, ApiId, OperationId, ApimSubscriptionId,
            RequestBody, ResponseCode, ResponseBody, BackendUrl
  | where OperationId has 'post-encounter'
  | where toint(ResponseCode) == 500
  | order by TimeGenerated desc
  ```
- Full guide: [How to Troubleshoot HIDEX problem by using Azure Portal](../../Operations/Support/How-to-Troubleshoot-HIDEX-problem-by-using-Azure-Portal.md)

---

## 5. Data Validation & Mapping

1. Use Log Analytics to pull raw message payloads for the transaction in question.
2. Cross-reference with the EDI/HL7/FHIR specification or trading partner agreement.
3. Identify field-level mapping discrepancies and document them in a work item.
4. Engage Development to apply mapping corrections; validate in QA before promoting.
5. Update the data dictionary or mapping document after every approved correction.

---

## 6. BizTalk Operations

### 6.1 Routine Monitoring

- Log in to BizTalk Admin Console daily to check for **Suspended Messages**.
- Run the SQL query for suspended/active messages and party thumbprint checks:
  - Target server: `sqlp6.support` (or equivalent).
- Review the BHM 6 AM daily health check output (`mbvoutput`).

### 6.2 Error Correction

1. Identify suspended message(s) in BizTalk Admin Console.
2. Check party properties — confirm thumbprint is valid.
3. Resume or terminate the message per the business rule (do not resume without confirming root cause).
4. Document in the BizTalk support log and link to the relevant HEAT ticket.
5. See also: [BizTalk Support procedures](../../Operations/Support/BizTalk-support.md)

---

## 7. Change Control

- All production changes must be submitted via the Change Control process.
- Change Control meeting: **Tuesdays at 1:00 PM**.
- Submit change requests at least **48 hours** before the meeting.
- Include: change description, risk assessment, rollback plan, and testing evidence.

---

## 8. Documentation Standards

- All new runbooks, procedures, or troubleshooting guides must be added to this wiki.
- Use clear headings, numbered steps, and code blocks for queries/commands.
- Link related wiki pages where applicable.
- Review and update assigned documentation quarterly.

---

## 9. Key Contacts & Resources

| Resource | Link / Contact |
|----------|---------------|
| HEAT Ticketing System | Internal HEAT URL |
| NTST SF Ticket Tracker | Netsmart ServiceFirst portal |
| Azure DevOps (Integration Services) | https://dev.azure.com/LACDMH-DPH-Integration |
| Azure DevOps (Administration) | https://lacdmh-integrationservices.visualstudio.com/Administration |
| Log Analytics | Azure Portal → Log Analytics Workspace |
| Application Insights | Azure Portal → Application Insights |
| BizTalk Admin Console | BizTalk Server Admin Console (on-prem) |
| Change Control Calendar | Teams calendar — Integration Services Change Control |
