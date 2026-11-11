# Ross Business Systems Engineering Baseline

Baseline version: `RBS-ENG-1`

This document defines organisation-wide engineering and AI-agent rules for Ross Business Systems repositories.

Project-specific instructions belong in the root `AGENTS.md` and extend this baseline. A project-specific rule may intentionally differ from this baseline only when the exception is explicit, justified and scoped.

---

## 1. Authority and source-of-truth discipline

Identify authoritative sources before implementing projections, caches, dashboards or integrations.

Rules:

- Repository-owned source and planning files remain authoritative for repository state.
- External systems remain authoritative for the records they own.
- Cached, indexed or derived data must be clearly rebuildable where practical.
- Do not silently create editable copies of authoritative data that can drift from their source.
- Preserve source provenance for imported or projected evidence.
- Never silently upgrade estimated, inferred or reconstructed information into measured fact.

When an application projects data from another system, the default model is:

```text
authoritative source
        |
        v
read / retrieve
        |
        v
validate
        |
        v
projection / cache
        |
        v
presentation / decision support
```

---

## 2. Project instruction hierarchy

Before changing a repository:

1. Read `AGENTS.org.md`.
2. Read the root `AGENTS.md`.
3. When the task uses multi-agent implementation, review, remediation or orchestration, read `MULTI_AGENT_DELIVERY.md`.
4. Read the active backlog and architecture documentation relevant to the task.
5. Inspect existing implementation and tests before proposing replacement abstractions.

Repository-specific instructions take precedence only where they explicitly define a justified project exception.

Do not infer a new policy merely because a task is narrow or local. Preserve established repository, deployment and operational state unless the requested work requires it to change.

---

## 3. Delivery discipline

Prefer small, reviewable vertical slices.

Rules:

- One canonical backlog item per implementation branch unless the repository explicitly uses another workflow.
- Do not bundle unrelated cleanup into feature work.
- Do not start the next backlog item merely because the current task finishes early.
- A task is complete only when implementation, tests and required documentation are repository-verifiable.
- Keep code completion separate from operational approval, production rollout or external evidence.
- Review the final diff before declaring completion.
- Verify `git status` contains only intentional changes.

Where pull requests are used:

- address valid review comments with the smallest satisfactory change;
- do not reopen settled architecture without evidence that it is wrong;
- wait for required CI checks before merge;
- prefer squash merge for single-slice delivery unless repository history requires otherwise;
- remove completed feature branches after successful merge unless retention is deliberate.

---

### Pull-request description quality

A pull-request description is part of the review evidence and must be human-readable.

For implementation PRs, use structured Markdown with clear sections appropriate to the change, normally including:

- canonical backlog item;
- implementation outcome;
- architecture/invariants;
- tests and verification;
- documentation/backlog changes;
- limitations/follow-up.

Do not submit PR bodies containing literal escaped newline sequences such as `\n`.
Do not collapse the description into one unstructured paragraph merely to satisfy metadata requirements.

When creating a PR through CLI tooling:

- prefer a temporary Markdown file with `--body-file`, or another mechanism that preserves intended Markdown formatting;
- inspect the rendered PR body after creation;
- correct malformed Markdown before requesting review.

The PR description should be concise, but it must remain useful to a human reviewer and durable as delivery evidence.

---

## 4. Architecture and abstraction discipline

Prefer the smallest abstraction supported by current requirements.

Rules:

- Do not create generic frameworks for hypothetical future providers, workflows or integrations.
- Introduce interfaces at real architectural boundaries, not mechanically around every class.
- Provider-specific models must not leak into provider-neutral domain layers.
- Keep external I/O, persistence, transport and provider SDK concerns outside provider-neutral domain code.
- Favour explicit orchestration over opaque pipeline machinery.
- Preserve graceful degradation when one external source fails and unrelated functionality can still operate.
- Make failure semantics explicit where stale or previous valid state may be retained.

Design for explainability before cleverness.

---

## 5. Security and data handling

Treat all external input as untrusted.

Rules:

- Never commit credentials, API keys, connection secrets, private certificates or tokens.
- Use least-privilege credentials and scopes.
- Keep credentials outside repository manifests and source control.
- Do not log secrets or sensitive payloads wholesale.
- Validate filesystem paths and prevent path traversal.
- Do not execute repository content merely because it was discovered or parsed.
- Sanitise rendered user-controlled markup.
- Keep production data out of automated tests unless an explicitly approved non-destructive integration environment exists.
- Private repository visibility does not make confidential material appropriate for source control.

Potentially destructive or externally consequential operations require clear intent, but do not demand repetitive confirmation when the user has already explicitly specified the operation and the surrounding state to preserve.

---

## 6. Testing and verification

Every implementation slice should have proportionate automated verification.

Prefer:

- unit tests for domain rules and calculations;
- integration tests for filesystem, persistence, transport and adapter boundaries;
- fixture-based tests for external formats;
- end-to-end tests for critical vertical slices where practical.

Tests must cover meaningful failure and unavailable states, not only the happy path.

Do not write automated tests against production business records.

Run the repository-defined restore, build, test, formatting, static-analysis, vulnerability and container checks before declaring work complete where those checks exist.

---

## 7. CI/CD and runtime discipline

CI should provide deterministic evidence, not ceremony.

Rules:

