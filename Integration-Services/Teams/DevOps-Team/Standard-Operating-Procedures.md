# Standard Operating Procedures — DevOps Team

[[_TOC_]]

---

## Overview

This document defines the standard operating procedures for the Integration Services DevOps Team. It covers pipeline management, infrastructure provisioning, monitoring & alerting, access management, release management, and incident response from an operations and infrastructure perspective.

---

## 1. Daily Operations

### 1.1 Morning Checklist

- [ ] Review Azure Monitor dashboards and alerts from overnight.
- [ ] Check pipeline run health in Azure DevOps — investigate any failed runs.
- [ ] Verify Application Insights / Log Analytics for anomalies.
- [ ] Review GitHub Actions workflow runs for failures.
- [ ] Attend daily standup at **11:00 AM**.
- [ ] Review and action any access provisioning requests.

### 1.2 Key Dashboards & Monitors

| Dashboard | Purpose |
|-----------|---------|
| Azure Monitor | Infrastructure health, metrics, alerts |
| Application Insights | Application performance, traces, exceptions |
| Log Analytics | Cross-resource log analysis, KQL queries |
| Azure DevOps Pipelines | CI/CD build and release status |
| BHM 6 AM Health Check | BizTalk daily health (`mbvoutput`) |

---

## 2. CI/CD Pipeline Management

### 2.1 Pipeline Standards

All pipelines must follow these standards:

- **YAML pipelines only** — no Classic/GUI pipelines for new work.
- Pipelines must use **pipeline templates** for shared stages and steps.
- All environment-specific values must be **parameterized** — no hardcoded values.
- Secrets must be sourced from **Azure Key Vault** via variable groups.
- All production pipelines must require an **approval gate** before deployment.

See [Pipeline RBAC](../../Governance/Azure-DevOps/Pipeline-RBAC.md) for access control rules.

### 2.2 Pipeline Failure Response

1. Identify the failing step from the pipeline run logs.
2. Check if the failure is infrastructure-related (connectivity, resource availability) or code-related.
3. For code failures: notify the Development Team; assign a work item.
4. For infrastructure failures: investigate and remediate; document the issue.
5. Re-run the pipeline after remediation.
6. For recurring failures: create a work item for root cause investigation.

### 2.3 Environment Promotion Flow

```
Dev (CI) → QA (CD, auto-deploy) → Staging (CD, approval required) → Production (CD, Change Control required)
```

- Dev and QA deployments may be automated.
- Staging and Production deployments require environment approvals.
- See [Environments](../../Operations/DevOps/Environments.md) for approver configuration.

---

## 3. Infrastructure-as-Code (IaC)

### 3.1 IaC Standards

- All Azure resources must be provisioned via **Bicep** or **Terraform** — no manual Azure Portal provisioning in QA, Staging, or Production.
- IaC code must be stored in version control (Azure DevOps / GitHub).
- Infrastructure changes must go through the PR process with at least one reviewer.
- All resources must follow the [Azure Naming Conventions](../../Governance/Azure-Naming-Conventions.md).
- Resources must be organized per the [Resource Organization](../../Architecture/Resource-Organization.md) guidelines.

### 3.2 Resource Provisioning Request Process

1. Developer or Support submits a resource request via Azure DevOps work item.
2. DevOps Team reviews: confirm naming, sizing, RBAC requirements, and cost.
3. DevOps implements IaC changes in a feature branch and creates a PR.
4. PR reviewed and approved by DevOps Lead.
5. Pipeline deploys to Dev/QA for validation.
6. Change Control submitted for Production provisioning.
7. Production provisioned after Change Control approval.

---

## 4. Access Management

### 4.1 Access Provisioning

All access requests must be submitted via the approved ticketing process:

| System | Access Process |
|--------|---------------|
| Azure Portal (subscriptions) | Azure RBAC via Azure AD groups — submit request to IT or DevOps |
| Azure DevOps | Managed via [Teams & Permissions](../../Governance/Azure-DevOps/Permissions.md) — request via work item |
| GitHub | Repository access via GitHub org — request via work item |
| Azure Key Vault | Key Vault access policies or RBAC — approved by DevOps Lead |
| Service Connections | Governed by [Service Connection RBAC](../../Governance/Azure-DevOps/Service-Connection-RBAC.md) |

**Principle of Least Privilege:** All access grants must follow the minimum required access level.

### 4.2 Access Review

