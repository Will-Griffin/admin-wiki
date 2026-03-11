# Standard Operating Procedures — Development Team

[[_TOC_]]

---

## Overview

This document defines the standard operating procedures for the Integration Services Development Team. It covers the software development lifecycle (SDLC), code quality standards, deployment procedures, and team collaboration practices.

---

## 1. Work Item & Sprint Management

### 1.1 Creating & Managing Work Items

All development work must be tracked in Azure DevOps.

| Work Item Type | Criteria |
|---------------|----------|
| **Epic** | Major business initiative spanning multiple sprints |
| **Feature** | Functional capability deliverable within a sprint or two |
| **User Story** | End-user value; follows "As a [user], I want [goal] so that [reason]" format |
| **Task** | Technical subtask; < 1 day ideally; linked to a User Story |
| **Bug** | Defect in existing functionality; includes repro steps and expected vs actual behavior |

- All work items must be linked to a parent (Story → Feature → Epic).
- Stories must include Acceptance Criteria and Definition of Done before entering a sprint.
- Estimates are required before sprint planning.
- See [Team Standards](../../Governance/Standards.md) for full work item guidelines.

### 1.2 Sprint Cadence

| Event | Frequency | Day/Time |
|-------|-----------|----------|
| Sprint Planning | Bi-weekly | Monday |
| Daily Standup | Daily | 3:00 PM |
| Sprint Review / Demo | Bi-weekly | Friday |
| Retrospective | Bi-weekly | Friday (after Review) |
| Backlog Refinement | Weekly | Wednesday |

---

## 2. Development Workflow

### 2.1 Branching Strategy

Follow the [Branching Strategy](../../Operations/DevOps/Branching-Strategy.md) defined in Operations:

```
main
  └── features/{task|story-id}-short-description
```

- **Never commit directly to `main`.**
- All changes require a Pull Request (PR) with at least one approved reviewer.
- Delete feature branches after merge.

### 2.2 Commit Message Standards

```
[{Story/Task ID}] Short imperative description (max 72 chars)

Optional: Longer explanation of why the change was made.
```

Example:
```
[1234] Add retry logic to FHIR proxy authentication

Adds exponential backoff retry policy to handle transient Azure AD
token acquisition failures observed in production.
```

### 2.3 Pull Request Checklist

Before submitting a PR:

- [ ] Branch is up to date with `main`.
- [ ] Code compiles with no errors or warnings.
- [ ] Unit tests added or updated; all tests pass.
- [ ] Integration tests validated in local or dev environment.
- [ ] No hardcoded secrets, connection strings, or credentials.
- [ ] All configuration values are externalized (Azure App Configuration / Key Vault).
- [ ] PR title includes story/task ID (e.g., `[1234] Fix authentication retry`).
- [ ] PR description explains **what** changed, **why**, and **how to test**.
- [ ] Linked to the work item in Azure DevOps.
- [ ] Requested at least one reviewer.
- [ ] Pipeline passes.

See [Branch Policy](../../Governance/Azure-DevOps/Branch-Policy.md) for enforcement rules.

---

## 3. Code Quality Standards

### 3.1 General Principles

- Follow SOLID design principles.
- Keep functions and methods small and focused (Single Responsibility).
- Write self-documenting code; add comments only when logic is non-obvious.
- Prefer configuration over hardcoding.
- All secrets must be stored in **Azure Key Vault** — never in code or config files.

### 3.2 Language-Specific Guidelines

#### C# / .NET
- Follow Microsoft .NET coding conventions.
- Use `async`/`await` for all I/O-bound operations.
- Use `IOptions<T>` pattern for configuration binding.
- Use structured logging with `ILogger<T>` and Application Insights.

#### YAML (Azure Pipelines)
- Parameterize all environment-specific values.
- Use pipeline templates for reusable stages and steps.
- Reference pipeline documentation: [DevOps Test Strategy](../../Operations/DevOps/Test-Strategy.md)

### 3.3 Security Standards