- Keep CI reproducible from documented local commands where practical.
- Do not hard-code one developer machine into workflow logic.
- Use capability/runner labels rather than machine names when self-hosted runners are used.
- Do not weaken security boundaries to make CI convenient.
- Preserve established deployment mode, feature flags, integrations and runtime configuration unless the task explicitly changes them.
- A cosmetic or local application change must not silently change deployment topology or integration mode.
- Report deployment verification using observable evidence such as health status, process state or endpoint checks.

Applications should support repeatable packaging and deployment appropriate to their platform. Containerisation is preferred for server workloads where it improves reproducibility, but must not be imposed where technically inappropriate.

---

## 8. Operational interoperability and DevDash compatibility

All new Ross Business Systems applications should implement the current RBS operational-status contract unless technically inapplicable.

Applications expose evidence. DevDash interprets it.

An application must remain correct and operable when DevDash is unavailable.

At minimum, supported applications should expose or declare:

- stable application/service identity;
- application/build version;
- environment identity;
- basic health;
- declared operational capabilities;
- explicit unsupported, not-configured, partial, failed and stale states where applicable.

Recommended endpoint family:

```text
/internal/ops/v1
/internal/ops/v1/health
/internal/ops/v1/capabilities
/internal/ops/v1/dependencies
/internal/ops/v1/deployment
```

Only expose endpoints that have meaningful data. Capabilities must make optional support discoverable rather than fabricating empty success responses.

Operational endpoints must:

- be read-only by default;
- expose no credentials, secrets or customer payloads;
- preserve timestamps/provenance where relevant;
- evolve additively where practical;
- use explicit status semantics;
- remain non-essential to core application correctness.

Repositories should provide `ops-manifest.yaml` when the current RBS manifest contract applies. The manifest may describe non-secret identity, environment, endpoint, capability and freshness metadata. Credentials belong elsewhere.

---

## 9. Observability and diagnostics

Use structured logging appropriate to the platform.

Important operations should emit enough evidence to diagnose:

- startup and shutdown;
- source refresh or synchronisation lifecycle;
- external dependency failure;
- rejected or malformed input;
- deployment/version identity;
- material background-worker failures;
- projection/index rebuilds where applicable.

Do not confuse telemetry volume with observability quality. Prefer useful, bounded events over noisy logs.

---

## 10. Documentation and decision evidence

Durable architectural and operational decisions belong in repository documentation, ADRs or equivalent project-owned records.

Rules:

- Do not leave authoritative decisions only in chat threads, agent scratch files or pull-request prose.
- Keep documentation close to the implementation it governs.
- Update documentation when a change alters an established contract.
- Do not produce speculative documentation for features that are not yet sufficiently understood.
- Preserve historical provenance when ownership, naming or URLs change unless rewriting history is required for correctness or security.

---

## 11. Workspace hygiene and AI tooling state

AI tooling may create local working state where useful, but repository source state remains authoritative.

Rules:

- AI/tooling state must not be committed unless explicitly part of the project design.
- Agent workspace directories such as `.codex/`, `agents/` or equivalent are local development state.
- Persistent local agent state is acceptable and preferable to repeatedly creating, deleting or relocating the same directories during normal work.
- Tooling metadata must not replace repository documentation, ADRs, backlog files or source code as authoritative project records.
- Temporary files, generated artefacts and agent scratch state should remain outside tracked project content.
- Before completing work, verify `git status` contains only intentional project changes.

---

## 12. Cost and complexity discipline

Prefer the lowest-complexity solution that satisfies demonstrated requirements.

For external services and evidence collection, prefer:

1. local/free collection;
2. already-paid APIs and infrastructure;
3. free allowances/public data;
4. new paid tooling only where decision, operational or diligence value clearly exceeds cost.

Do not introduce distributed infrastructure, queues, search clusters, orchestration platforms or paid telemetry merely because they may become useful later.

---

## 13. Bounded domain triage for review findings

Automated review findings must be classified before implementation.

When a review identifies a new case, determine:

> Does this represent a missing bounded relationship/category within the documented domain, or an unsupported form outside the documented classifier domain?

### Missing bounded relationship/category

A finding belongs here when:

- the behaviour is already implied by the existing contract;
- the semantic category already exists;
- the missing case is a constrained variation.

Examples:

- present/past variants of the same relationship;
- additional supported predicate forms;
- composition of already-supported subject and relationship grammars.

Required action:

- implement the smallest correction;
- add permanent regression coverage;
- preserve existing boundaries;
- update documentation only where the contract changes.

### Unsupported domain expansion

A finding belongs here when:

- it requires unrestricted interpretation;
- it introduces a new semantic category;
- it expands beyond the documented system guarantee.

Required action:

- do not automatically implement;
- document the limitation;
- create a separate design decision if expansion is justified.

### Decision test

Before accepting a review finding:

Ask:

> Can this be represented as a bounded addition to the existing semantic model?

If yes:

implement + regression

If no:

document boundary + defer

## 14. Completion checklist

Before declaring a task complete, confirm:

- the requested scope is implemented;
- architecture boundaries remain intact;
- authoritative sources remain authoritative;
- relevant tests pass;
- repository-defined CI-equivalent checks pass where practical;
- required documentation is updated;
- no credentials or sensitive material were introduced;
- no unrelated implementation stream was started;
- `git status` contains only intentional project changes.
