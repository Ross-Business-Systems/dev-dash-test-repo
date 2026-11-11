# Ross Business Systems Multi-Agent Delivery Standard

Status: organisation-wide engineering policy.

This standard extends `AGENTS.org.md`. Repository-specific `AGENTS.md` may specialise it only through an explicit, justified and scoped exception.

## Purpose

Use AI-agent parallelism to increase delivery throughput without weakening architecture, review quality, traceability or repository discipline.

The default model is one accountable orchestrator coordinating bounded implementation, review, remediation and specialist agents. The objective is maximum safe parallel progress against canonical backlog items, not maximum concurrent activity.

## Authority hierarchy

Before work begins, agents follow this order:

1. `AGENTS.org.md`.
2. repository `AGENTS.md`.
3. canonical backlog and relevant architecture/decision records.
4. existing implementation and tests.
5. orchestrator assignment.

The orchestrator may sequence and decompose work but may not silently override settled architecture or authoritative project sources.

## Team roles

A multi-agent team normally contains:

- **Orchestrator**: package interpretation, sequencing, ownership boundaries, integration and closure.
- **Implementation agents**: one bounded backlog item or explicitly partitioned sub-slice each.
- **Review agent**: independent review against requirements, architecture, tests and failure semantics.
- **Remediation agent**: smallest satisfactory repair for accepted findings.
- **Specialist agents** where useful: domain, persistence, UI, security, testing, documentation or migration.

One agent may hold more than one role for small packages, but role accountability must remain explicit.

## Orchestrator responsibilities

The orchestrator must:

- read the canonical backlog and dependency graph before delegation;
- identify the exact delivery package and repository head;
- classify candidate work as `SERIAL`, `PARALLEL-SAFE` or `PARALLEL-AFTER-CONTRACT`;
- define implementation boundaries and expected outputs for every agent;
- prevent competing ownership of the same mutable contract or surface;
- preserve one canonical backlog item per branch unless the repository explicitly differs;
- settle shared contracts before dependent parallel implementation starts;
- stop or resequence work if a discovered dependency invalidates parallel assumptions;
- integrate branches in dependency-safe order;
- require repository-defined verification and CI against the exact integration head;
- reconcile review findings before closure;
- update backlog, ADRs and documentation when implementation changes settled assumptions;
- produce a final closeout covering implementation, verification, limitations and follow-up.

The orchestrator is accountable for integration correctness even when it writes little or no production code.

## Parallelisation classes

### SERIAL

Use when an item defines contracts, architecture, schema/migration state or another prerequisite required by later work, or when concurrent edits create high integration risk.

### PARALLEL-AFTER-CONTRACT

Use when multiple slices can proceed independently only after a shared interface, schema, domain invariant or migration boundary is frozen and verified.

### PARALLEL-SAFE

Use when contracts are settled, edit surfaces are distinct, verification is independent and merge/integration risk is low.

Idle agents are never sufficient reason to classify work as parallel-safe.

## Parallelisation decision test

Before parallelising, the orchestrator should be able to answer yes to the applicable questions:

- Are shared contracts explicit and settled?
- Can each agent state its ownership/edit surface?
- Can each slice be tested independently?
- Can integration order be predetermined or safely reconciled?
- Will one slice remain semantically valid if another implementation detail changes?
- Is there a deterministic integration verification path?

If not, keep the work serial or freeze the missing contract first.

## Agent assignment contract

Every implementation-agent assignment must identify:

- canonical backlog item or explicit sub-slice;
- repository and starting ref/head;
- agent name, role and scope;
- authoritative documents to read;
- expected modules/files where useful;
- dependencies assumed settled;
- architecture/security invariants;
- required tests and verification;
- prohibited adjacent scope;
- expected handoff format.

Agents must not begin unrelated backlog items after completing their assignment.

## Implementation-agent handoff

Each implementation agent returns a concise evidence package containing:

- implemented scope;
- files/modules changed;
- contracts or migrations introduced/changed;
- tests added/updated;
- verification commands and outcomes;
- unresolved limitations or risks;
- new review-worthy findings;
- branch/head/PR identity where applicable.

The handoff is evidence for the orchestrator, not a substitute for repository inspection.

## Shared surfaces

Prefer domain/module ownership over arbitrary file splitting.

When two agents require the same public contract or shared file, use one of these patterns:

1. one agent owns the contract first, then dependent agents start;
2. one integration agent owns the shared surface while specialists contribute isolated implementations;
3. keep the work serial.

Do not let several agents independently evolve the same public contract and rely on merge conflict resolution to decide semantics.

## Branch and PR discipline

The organisation delivery baseline remains in force:

