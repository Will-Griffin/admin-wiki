# Team Standards for User Stories, Features, Tasks, and Pull Requests

To ensure consistency, quality, and smooth collaboration, our team follows the standards below when creating and managing User Stories, Features, Tasks, and Pull Requests (PRs).

---

##  User Stories

User Stories define a user's goal and the value they receive from a feature or change.

**Format**:  
> As a *[type of user]*, I want *[goal]* so that *[reason]*.

### Story Checklist
- [ ] Follows the INVEST model (Independent, Negotiable, Valuable, Estimable, Small, Testable)
- [ ] Clear and concise user-centric goal
- [ ] Acceptance Criteria included (Gherkin-style or bullet points)
- [ ] Definition of Done defined
- [ ] Linked to parent Feature or Epic
- [ ] Prioritized and estimated

---

## 🧩 Features (or Epics)

Features describe broader business initiatives broken down into smaller stories.

### Feature Checklist
- [ ] Clearly defined business objective
- [ ] Breaks down into 2+ user stories
- [ ] Aligned to quarterly roadmap or sprint goal
- [ ] Includes success metrics or KPIs (if applicable)
- [ ] Definition of Ready and Done established

---

##  Tasks (or Subtasks)

Tasks represent the specific engineering, testing, or documentation work required to deliver a user story.

###  Task Checklist
- [ ] Technical and implementation-focused
- [ ] Estimated in hours (or story points)
- [ ] Assigned to a team member
- [ ] Clear, actionable, and small in scope (< 1 day ideally)
- [ ] Linked to parent user story

---

## Pull Requests (PRs)

Pull Requests are used to merge code changes into the main branch, with quality and traceability in mind.

###  PR Checklist
- [ ] Title includes Jira ID and brief description (e.g. `[ABC-123] Fix login bug`)
- [ ] Description includes:
  - What was changed
  - Why it was changed
  - How to test it
- [ ] Linked to story/feature
- [ ] Unit and/or integration tests included
- [ ] Reviewed and approved by at least one peer
- [ ] CI/CD pipeline passes
- [ ] No unrelated changes or large diffs

---

##  Definition of Done (Applies to All Items)
- [ ] Requirements or acceptance criteria are met
- [ ] Peer reviewed (for code or documentation)
- [ ] Tests (automated or manual) are passing
- [ ] Documentation is updated (if needed)
- [ ] Deployed to relevant environment
- [ ] Stakeholder or QA sign-off (if required)

---

## 📎 Additional Tips
- Keep communication open via story comments or PR threads
- Avoid overloading stories with implementation details—use tasks for that
- Break down work when stories or PRs get too large to manage effectively

---

Let’s build great software — one clear, valuable, and testable story at a time.
