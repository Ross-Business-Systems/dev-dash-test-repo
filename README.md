# Ross Business Systems Project Template

Baseline repository template for new Ross Business Systems software projects.

Use this repository as the starting point for new projects, then replace the project-specific placeholders in `AGENTS.md`, `todo.md`, `docs/architecture.md` and `ops-manifest.yaml` before implementation begins.

## Instruction hierarchy

1. `AGENTS.org.md` defines organisation-wide Ross Business Systems engineering rules.
2. `AGENTS.md` defines project-specific rules that extend the organisation baseline.
3. Repository documentation and source files remain authoritative for project decisions and implementation state.

A project-specific rule may intentionally differ from the organisation baseline only when the exception is explicit and justified in `AGENTS.md`.

## Template contents

- `AGENTS.org.md` - organisation engineering baseline.
- `AGENTS.md` - project-specific agent instruction overlay.
- `todo.md` - authoritative active delivery backlog template.
- `docs/architecture.md` - project architecture decision baseline.
- `ops-manifest.yaml` - non-secret operational interoperability manifest template.
- `.editorconfig` - baseline editor conventions.
- `.gitignore` - common generated and AI-tooling local state exclusions.

## Operational interoperability

New Ross Business Systems applications should expose the current RBS operational-status contract unless technically inapplicable. Applications expose evidence; DevDash interprets it. Applications must not depend on DevDash for correctness.