- one canonical backlog item per implementation branch by default;
- draft PR while implementation/review is active;
- human-readable PR description with item, outcome, invariants, verification and follow-up;
- required automated review and CI before merge;
- squash merge for a bounded slice unless repository history requires otherwise;
- delete completed branches unless retention is deliberate.

For parallel teams, independent backlog items normally retain independent branches/PRs. Do not create a giant umbrella implementation branch merely because one orchestrator owns the package.

## Review and finding triage

Implementation and review remain separable.

Review should inspect requirement coverage, architecture boundaries, failure/unavailable states, persistence/migration correctness, security/trust boundaries, concurrency/idempotency where relevant, test adequacy, documentation consistency and unintended expansion.

Automated findings must be triaged under the bounded-domain rules in `AGENTS.org.md` before implementation.

Accepted findings become one of:

- immediate bounded repair;
- explicit remediation backlog item;
- documented limitation/deferred work;
- rejected finding with rationale.

## Remediation

A remediation agent receives the accepted finding, evidence, affected contract and smallest required correction scope.

Remediation must not become a stealth redesign. Valid defects require permanent regression coverage. Re-run relevant review and exact-head CI after material repair.

## Integration gate

Before closing a multi-agent package:

- all intended items are integrated in dependency-safe order;
- no unreviewed agent branch is treated as complete merely because it builds locally;
- the final integration head passes repository-defined verification;
- required current-head CI/checks are green;
- review findings are resolved, explicitly deferred or converted to canonical backlog work;
- docs/backlog/ADRs match final implementation state;
- no unrelated changes remain;
- settled state, current implementation, planned work, deferred work and unresolved questions are distinguished.

## Naming and role identity

Agent names may be memorable, but every assignment maps the name to a concrete role and item.

Example:

```text
Volta  — Domain            — SYS-1.1
Curie  — Persistence       — SYS-1.2
Turing — Adversarial Tests — SYS-1.3
Picard — Review
Stark  — Remediation
```

The backlog item and role are the durable identity, not the nickname.

## Specialist-team pattern

For a large bounded item, the orchestrator may assign domain/model, persistence/migration, UI/client, testing/adversarial, security/trust-boundary or documentation/reconciliation specialists.

Use this only when shared contracts are stable enough to avoid competing ownership.

## Model and reasoning allocation

Use stronger reasoning capacity for orchestration, architecture, ambiguous review triage and cross-cutting remediation. Use implementation-optimised agents for bounded coding once contracts are clear.

Do not spend premium reasoning capacity merely to duplicate deterministic implementation work. Do not delegate unresolved architecture to implementation agents solely to maximise concurrency.

## Evidence and economics

Where practical, preserve enough evidence for DevDash or later RBS tooling to correlate:

- agent role/model;
- backlog item;
- branch/PR;
- founder review/rework time;
- accepted, rejected or abandoned outcome;
- review findings;
- merged/released state;
- estimated or measured AI cost basis where available.

Do not equate token volume, branch count or agent count with value. The useful measure is reviewed, integrated outcome relative to founder attention and cost.

## Documentation and decisions

Material decisions discovered during orchestration belong in canonical project sources during the same session where practical.

Do not leave architecture changes, accepted limitations, terminology or dependency changes only in transcripts or PR comments.

## Founder role

In founder-led delivery, the founder remains final product/architecture authority unless explicitly delegated. Multi-agent orchestration should shift founder effort away from serial implementation and toward problem framing, contract design, decomposition, review judgement, commercial/product decisions, exceptional debugging and final acceptance.

Optimise founder attention, not the number of agents requiring supervision.

## Failure modes

Do not:

- parallelise unresolved architecture;
- let agents silently redefine public contracts;
- allow overlapping ownership without an integration plan;
- merge because several agents independently report success;
- accept review findings without bounded-domain triage;
- create undocumented agent-specific architecture;
- let implementation agents start adjacent backlog items;
- use agent activity as a proxy for progress/value;
- hide rejected or abandoned work from later evidence;
- let orchestrator summaries replace repository-verifiable state.

## Project adoption

New RBS software repositories should carry this file with `AGENTS.org.md` and `AGENTS.md` through the Project Template. Existing repositories adopt it incrementally; adoption does not reopen completed work solely to conform history to the standard.

## Minimum kickoff contract

A multi-agent kickoff specifies:

- objective and canonical package;
- current repository state/head;
- dependency graph;
- parallelisation classification;
- named agents with roles/items;
- shared contracts and prohibited overlap;
- branch/PR strategy;
- verification/review gates;
- integration order;
- stop/escalation conditions;
- final reconciliation requirements.

## Completion test

The workflow succeeds when increased parallelism reduces founder implementation burden while preserving or improving correctness, traceability, review quality and architectural coherence.
