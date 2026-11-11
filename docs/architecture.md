# Architecture

## Status

Template. Replace placeholder sections with project-specific architecture before implementation materially progresses.

## Purpose

Describe the system's architectural goals and the constraints that matter.

## Authoritative sources

List each authoritative source and distinguish it from caches, indexes, projections and imported evidence.

## Solution boundaries

Describe major modules/projects/services and allowed dependency direction.

## Data and persistence

Describe authoritative data stores, rebuildable projection state, retention and migration strategy.

## External integrations

Document each real integration only when introduced. Include ownership, failure semantics, authentication boundary and graceful-degradation behaviour.

## Operational interoperability

Describe the implemented RBS operational-status contract, endpoint locations, declared capabilities and `ops-manifest.yaml` relationship.

Applications expose evidence; DevDash interprets it. DevDash must not become a runtime dependency of the application.

## Security boundaries

Document untrusted input, sensitive data, secrets, permissions and prohibited flows.

## Verification

Record the canonical local commands and CI-equivalent verification path.

## Deferred decisions

Record important unresolved architecture decisions without prematurely implementing them.
