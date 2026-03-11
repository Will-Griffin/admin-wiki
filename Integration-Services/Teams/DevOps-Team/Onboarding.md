# Onboarding Guide — DevOps Team

[[_TOC_]]

---

## Welcome to the Integration Services DevOps Team!

This guide is designed to help new DevOps Team members get up to speed on our infrastructure, pipelines, and operational processes. Complete each section in order during your first 90 days.

---

## Week 1 — Orientation & Access

### Day 1–2: Accounts & Access

Work with your manager to request access to the following systems:

| System | Purpose | Request Via |
|--------|---------|------------|
| Azure Portal | Cloud infrastructure & monitoring | Manager / Azure Admin |
| Azure DevOps (HIDEX) | CI/CD pipelines, repos, work items | Manager |
| Azure DevOps (Administration) | Secondary ADO org | Manager |
| GitHub (Internal Org) | Source control (post-migration) | Manager |
| Azure Subscriptions (relevant) | Resource management | Manager via RBAC request |
| Azure Key Vault | Secrets management (read for non-prod) | Manager |
| Microsoft Teams | Collaboration | IT Help Desk |
| SharePoint / Wiki | Documentation | Manager |
| BizTalk Admin Console | BizTalk monitoring (read-only) | Manager |

### Dev Environment Setup

- [ ] Install Azure CLI; run `az login` and verify subscription access.
- [ ] Install PowerShell 7+ and Az module: `Install-Module Az`.
- [ ] Install Bicep CLI and VS Code with Bicep extension.
- [ ] Install Terraform (latest version).
- [ ] Install Git; configure user name and email.
- [ ] Install Docker Desktop.
- [ ] Install kubectl (for AKS access if applicable).
- [ ] Clone pipeline template repositories from Azure DevOps / GitHub.

### Day 3–5: Platform Orientation

- [ ] Review [Integration Services Overview](../../Integration-Services.md).
- [ ] Read [Architecture Overview](../../Architecture.md) to understand the platform.
- [ ] Read [DevOps Team SOPs](./Standard-Operating-Procedures.md).
- [ ] Review [Governance: Azure DevOps](../../Governance/Azure-DevOps.md) (all sub-pages).
- [ ] Review [Azure Naming Conventions](../../Governance/Azure-Naming-Conventions.md).
- [ ] Review [Resource Organization](../../Architecture/Resource-Organization.md).
- [ ] Shadow a senior engineer for a pipeline walkthrough (HIDEX CI/CD pipeline).
- [ ] Set up Azure Portal favorites: Monitor, Log Analytics, Application Insights, Key Vault.

---

## Week 2–3 — Deep Dive

### Pipeline & Infrastructure Knowledge

Review these wiki articles in depth:

1. [Environments](../../Operations/DevOps/Environments.md)
2. [Branching Strategy](../../Operations/DevOps/Branching-Strategy.md)
3. [Test Strategy](../../Operations/DevOps/Test-Strategy.md)
4. [Load Testing](../../Operations/DevOps/Test-Strategy/Load-Testing.md)
5. [Department-Specific Pipelines](../../Operations/DevOps/Department-Specific.md)
6. [Pipeline RBAC](../../Governance/Azure-DevOps/Pipeline-RBAC.md)
7. [Service Connection RBAC](../../Governance/Azure-DevOps/Service-Connection-RBAC.md)
8. [Approvals](../../Governance/Azure-DevOps/Approvals.md)
9. [Identity & Access Management](../../Architecture/Identity-&-Access-Management.md)
10. [Configuration Management](../../Architecture/Configuration-Management.md)

### Architecture Deep Dive

1. [Workstreams — Azure Cloud](../../Architecture/Workstreams/Azure-Cloud.md)
2. [Azure DevOps Workstream](../../Architecture/Workstreams/Azure-DevOps.md)
3. [GitHub Workstream](../../Architecture/Workstreams/GitHub.md)
4. [BizTalk Server](../../Architecture/Workstreams/BizTalk-Server.md)
5. [EFT and MFT](../../Architecture/Workstreams/EFT-and-MFT.md)

### Attend Recurring Meetings

| Meeting | Day/Time | Purpose |
|---------|----------|---------|
| Daily Standup | Daily at 11:00 AM | Team sync |
| Change Control | Tuesdays at 1:00 PM | Production change approvals |
| Sprint Planning / Retrospectives | Per sprint cadence | Team planning |

---

## Week 4 — First Contribution

- [ ] Investigate and resolve one pipeline failure (with mentor guidance).
- [ ] Make a small IaC change (e.g., add a tag to a resource group) and deploy through Dev.
- [ ] Write a KQL query in Log Analytics to find a specific log event.
- [ ] Review a Pull Request for a pipeline or IaC change.
- [ ] Contribute to or update a page in the Operations/DevOps section of the wiki.

---

## 30 / 60 / 90 Day Goals

| Milestone | Goals |
|-----------|-------|
| **30 Days** | Complete onboarding track training. Understand HIDEX pipeline architecture. Independently investigate pipeline failures. Comfortable with Azure Portal, Monitor, and Log Analytics. |
| **60 Days** | Author a YAML pipeline change end-to-end. Provision a non-production Azure resource via IaC. Manage an access provisioning request. Start AZ-104 certification study. |
| **90 Days** | Lead a production deployment through Change Control. Author a Bicep template for a new resource type. Complete AZ-104 certification. Contribute meaningfully to DevOps documentation. |

---

## Required Training (First 90 Days)

See the [Training Page](./Training.md) for full details. Minimum required within 90 days:

1. Azure DevOps: Getting Started — Pluralsight
2. Azure Administrator (AZ-104) — Udemy
3. Azure DevOps Pipelines: Getting Started — Pluralsight
4. Git: Getting Started — Pluralsight
5. Azure Monitor: Getting Started — Pluralsight

---

## Key Contacts

| Role | Name | Notes |
|------|------|-------|
| DevOps Team Lead | (see Team Roster) | Technical guidance & approvals |
| Development Team Lead | (see Dev Team Roster) | Pipeline & deployment questions |
| Support Team Lead | (see Support Team Roster) | Monitoring & incident coordination |
| Integration Services Manager | (see Teams page) | Access requests, escalations |

---

## Helpful Links

- [Integration Services Wiki Home](../../Integration-Services.md)
- [DevOps Team SOPs](./Standard-Operating-Procedures.md)
- [Training Resources](./Training.md)
- [Position Descriptions](./Position-Descriptions.md)
- [Architecture Overview](../../Architecture.md)
- [Governance: Azure DevOps](../../Governance/Azure-DevOps.md)
- [Azure Naming Conventions](../../Governance/Azure-Naming-Conventions.md)
- [Environments Overview](../../Operations/DevOps/Environments.md)
- [Azure DevOps — HIDEX](https://dev.azure.com/LACDMH-DPH-Integration/HIDEX)
- [Azure DevOps — Administration](https://lacdmh-integrationservices.visualstudio.com/Administration)
