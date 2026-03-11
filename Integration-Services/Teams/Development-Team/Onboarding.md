# Onboarding Guide — Development Team

[[_TOC_]]

---

## Welcome to the Integration Services Development Team!

This guide is designed to help new Development Team members ramp up quickly on our codebase, processes, and tools. Complete each section in order during your first 90 days.

---

## Week 1 — Orientation & Access

### Day 1–2: Accounts & Access

Work with your manager to request access to the following systems:

| System | Purpose | Request Via |
|--------|---------|------------|
| Azure Portal | Cloud resources & monitoring | Manager / Azure Admin |
| Azure DevOps (HIDEX) | Work items, repos, pipelines | Manager |
| Azure DevOps (Administration) | Secondary ADO org | Manager |
| GitHub (Internal Org) | Source control (post-migration) | Manager |
| Visual Studio / VS Code | IDE | IT Help Desk or self-install |
| Microsoft Teams | Collaboration | IT Help Desk |
| SharePoint / Wiki | Documentation | Manager |
| Azure Key Vault | Secrets (read-only initially) | Manager |

### Dev Environment Setup

- [ ] Install Visual Studio 2022 or VS Code with C# Dev Kit.
- [ ] Install .NET 8 SDK (or latest LTS).
- [ ] Install Git; configure user name and email.
- [ ] Clone primary repositories from Azure DevOps / GitHub.
- [ ] Install Docker Desktop (for local container testing).
- [ ] Install Postman and/or Bruno.
- [ ] Install Azure CLI; run `az login` and verify access.
- [ ] Install Azure Functions Core Tools.

### Day 3–5: Codebase Orientation

- [ ] Review [Integration Services Overview](../../Integration-Services.md).
- [ ] Read [Architecture Overview](../../Architecture.md) and all sub-pages.
- [ ] Review [Development Team SOPs](./Standard-Operating-Procedures.md).
- [ ] Review [Governance Standards](../../Governance/Standards.md).
- [ ] Review [Branch Policy](../../Governance/Azure-DevOps/Branch-Policy.md).
- [ ] Shadow a senior developer for a code walkthrough of the HIDEX FHIR Proxy.
- [ ] Review the current sprint board in Azure DevOps.

---

## Week 2–3 — Deep Dive

### Architecture & Platform Knowledge

Review these wiki articles in depth:

1. [Workstreams — Azure Cloud](../../Architecture/Workstreams/Azure-Cloud.md)
2. [X12 Claim Flow](../../Architecture/Workstreams/Azure-Cloud/X12-Claim-Flow.md)
3. [FHIR API Flow](../../Architecture/Workstreams/Azure-Cloud/FHIR-API-Flow.md)
4. [SOAP Flow](../../Architecture/Workstreams/Azure-Cloud/SOAP-Flow.md)
5. [BizTalk Server](../../Architecture/Workstreams/BizTalk-Server.md)
6. [EFT and MFT](../../Architecture/Workstreams/EFT-and-MFT.md)
7. [Identity & Access Management](../../Architecture/Identity-&-Access-Management.md)
8. [Configuration Management](../../Architecture/Configuration-Management.md)

### DevOps & CI/CD Knowledge

1. [Environments](../../Operations/DevOps/Environments.md)
2. [Branching Strategy](../../Operations/DevOps/Branching-Strategy.md)
3. [Test Strategy](../../Operations/DevOps/Test-Strategy.md)
4. [Postman File Structure](../../Operations/DevOps/Test-Strategy/Postman-file-structure.md)
5. [Load Testing](../../Operations/DevOps/Test-Strategy/Load-Testing.md)

### Attend Recurring Meetings

| Meeting | Day/Time | Purpose |
|---------|----------|---------|
| Daily Standup | Daily at 3:00 PM | Team sync |
| Sprint Planning | Bi-weekly Monday | Sprint commitment |
| Sprint Review/Demo | Bi-weekly Friday | Showcase work |
| Retrospective | Bi-weekly Friday | Process improvement |
| Backlog Refinement | Weekly Wednesday | Groom backlog |

---

## Week 4 — First Contribution

- [ ] Pick up your first task (P3/P4 bug or small enhancement) from the sprint board.
- [ ] Create a feature branch following the naming convention.
- [ ] Implement the change with unit tests.
- [ ] Submit a Pull Request; get it reviewed and merged.
- [ ] Confirm the fix is deployed to Dev environment via pipeline.
- [ ] Document any new operational procedures in the wiki.

---

## 30 / 60 / 90 Day Goals

| Milestone | Goals |
|-----------|-------|
| **30 Days** | Complete onboarding track training. Understand core architecture (HIDEX, BizTalk, EDI flows). Successfully merge at least 2 PRs. Comfortable with Azure Portal and App Insights. |
| **60 Days** | Independently pick up and deliver user stories. Lead code review discussions. Understand FHIR Proxy and APIM policy configurations. Start AZ-204 certification study. |
| **90 Days** | Deliver at least one feature end-to-end (Dev → QA → Prod). Lead a backlog refinement session. Complete AZ-204 certification. Contribute to wiki documentation. |

---

## Required Training (First 90 Days)

See the [Training Page](./Training.md) for full details. Minimum required within 90 days:

1. Microsoft Azure Developer Associate (AZ-204) — Udemy
2. C# Advanced Topics — Udemy
3. REST API Design — Udemy
4. Azure DevOps: Getting Started — Pluralsight
5. Git: Getting Started — Pluralsight

---

## Key Contacts

| Role | Name | Notes |
|------|------|-------|
| Development Team Lead / Senior Dev | (see Team Roster) | Technical questions & PR reviews |
| DevOps Team Lead | (see DevOps Team Roster) | Pipeline & infra questions |
| Support Team Lead | (see Support Team Roster) | Operational escalations |
| Integration Services Manager | (see Teams page) | Access requests, escalations |

---

## Helpful Links

- [Integration Services Wiki Home](../../Integration-Services.md)
- [Development Team SOPs](./Standard-Operating-Procedures.md)
- [Training Resources](./Training.md)
- [Position Descriptions](./Position-Descriptions.md)
- [Architecture Overview](../../Architecture.md)
- [Governance Standards](../../Governance/Standards.md)
- [Azure DevOps — HIDEX](https://dev.azure.com/LACDMH-DPH-Integration/HIDEX)
- [Azure DevOps — Administration](https://lacdmh-integrationservices.visualstudio.com/Administration)
- [Delivery Plan — HIDEX](https://dev.azure.com/LACDMH-DPH-Integration/HIDEX/_deliveryplans/plan/9b7447a8-a3da-4f09-85b2-a9ca2353cd86)
- [Delivery Plan — All Applications](https://lacdmh-integrationservices.visualstudio.com/Administration/_deliveryplans/plan/7b9bedab-07d0-44da-bb91-dcd320df745d)
