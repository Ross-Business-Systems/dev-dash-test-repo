# TaskBoard Demo — Development Backlog

> **Purpose:** Synthetic development backlog for testing DevDash repository discovery, progress tracking, dependency parsing, attention views and GitHub source onboarding.
>
> **Project:** TaskBoard Demo  
> **Repository:** `Ross-Business-Systems/dev-dash-test-repo`  
> **Status:** Demonstration fixture, not a production application.
>
> This backlog contains illustrative work only. Checklist completion must reflect actual repository evidence. Completed items should be archived under `docs/archive/` with their original identifiers preserved.

## Current focus

- **PROJECT-1.1:** Define the initial TaskBoard architecture and application boundaries.
- **Next:** PROJECT-1.2, basic project and task management.
- **Blocked:** PROJECT-2 requires completion of PROJECT-1.2.
- **Deferred:** PROJECT-4 analytics and reporting.

## Active delivery

### PROJECT-1 — Application Foundation

Establish the core application structure and minimum viable task-management workflow.

- [ ] **PROJECT-1.1** Define the TaskBoard architecture, technology stack and source-of-truth rules.
- [ ] **PROJECT-1.2** Implement project creation, editing and archival.
  - Depends on PROJECT-1.1.
- [ ] **PROJECT-1.3** Implement task creation, assignment, priority and lifecycle status.
  - Depends on PROJECT-1.2.
- [ ] **PROJECT-1.4** Implement persistent task and project storage.
  - Depends on PROJECT-1.1.
- [ ] **PROJECT-1.5** Add automated unit and integration tests.
  - Depends on PROJECT-1.3 and PROJECT-1.4.
- [ ] **PROJECT-1.6** Establish continuous integration with build, test and formatting checks.
  - Depends on PROJECT-1.5.

### PROJECT-2 — User Experience

Provide a responsive interface for managing tasks.

**Dependency:** PROJECT-1.2 and PROJECT-1.3.

- [ ] **PROJECT-2.1** Create the main project dashboard.
  - Depends on PROJECT-1.2.
- [ ] **PROJECT-2.2** Implement task listing with sorting and filtering.
  - Depends on PROJECT-1.3.
- [ ] **PROJECT-2.3** Add task detail and editing views.
  - Depends on PROJECT-2.2.
- [ ] **PROJECT-2.4** Implement accessible form validation and error handling.
  - Depends on PROJECT-2.3.
- [ ] **PROJECT-2.5** Verify responsive layouts at desktop, tablet and mobile widths.
  - Depends on PROJECT-2.1 through PROJECT-2.4.

### PROJECT-3 — Collaboration

Introduce controlled multi-user functionality.

**Status:** Planned.

- [ ] **PROJECT-3.1** Define user identity and permission boundaries.
  - Depends on PROJECT-1.1.
- [ ] **PROJECT-3.2** Implement project membership and role assignment.
  - Depends on PROJECT-3.1.
- [ ] **PROJECT-3.3** Add task assignment and reassignment.
  - Depends on PROJECT-3.2.
- [ ] **PROJECT-3.4** Record auditable task status changes.
  - Depends on PROJECT-1.3 and PROJECT-3.1.
- [ ] **PROJECT-3.5** Add project activity history.
  - Depends on PROJECT-3.4.

### PROJECT-4 — Analytics and Reporting

**Status:** Deferred until reliable task lifecycle data exists.

- [ ] **PROJECT-4.1** Define task completion and lead-time metrics.
  - Depends on PROJECT-3.4.
- [ ] **PROJECT-4.2** Add project progress reporting.
  - Depends on PROJECT-4.1.
- [ ] **PROJECT-4.3** Implement historical progress snapshots.
  - Depends on PROJECT-4.2.
- [ ] **PROJECT-4.4** Export project summaries to CSV.
  - Depends on PROJECT-4.2.

## Platform and Infrastructure

### PLAT-1 — Deployment Foundation

- [ ] **PLAT-1.1** Define local development environment configuration.
- [ ] **PLAT-1.2** Provide a reproducible container build.
  - Depends on PLAT-1.1.
- [ ] **PLAT-1.3** Implement application health and readiness endpoints.
  - Depends on PROJECT-1.1.
- [ ] **PLAT-1.4** Document deployment and rollback procedures.
  - Depends on PLAT-1.2.
- [ ] **PLAT-1.5** Verify backup and restoration of persistent application data.
  - Depends on PROJECT-1.4 and PLAT-1.2.

## Operational Readiness

Operational items require independent evidence and cannot be completed solely through repository implementation.

### OPS-1 — Security and Access

- [ ] **OPS-1.1** Approve the application's authentication approach.
- [ ] **OPS-1.2** Review credential and secret-management practices.
- [ ] **OPS-1.3** Verify least-privilege deployment permissions.
- [ ] **OPS-1.4** Complete dependency and vulnerability review.

### OPS-2 — Release Preparation

- [ ] **OPS-2.1** Confirm deployment topology and responsible operator.
- [ ] **OPS-2.2** Complete representative user acceptance testing.
  - Depends on PROJECT-2.5.
- [ ] **OPS-2.3** Confirm backup and recovery responsibilities.
  - Depends on PLAT-1.5.
- [ ] **OPS-2.4** Approve first release.
  - Depends on OPS-2.1 through OPS-2.3.

## Known Risks and Blockers

### RISK-1 — Persistence Technology

The reference database has not yet been selected.

**Impact:** PROJECT-1.4 cannot be completed until persistence requirements and constraints are established.

**Mitigation:** Resolve the database decision within PROJECT-1.1 and document its rationale.

### RISK-2 — Authentication Scope

Multi-user collaboration introduces new identity and authorisation requirements.

**Impact:** PROJECT-3 is not ready for unrestricted implementation.

**Mitigation:** Complete PROJECT-3.1 before developing membership and sharing capabilities.

### RISK-3 — Deployment Environment

The production hosting model is not yet selected.

**Impact:** PLAT-1.4 and OPS-2 cannot be fully completed.

**Mitigation:** Define a reproducible local environment without assuming production infrastructure.

## Definition of Done

An implementation item is complete only when:

- [ ] Its stated functionality is implemented.
- [ ] Applicable unit and integration tests pass.
- [ ] The solution builds without errors.
- [ ] Required CI checks pass.
- [ ] Review findings are addressed.
- [ ] Documentation reflects the implemented state.
- [ ] Changes are merged into the authoritative branch.
- [ ] Completed work is archived with its original identifier.

## Roadmap

| Phase | Scope | Status |
|---|---|---|
| 1 | Application foundation | Planned |
| 2 | User experience | Planned |
| 3 | Collaboration | Planned |
| 4 | Analytics | Deferred |
| 5 | Production deployment | Dependent on operational approval |

---

*This file is a synthetic DevDash integration fixture. It does not constitute evidence that any TaskBoard functionality has been implemented.*