- Conduct quarterly access reviews for all Azure subscriptions and Azure DevOps projects.
- Remove access within 24 hours of a team member offboarding.
- Document all access grants and revocations in the access audit log.

---

## 5. Monitoring & Alerting

### 5.1 Alert Configuration

All production resources must have the following alerts configured in Azure Monitor:

| Alert Type | Threshold | Channel |
|-----------|-----------|---------|
| Azure Function failures | > 5 failures in 5 minutes | Teams webhook, email |
| APIM error rate | > 10% 5xx responses in 5 minutes | Teams webhook, email |
| BizTalk host instance down | Any instance down | Teams webhook, email |
| Pipeline failure (NTST Smoke) | Any failure | Teams webhook |
| Resource availability | < 99% uptime | Teams webhook, email |

### 5.2 NTST Smoke Pipeline Maintenance

- NTST smoke pipelines make direct calls to Netsmart/ClientServices.
- Run on **hourly** schedule.
- On failure: notify Support Team immediately; begin incident triage.
- Adjust pipeline frequency or parameters as needed following Netsmart changes.

### 5.3 BizTalk Live Monitoring

- Configure BHM rules to alert when receive/send ports + host instances go down.
- Note: some ports are expected to stay down — validate against the allow-list before alerting.
- Live monitoring configuration should align with the [BizTalk Support Runbook](../../Operations/Support/BizTalk-support.md).

---

## 6. Release Management

### 6.1 Standard Release Process

1. Development Team merges code to `main`; CI pipeline triggers automatically.
2. QA pipeline auto-deploys to QA environment.
3. Support Team validates in QA (functional sign-off).
4. DevOps Team verifies pipeline health and monitoring for QA.
5. Submit Change Control request for Production deployment (minimum 48 hours notice).
6. After Change Control approval: trigger Staging pipeline with approval gate.
7. Staging validation (Dev + Support).
8. Trigger Production pipeline with approval gate.
9. Post-deployment monitoring: 30-minute watch window.
10. Document release in the release log.

### 6.2 Rollback Procedure

1. Identify the failing deployment and version.
2. Trigger the rollback pipeline (prior release artifact) or re-deploy the previous version.
3. Verify rollback success via monitoring dashboards and smoke tests.
4. Notify all stakeholders of the rollback.
5. Document in the Change Control ticket.
6. Conduct root cause analysis within 24 hours.

---

## 7. Security Operations

### 7.1 Secret Rotation

- All Azure Key Vault secrets must be rotated per the schedule:
  - API keys and connection strings: every **90 days**.
  - Certificates: before expiry (alert at 30 days remaining).
- Use Azure Key Vault expiry notifications and automate rotation where possible.
- After rotation: trigger pipeline to redeploy affected services.

### 7.2 Certificate Management

- Track all certificate expiry dates in the certificate tracking log.
- Set Azure Monitor alerts for certificates expiring within 30 days.
- For provider certificates in BizTalk: coordinate with Support Team for thumbprint updates.

---

## 8. Change Control

- All infrastructure changes to QA (some), Staging, and Production require Change Control approval.
- DevOps submits the change request in the Change Control system.
- Change Control meeting: **Tuesdays at 1:00 PM**.
- Include: change description, risk, rollback plan, testing evidence, approver.

---

## 9. Documentation Requirements

- All infrastructure provisioning steps must have an IaC template committed to source control.
- All pipeline designs must be documented in the Operations/DevOps section of the wiki.
- Alert thresholds and monitoring configurations must be documented.
- Post-incident reviews must be written within 24 hours and linked to the incident ticket.

---

## 10. Key Contacts & Resources

| Resource | Link |
|----------|------|
| Azure DevOps (HIDEX Pipelines) | https://dev.azure.com/LACDMH-DPH-Integration/HIDEX |
| Azure DevOps (Administration Pipelines) | https://lacdmh-integrationservices.visualstudio.com/Administration |
| Azure Portal | https://portal.azure.com |
| GitHub (Integration Services) | Internal GitHub organization |
| Pipeline RBAC | [Pipeline RBAC](../../Governance/Azure-DevOps/Pipeline-RBAC.md) |
| Service Connection RBAC | [Service Connection RBAC](../../Governance/Azure-DevOps/Service-Connection-RBAC.md) |
| Azure DevOps Environments | [Environments](../../Operations/DevOps/Environments.md) |
| Naming Conventions | [Azure Naming Conventions](../../Governance/Azure-Naming-Conventions.md) |
