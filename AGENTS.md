# AGENTS.md

Read and follow [`AGENTS.org.md`](AGENTS.org.md) first.

When the task uses multi-agent implementation, review, remediation or orchestration, also read and follow [`MULTI_AGENT_DELIVERY.md`](MULTI_AGENT_DELIVERY.md) after this project-specific overlay and before beginning delivery work.

This file contains project-specific instructions that extend the Ross Business Systems engineering baseline.

Where this project intentionally differs from the organisation baseline, document the exception explicitly here with its rationale and scope.

---

## Project purpose

Describe what this project exists to do, its users and the problem it solves.

---

## Technology baseline

List project-specific languages, frameworks, runtime versions, persistence, testing and deployment technologies.

Do not repeat organisation-wide rules unless this project intentionally specialises them.

---

## Architecture boundaries

Describe the solution/module boundaries and dependency direction that must be preserved.

Include the authoritative architecture document path where applicable.

---

## Source-of-truth rules

Identify the authoritative source for each important class of project data.

Explicitly distinguish authoritative records from caches, projections and imported evidence.

---

## Development and delivery workflow

Document project-specific branch, pull-request, CI and merge conventions.

If the repository intentionally works directly on `main`, state that explicitly here.

For multi-agent implementation, review, remediation or orchestration, the organisation-wide workflow in [`MULTI_AGENT_DELIVERY.md`](MULTI_AGENT_DELIVERY.md) applies unless this section documents an explicit, justified and scoped exception.

---

## Review finding triage

When automated review discovers new behaviour, classify the finding before implementation.

Determine whether it is:
- a missing bounded addition to an existing contract; or
- an unsupported expansion outside the documented domain.

Do not expand deterministic systems through heuristic accumulation.

---

## Runtime and deployment constraints

Document supported development/runtime topology, deployment environments and state that must be preserved during routine redeployments.

---

## Security and data boundaries

Document project-specific sensitive data, credentials, trust boundaries and prohibited data handling.

---

## Testing requirements

Document project-specific verification commands, integration fixtures and any systems automated tests must never modify.

---

## Delivery sequencing

Reference the active root `todo.md` and record any ordering constraints that agents must preserve.

Do not begin a later implementation stream merely because an earlier item completes unless explicitly instructed.

---

## Project-specific operational interoperability

Document which RBS operational-status capabilities this project implements and any justified omissions from the organisation baseline.