- No plaintext secrets in repositories or pipelines.
- All Azure resources must use Managed Identity where possible.
- RBAC must follow principle of least privilege.
- See [Identity & Access Management](../../Architecture/Identity-&-Access-Management.md) for details.

---

## 4. Code Review Standards

### 4.1 Reviewer Responsibilities

- Respond to PR review requests within **1 business day**.
- Review for: correctness, security, performance, readability, and test coverage.
- Use Azure DevOps PR comments for specific feedback (not email or chat).
- Approve only when satisfied; request changes if issues are found.

### 4.2 Author Responsibilities

- Address all reviewer comments before merging.
- Mark resolved comments as resolved (not the reviewer's job).
- Do not squash reviewer history — use merge commits for traceability.

---

## 5. Testing Standards

### 5.1 Testing Requirements

| Test Type | Who Writes | When |
|-----------|-----------|------|
| Unit Tests | Developer | With the feature code |
| Integration Tests | Developer | Before PR merge |
| API Tests (Postman/Bruno) | Developer + Support | Before promoting to QA |
| Load Tests | Developer + DevOps | Before major releases |

### 5.2 Test Coverage Goals

- Minimum **70% unit test code coverage** for new code.
- All critical paths (authentication, data transformation, error handling) must be covered.

See [Test Strategy](../../Operations/DevOps/Test-Strategy.md) and [API Test Strategy](../../Operations/API-Services/Test-Strategy.md).

---

## 6. Deployment Procedures

### 6.1 Environment Promotion

```
Dev → QA → Staging → Production
```

- All deployments must go through CI/CD pipelines — **no manual deployments to QA or higher**.
- Production deployments require an approved Change Control request.
- Deployments to Production are scheduled during maintenance windows (unless P1 hotfix).

### 6.2 Hotfix Procedure

1. Create a `hotfix/{issue-id}-description` branch from `main`.
2. Implement the fix; get an expedited PR review (minimum 1 approver).
3. Deploy to QA; get Support Team sign-off.
4. Submit emergency Change Control request.
5. Deploy to Production; monitor for 30 minutes post-deployment.
6. Merge hotfix branch back to `main`.
7. Document the incident in the HEAT ticket.

See [Environments](../../Operations/DevOps/Environments.md) for environment approver details.

---

## 7. Azure App Configuration & Secrets

- All environment-specific configuration must be stored in **Azure App Configuration**.
- All secrets (connection strings, API keys, certificates) must be stored in **Azure Key Vault**.
- No configuration values should differ between environments based on hardcoded strings — use feature flags or configuration labels.

See [Configuration Management](../../Architecture/Configuration-Management.md).

---

## 8. On-Call & Support Escalation

- The Development Team provides Tier 2/3 escalation support for incidents triaged by the Support Team.
- P1 escalations may require immediate response outside business hours.
- Rotational on-call schedule is maintained by the Development Team Lead and shared with the Support Team.
- All escalations must be documented in the HEAT ticket with root cause and fix.

---

## 9. Documentation Requirements

- All new APIs must have an OpenAPI/Swagger specification committed to the repository.
- All architectural decisions must be documented in an Architecture Decision Record (ADR) in the wiki.
- Runbooks for operational procedures must be created in the Operations section of the wiki.
- Update relevant wiki pages with every sprint release.

---

## 10. Key Contacts & Resources

| Resource | Link |
|----------|------|
| Azure DevOps (HIDEX) | https://dev.azure.com/LACDMH-DPH-Integration/HIDEX |
| Azure DevOps (Administration) | https://lacdmh-integrationservices.visualstudio.com/Administration |
| HIDEX Delivery Plan | https://dev.azure.com/LACDMH-DPH-Integration/HIDEX/_deliveryplans/plan/9b7447a8-a3da-4f09-85b2-a9ca2353cd86 |
| GitHub (Integration Services) | Internal GitHub organization |
| Architecture Docs | [Architecture Overview](../../Architecture.md) |
| Governance Standards | [Standards](../../Governance/Standards.md) |
| Branch Policy | [Branch Policy](../../Governance/Azure-DevOps/Branch-Policy.md) |
